# 開発環境構築方法

## 前提条件

- Docker、Docker Compose がインストールされていること
- VS Code がインストールされていること、下記の拡張機能がインストールされていること
  - Remote Development

## 手順

1. リポジトリのクローン

```bash
git clone https://github.com/haruki26/php-advanced-class.git
```

2. Dev Container の起動

```bash
code php-advanced-class
```

-  `Ctrl + Shift + P` を押して、`Dev Containers: Reopen in Container` を選択する
  - Mac の場合は `Command + Shift + P`

> [!Note]
> 初回起動時は、Docker イメージのビルドに時間がかかる場合があります。

> [!Caution]
> **Dev Container のビルドに失敗する場合**
>
> Docker Buildx と Dev Containers の組み合わせによっては、起動時にファイルシステムのアクセス権限に関するエラーが発生する場合があります。
>
> ```text
> additional privileges requested: pass "--allow=fs.read=..." to grant requested privileges
> ```
>
> この場合は、以下のコマンドで VS Code を起動し、再度 `Dev Containers: Reopen in Container` を実行してください。
>
> ```bash
> BUILDX_BAKE_ENTITLEMENTS_FS=0 code php-advanced-class
> ```
>
> この環境変数は Buildx のファイルシステムアクセス制限を緩和するため、問題が解消されるまでの一時的な回避策として使用してください。
>
> 参考: [VS Code GitHub Issue #11896](https://github.com/microsoft/vscode-remote-release/issues/11896) 

---

以下からは、Dev Container 内での作業となります。

3. .env ファイルの作成

```bash
cp .env.example .env
php artisan key:generate
```

4. データベースのマイグレーション

```bash
php artisan migrate
```
