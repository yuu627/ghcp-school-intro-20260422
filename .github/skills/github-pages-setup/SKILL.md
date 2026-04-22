---
name: github-pages-setup
description: 'GitHub Pages サイトを構築・公開する手順を実行する Skill です。Use when: GitHub Pages 初回公開、Actions デプロイ設定、カスタムドメイン設定、公開トラブルの切り分け。'
argument-hint: 'サイト種別（静的/ビルド要）、公開元（branch/actions）、カスタムドメイン有無を指定してください。'
---

# GitHub Pages Setup

GitHub Pages の公式ドキュメントに沿って、最短で安全に公開するためのワークフローです。

## When to Use
- 新規リポジトリを GitHub Pages で公開したいとき
- 既存サイトを Branch 公開から Actions 公開へ移行したいとき
- カスタムドメインと HTTPS を設定したいとき
- 公開されない、更新が反映されない等の問題を切り分けたいとき

## Inputs
- リポジトリ名と既定ブランチ
- サイトの生成方法: `静的ファイルのみ` / `ビルドが必要`
- 公開方式: `Deploy from a branch` / `GitHub Actions`
- カスタムドメインの要否

## Procedure
1. 方式を決定する
- `静的ファイルのみ` かつシンプル公開なら Branch 公開を優先
- Astro などビルドが必要なら Actions 公開を優先

2. リポジトリの前提を確認する
- 公開するファイル配置を確認（例: ルート, `docs/`, ビルド出力）
- Pages 設定画面で公開元に選ぶ対象ブランチ/フォルダが存在することを確認

3. 公開方式ごとに設定する
- Branch 公開:
  1. Pages 設定で公開元ブランチとフォルダを選択
  2. 公開対象ファイルを push
- Actions 公開:
  1. Pages 用ワークフローを追加
  2. ビルド成果物を Pages artifact として deploy
  3. 権限（`pages`, `id-token`）とブランチ条件を確認

4. カスタムドメインを設定する（必要時のみ）
- DNS レコードを設定
- Pages 設定でカスタムドメインを登録
- HTTPS 強制が有効化される状態を確認

5. 公開確認と疎通確認を行う
- `https://<user>.github.io/<repo>/` または独自ドメインへアクセス
- 404 の場合はパス基準（特に SPA のルーティング）と公開フォルダを再確認
- キャッシュ影響を除外して再確認

## Decision Points
- Branch と Actions のどちらを選ぶか
- プロジェクトサイト（`/<repo>/`）かユーザー/組織サイト（`/`）か
- カスタムドメインを使うか
- SPA で 404 フォールバック対策が必要か

## Completion Checks
- Pages のデプロイが `success` で完了している
- 想定 URL でトップページと主要導線が表示される
- 更新コミットが数分以内に反映される
- カスタムドメイン使用時に HTTPS が有効

## Official References
- About GitHub Pages:
  https://docs.github.com/ja/pages/getting-started-with-github-pages/about-github-pages
- Creating a GitHub Pages site:
  https://docs.github.com/ja/pages/getting-started-with-github-pages/creating-a-github-pages-site
- Using custom workflows with GitHub Pages:
  https://docs.github.com/ja/pages/getting-started-with-github-pages/using-custom-workflows-with-github-pages
- Configuring a custom domain:
  https://docs.github.com/ja/pages/configuring-a-custom-domain-for-your-github-pages-site
- Setting up with Jekyll:
  https://docs.github.com/ja/pages/setting-up-a-github-pages-site-with-jekyll
