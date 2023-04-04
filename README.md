# Laravel + Nginx + Docker Startup Example

* 以 Docker 帶動 Nginx + Laravel 專案的示範倉庫
* 使用 [wujidadi/nginx-php](https://github.com/Wujidadi/Dockerfiles/tree/main/nginx-php) 映像檔作為基底

## Quick Start

1. 先在根目錄執行 `cp .env.example .env` 建立你的環境設定檔。
2. 將 `.env` 中的設定修改為你的專案配置。
3. 修改 `config/docker/Dockerfile` 中你要使用的基底映像檔。
4. 回到根目錄下執行 `./build` 拉起 Docker 容器。
   > 注意：務必用 `./build` 指令來啟動專案，不要用 `docker-compose up -d`！  
   > 原因有二：
   > 1. 必須先檢查 `zsh` 資料夾下是否存在 `root.zsh_history` 及 `user.zsh_history` 2 個檔案，不存在須先建立  
   >    否則掛載 volume 的時候會因為自動建立成資料夾，導致整個容器啟動失敗。
   > 2. Apple M2 晶片電腦上 Docker Compose 的 `build` 選項會遇到 `DeadlineExceeded` 與 `i/o timeout` 錯誤，  
   >    無法直接從 `docker-compose.yml` 建立映像檔，因此須先手動建立映像檔，而這部分就寫在 `./build` 裡。
5. 再到 `src` 目錄下 (最好是在 Docker 容器內) 執行 Laravel 與 Node.js 的初始化指令  
   參考指令：
   ```bash
   cp .env.example .env
   composer i
   npm ci
   php artisan key:generate
   php artisan migrate
   ```
