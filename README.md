# Go 1.24 Development Container

Go 1.24開発用のDocker開発コンテナ設定です。Debian Bookwormベースで、fishシェルを標準搭載しています。

## 概要

このリポジトリは、Go 1.24.3開発環境をDockerコンテナとして提供します。VS Code Remote Containerと組み合わせて使用することで、一貫した開発環境を簡単に構築できます。

## 特徴

- **ベースイメージ**: `ghcr.io/bearfield/debian-fish:bookworm`
- **Goバージョン**: 1.24.3
- **対応アーキテクチャ**: ARM64, AMD64
- **デフォルトシェル**: fish
- **開発ツール**: gcc, g++, libc6-dev, pkg-config

## 利用方法

### VS Code Dev Containerとして使用

1. このリポジトリをクローン
2. VS Codeで開く
3. "Reopen in Container"を選択

### スタンドアロンDockerイメージとして使用

```bash
docker pull ghcr.io/kumanoryo/golang:1.24
```

## ビルドとテスト

### ローカルビルド

```bash
# ARM64版のビルドとテスト
make test.arm64

# AMD64版のビルドとテスト  
make test.amd64

# 両アーキテクチャのビルドとテスト
make test
```

### ビルドコマンド詳細

- `make test.build.arm64` - ARM64版イメージのビルド
- `make test.build.amd64` - AMD64版イメージのビルド
- `make test.rmi.arm64` - ARM64版イメージの削除
- `make test.rmi.amd64` - AMD64版イメージの削除

## 自動ビルドとリリース

GitHub Actionsにより、以下のタイミングで自動ビルドとリリースが実行されます：

- mainブランチへのプッシュ時（docker/配下またはワークフローファイルの変更時）
- 毎日午前4時（JST）の定期ビルド

### 公開イメージ

- `ghcr.io/kumanoryo/golang:1.24` - マルチプラットフォーム対応
- `ghcr.io/kumanoryo/golang:1.24-arm64` - ARM64専用
- `ghcr.io/kumanoryo/golang:1.24-amd64` - AMD64専用

## 環境設定

### コンテナ内の設定

- **GOPATH**: `/go`
- **作業ディレクトリ**: `/go`
- **ユーザー**: カスタマイズ可能（デフォルト: devuser）

### カスタマイズ

GitHub リポジトリの変数で以下をカスタマイズできます：

- `CONTAINER_USER_NAME`: コンテナ内のユーザー名（デフォルト: devuser）

## 必要な設定

### GitHub Secrets

- `CR_PAT`: GitHub Container Registryへのプッシュ権限を持つPersonal Access Token

## ライセンス

このプロジェクトのライセンスについては、LICENSEファイルを参照してください。
