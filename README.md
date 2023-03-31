# Total Repos Size

A simple website to calculate the combined size of all your GitHub repositories.

**NOTICED**: IT'S ONLY FOR **PUBLIC** REPOSITORIES AND IT'S DIFFERENT FROM THE SIZE DOWNLOADED BY CLONING.

一個簡單計算您所有 GitHub 存儲庫總大小的網站。

**注意**: 這個網站僅計算**公開**的 GitHub Repos 的大小，並非下載後的大小。

## Built with

![https://svelte.dev/](https://img.shields.io/badge/Svelte-4A4A55?style=for-the-badge&logo=svelte&logoColor=FF3E00) ![https://github.com/sveltejs/kit](https://img.shields.io/badge/SvelteKit-FF3E00?style=for-the-badge&logo=Svelte&logoColor=white) ![GitHub](https://img.shields.io/badge/GitHub-100000?style=for-the-badge&logo=github&logoColor=white)

- 前端框架(Frontend Framework): [Svelte](https://github.com/sveltejs/svelte)
- API 串接(API Integration): [GitHub API](https://docs.github.com/en/rest)

## TODO List

- [x] 顯示使用者上所有 GitHub Repos 的總大小
      Display the total size of all user's GitHub Repos
- [x] 新增暗色模式
      Add Dark Mode
- [ ] 關於頁面
      About Page
- [ ] 如果使用者輸入不存在的 GitHub 帳號，要有錯誤訊息
      If the user enters a non-existent GitHub account, an error message should be displayed.

## Usage

### 1. 複製儲存庫至本地 Clone this repository

```bash
git clone https://github.com/xxrjun/total-repos-size.git
```

### 2. 安裝套件 Install dependencies

```bash
# Using npm
npm install
```

### 3. 運行應用程式(開發模式) Start the app in development mode

```bash
npm run dev
```

### 4. 打包應用程式 Build the app

```bash
npm run build
```

### 5. 運行應用程式(產品模式) Start the app in production mode

```bash
npm run start
```