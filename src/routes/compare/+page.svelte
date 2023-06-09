<script>
	import { onMount } from 'svelte';
	import axios from 'axios';

	let userId1 = '';
	let userId2 = '';
	let totalRepos1 = 0;
	let totalRepos2 = 0;
	let totalSize1 = '';
	let totalSize2 = '';
	let compareResult = '';
	let errorMessage1 = '';
	let errorMessage2 = '';
	let timestamp1 = '';
	let timestamp2 = '';

	// Calculate the total size of all repositories
	async function calculate() {
		if (userId1) {
			try {
				const response = await axios.get(`https://api.github.com/users/${userId1}/repos`);
				const repositories = response.data;

				totalRepos1 = repositories.length;
				const totalSize = repositories.reduce(
					(/** @type {any} */ acc, /** @type {{ size: any; }} */ repo) => acc + repo.size,
					0
				);

				totalSize1 = formatSize(totalSize);
				timestamp1 = new Date().toLocaleString();
			} catch (error) {
				totalRepos1 = 0;
				totalSize1 = '';
				errorMessage1 = error;
			}
		} else {
			totalRepos1 = 0;
			totalSize1 = '';
			compareResult = '';
		}

		if (userId2) {
			try {
				const response = await axios.get(`https://api.github.com/users/${userId2}/repos`);
				const repositories = response.data;

				totalRepos2 = repositories.length;
				const totalSize = repositories.reduce(
					(/** @type {any} */ acc, /** @type {{ size: any; }} */ repo) => acc + repo.size,
					0
				);
				totalSize2 = formatSize(totalSize);
				timestamp2 = new Date().toLocaleString();
			} catch (error) {
				totalRepos2 = 0;
				totalSize2 = '';
				errorMessage2 = error;
			}
		} else {
			totalRepos2 = 0;
			totalSize2 = '';
			compareResult = '';
		}
	}

	// Show total size in all kind of human-readable formats
	/**
	 * @param {number} size
	 */
	function formatSize(size) {
		if (size < 1024 * 1024) {
			return `${size.toFixed(2)} KB ( ${(size / 1024).toFixed(2)} MB)`;
		} else if (size < 1024 * 1024 * 1024) {
			return `${(size / 1024).toFixed(2)} MB ( ${(size / 1024 / 1024).toFixed(2)} GB)`;
		} else {
			return `${(size / 1024 / 1024).toFixed(2)} GB ( ${(size / 1024 / 1024 / 1024).toFixed(
				2
			)} TB)`;
		}
	}

	onMount(() => {});
</script>

<svelte:head>
	<title>Compare | GitHub Repository Size Calculator</title>
	<meta name="description" content="GitHub Repository Size Calculator" />
</svelte:head>

<section class="container">
	<h1 class="title">GitHub Repository Size Calculator</h1>

	<form on:submit|preventDefault={calculate}>
		<div class="grid">
			<div class="card">
				<label class="label" for="userId1">GitHub ID 1</label>
				<input class="input" type="text" id="userId1" bind:value={userId1} />
				<button class="button" on:click={calculate}>Calculate</button>
				{#if totalRepos1 !== null}
					<div class="result">
						<p>
							User <span class="username">{userId1}</span> has
							<span class="repos">{totalRepos1}</span>
							public repositories, and the total size is
							<span class="size">{totalSize1}</span>
						</p>
						<span class="time">{timestamp1}</span>
					</div>
				{/if}
			</div>
			<div class="card">
				<label class="label" for="userId2">GitHub ID 2</label>
				<input class="input" type="text" id="userId2" bind:value={userId2} />
				<button class="button" on:click={calculate}>Calculate</button>
				{#if totalRepos2 !== null}
					<div class="result">
						<p>
							User <span class="username">{userId2}</span> has
							<span class="repos">{totalRepos2}</span>
							public repositories, and the total size is
							<span class="size">{totalSize2}</span>
						</p>
						<span class="time">{timestamp2}</span>
					</div>
				{/if}
			</div>
		</div>
	</form>
</section>

<style>
	.container {
		display: flex;
		flex-direction: column;
		align-items: center;
		margin: 2rem;
	}

	.title {
		font-size: 2rem;
		font-weight: bold;
		margin-bottom: 2rem;
	}

	form {
		width: 100%;
	}

	.grid {
		display: grid;
		grid-template-columns: repeat(auto-fit, minmax(20rem, 1fr));
		grid-gap: 2rem;
	}

	.card {
		border-radius: 0.5rem;
		padding: 1rem;
		background-color: #f7f7f7;
		box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
	}

	.label {
		display: block;
		font-size: 1.2rem;
		font-weight: bold;
		margin-bottom: 0.5rem;
	}

	.input {
		padding: 0.5rem;
		border-radius: 0.5rem;
		border: none;
		background-color: #fff;
		box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
		width: 100%;
		margin-bottom: 1rem;
	}

	.button {
		padding: 0.5rem 1rem;
		border-radius: 0.5rem;
		border: none;
		background-color: #007bff;
		color: #fff;
		font-weight: bold;
		cursor: pointer;
		transition: background-color 0.2s ease;
	}

	.button:hover {
		background-color: #0062cc;
	}

	.result {
		margin-top: 1rem;
	}

	.result p {
		font-size: 1.2rem;
		line-height: 1.5;
	}

	.username {
		font-weight: bold;
	}

	.repos {
		font-weight: bold;
		margin: 0 0.2rem;
	}

	.size {
		font-weight: bold;
		margin: 0 0.2rem;
	}

	.time {
		/* position: absolute; */
		bottom: 1rem;
		right: 1rem;
		font-size: 0.8rem;
		font-weight: bold;
		color: #666;
		font-family: Arial, sans-serif;
	}

	@media screen and (max-width: 640px) {
		.container {
			margin: 0rem;
		}

		form {
			width: 100%;
			/* grid-template-columns: 1rem repeat(auto-fill, 100px) 1rem; */
			padding: 0 0.5rem;
		}
		.grid {
			grid-template-columns: 1fr;
		}
	}
</style>
