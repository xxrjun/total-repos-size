<script>
	import { page } from '$app/stores';
	import { onMount } from 'svelte';
	import github from '$lib/images/github.svg';

	onMount(() => {
		const checkbox = document.getElementById('checkbox');

		checkbox?.addEventListener('change', () => {
			document.body.classList.toggle('dark');
		});
	});
</script>

<header>
	<div class="corner">
		<div>
			<input type="checkbox" class="checkbox" id="checkbox" />
			<label for="checkbox" class="label">
				<i class="fas fa-moon" />
				<i class="fas fa-sun" />
				<div class="ball" /></label
			>
		</div>
	</div>

	<nav>
		<svg viewBox="0 0 2 3" aria-hidden="true">
			<path d="M0,0 L1,2 C1.5,3 1.5,3 2,3 L2,0 Z" />
		</svg>
		<ul>
			<li aria-current={$page.url.pathname === '/' ? 'page' : undefined}>
				<a href="/">Home</a>
			</li>
			<li aria-current={$page.url.pathname === '/compare' ? 'page' : undefined}>
				<a href="/compare">Compare</a>
			</li>
			<li aria-current={$page.url.pathname === '/about' ? 'page' : undefined}>
				<a href="/about">About</a>
			</li>
		</ul>
		<svg viewBox="0 0 2 3" aria-hidden="true">
			<path d="M0,0 L0,3 C0.5,3 0.5,3 1,2 L2,0 Z" />
		</svg>
	</nav>

	<div class="corner">
		<a href="https://github.com/xxrjun/total-repos-size">
			<img src={github} alt="GitHub" />
		</a>
	</div>
</header>

<style>
	header {
		display: flex;
		justify-content: space-between;
	}

	.corner {
		width: 5em;
		height: 5em;
	}

	.corner a {
		display: flex;
		align-items: center;
		justify-content: center;
		width: 100%;
		height: 100%;
	}

	.corner img {
		width: 4em;
		height: 4em;
		object-fit: contain;
	}

	.checkbox {
		opacity: 0;
		position: absolute;
		width: 100%;
	}

	.label {
		width: 50px;
		height: 26px;
		background-color: #111;
		display: flex;
		border-radius: 50px;
		align-items: center;
		justify-content: space-between;
		padding: 5px;
		margin: 1.5em 2em;
		position: relative;
		transform: scale(1.5);
	}

	.ball {
		width: 22px;
		height: 22px;
		background-color: white;
		position: absolute;
		top: 2px;
		left: 2px;
		border-radius: 50%;
		transition: transform 0.2s linear;
	}

	/*  target the elemenent after the label*/
	.checkbox:checked + .label .ball {
		transform: translateX(22px);
	}

	.fa-moon {
		color: rgb(234, 255, 0);
	}

	.fa-sun {
		color: yellow;
	}

	nav {
		display: flex;
		justify-content: center;
		--background: rgba(255, 255, 255, 0.7);
	}

	svg {
		width: 2em;
		height: 3em;
	}

	path {
		fill: var(--background);
	}

	ul {
		position: relative;
		padding: 0;
		margin: 0;
		height: 3em;
		display: flex;
		justify-content: center;
		align-items: center;
		list-style: none;
		background: var(--background);
		background-size: contain;
	}

	li {
		position: relative;
		height: 100%;
		margin: 0 0.5rem;
	}

	li[aria-current='page']::before {
		--size: 8px;
		content: '';
		width: 0;
		height: 0;
		position: absolute;
		top: 0;
		left: calc(50% - var(--size));
		border: var(--size) solid transparent;
		border-top: var(--size) solid var(--color-theme-1);
	}

	nav a {
		display: flex;
		height: 100%;
		width: 69px;
		align-items: center;
		justify-content: center;
		padding: 0 0.5rem;
		color: var(--color-text);
		font-weight: 700;
		font-size: 0.8rem;
		text-transform: uppercase;
		letter-spacing: 0.1em;
		text-decoration: none;
		transition: color 0.2s linear;
	}

	a:hover {
		color: var(--color-theme-1);
	}
</style>
