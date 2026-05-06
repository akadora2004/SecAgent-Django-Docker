# SecAgent-Django-Docker

LLM（Gemini API）を活用した自律型フィッシング分析エージェント「[SecAgent-Django](https://github.com/akadora2004/SecAgent-Django)」を、セキュリティの観点からコンテナ化したプロジェクトです。

## 📋 概要

本プロジェクトは、Webアプリケーション（Django）の実行環境をホストOSから適切に隔離し、安全に運用・開発することを目的に構築されました。

## 🛡️ セキュリティ・ベストプラクティスの実践

Snykの『[10 Docker Image Security Best Practices](https://snyk.io/jp/blog/10-docker-image-security-best-practices/)』を参考に、以下の3点を重点的に実装しています。

### ベースイメージの最小化 (Best Practice 1)
- `python:3.12-slim` を利用し、攻撃表面（アタックサーフェス）を最小限に抑えています。

### 最小特権ユーザーでの実行 (Best Practice 2)
- コンテナ内プロセスを root ではなく一般ユーザー（django-user）で実行し、万が一の侵害時の影響範囲を限定しています。

### マルチステージビルドの活用 (Best Practice 9)
- ビルド時のみ必要なツールを最終イメージから排除し、イメージの軽量化と安全性を両立しています。

## 📂 ディレクトリ構成

Docker設定ファイルとソースコードを分離して管理しています。

```
.
├── django/             # Dockerイメージ定義（Dockerfile, requirements.txt）
├── src/                # Djangoプロジェクト本体（manage.py, config/ 等）
├── .dockerignore       # イメージへの機密情報混入防止
├── .env                # 環境変数（APIキー等。Git管理除外対象）
├── .gitignore          # Git管理除外設定
└── docker-compose.yaml # コンテナオーケストレーション定義
```

## 🚀 セットアップ

### 1. 環境変数の設定
プロジェクトルートに `.env` ファイルを作成し、Gemini APIキーを記述してください。

```env
GOOGLE_API_KEY=ここにあなたのAPIキーをかく
```

### 2. コンテナの起動

```bash
docker compose up -d --build
```

## 🛠 使用技術

- **Framework**: Django (Python)
- **AI SDK**: google-genai
- **Infrastructure**: Docker / Docker Compose
