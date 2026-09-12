# Youhei Suzuki — AI-Assisted Development Portfolio

> 個人開発の成果物を、AI コーディングエージェント（主に Claude Code）を活用した開発プロセスとあわせて紹介する採用向けポートフォリオです。
> ソースコードの配布が目的ではないため、各プロジェクトは概要・構成図・工夫した点を中心にまとめています。

## 1. 概要

本業のかたわら、動画の自動生成 bot、家庭向けの学習アプリ、実店舗で使う業務アプリなどを個人で開発・運用しています。
開発では Claude Code を「開発エージェント」として使い、調査・設計検討・実装・デバッグを任せる一方で、何を作るか、どの案を採用するか、実環境で正しく動いているかの判断は自分で行っています。

このリポジトリは、その成果物と進め方を採用担当者・エンジニアの方が 5 分程度で把握できることを目標にしています。
元のリポジトリはすべて Private のままで、ここには秘密情報・個人情報・実運用データを含まない説明資料だけを新規に作成しています。

## 2. プロジェクト一覧

| プロジェクト | 一言説明 | 主な技術 | 状態 | 詳細 |
|---|---|---|---|---|
| YouTube Shorts Automation | テーマ選定から台本生成・検証・レンダリングまでを毎日自動で行う縦動画生成パイプライン | Remotion / React / TypeScript / Python / Claude API | 運用中（投稿は手動） | [詳細](projects/youtube-shorts-automation/README.md) |
| Instagram Reel Bots | 5 アカウント分のリール動画を共通アーキテクチャで毎日生成する bot 群 | Python / FFmpeg / Claude API | 運用中（投稿は手動） | [詳細](projects/instagram-reel-bots/README.md) |
| AI Home Tutor | 小学生向けのブラウザ家庭教師アプリ（英語が主教科、算数は補助） | Python / FastAPI / Claude API | 運用中（家族向け） | [詳細](projects/ai-home-tutor/README.md) |
| Grooming Salon Manager | 家族が営む実店舗のトリミングサロンで使う顧客・予約・カルテ・売上管理 PWA | React / TypeScript / Firebase | 運用中（実店舗で日常利用） | [詳細](projects/grooming-salon-manager/README.md) |

## 3. 開発スタイル — AI エージェントとの協働

AI エージェントに任せている部分と、自分で担当・判断している部分を分けて運用しています。

| AI エージェント（Claude Code）に任せている部分 | 自分が担当・判断している部分 |
|---|---|
| 技術調査、実現方法の検討、設計検討 | 何を作るか、どの機能が必要か、仕様 |
| 既存コードの解析、コード生成、複数ファイルにまたがる実装 | AI への指示（依頼文の作成、制約と停止条件の指定） |
| 修正、エラー原因の調査、デバッグ、リファクタリング | 生成結果の確認、問題の原因の切り分け、修正方針の採用 |
| テストコードの作成、ドキュメント整備 | 実環境での動作確認、最終的な採用判断、継続改善 |

「AI が全部作った」わけでも「すべて手書きした」わけでもなく、AI に実装を委ねつつ、判断と検証を自分が持つ形で進めています。
各プロジェクトには CLAUDE.md（プロジェクト固有の構成・設計判断・運用ルール）と作業記録（計画・教訓）を置き、毎回ゼロから指示するのではなく、ルールを積み上げながら開発しています。

詳細: [docs/ai-development-workflow.md](docs/ai-development-workflow.md)

## 4. 共通の開発フロー

```mermaid
flowchart LR
    A[課題・改善テーマ] --> B[要件整理・依頼文の作成]
    B --> C[Claude Code へ指示]
    C --> D[調査・計画の提示]
    D --> E{計画を確認}
    E -- 修正 --> B
    E -- 承認 --> F[実装]
    F --> G[確認・テスト]
    G --> H{問題あり?}
    H -- はい --> I[原因の切り分け・修正方針の決定]
    I --> F
    H -- いいえ --> J[実環境で動作確認]
    J --> K[Git へ記録]
    K --> L[教訓の記録・継続改善]
    L --> A
```

## 5. 技術スタック（全体）

4 プロジェクトで実際に使っている技術をまとめています。

| 分類 | 技術 |
|---|---|
| 言語 | Python、TypeScript |
| フロントエンド | React、Vite、Tailwind CSS、react-router、HTML / CSS / JavaScript（フレームワーク不使用の画面もあり）、Chart.js |
| 動画・画像・音声処理 | Remotion、FFmpeg、Pillow、budoux（日本語分かち書き）、VOICEVOX、Google Cloud Text-to-Speech、Web Speech API |
| バックエンド・データ | FastAPI、uvicorn、SQLite、Firebase（Authentication、Cloud Firestore）、YAML / JSON による設定・履歴管理 |
| AI・外部 API | Claude API（Anthropic）、Pexels API、YouTube Analytics API、Google Calendar API、Google Drive API、Google Identity Services（OAuth） |
| PWA・運用 | vite-plugin-pwa、launchd（macOS）、シェルスクリプト |
| 通知 | Slack API / Webhook、Telegram Bot API |
| テスト・品質 | unittest、pytest、TypeScript の型チェック、npm audit、読み取り専用エージェントによる監査 |
| 開発ツール | Git / GitHub、Claude Code |

## 6. セキュリティ・プライバシーへの配慮

- 認証情報は `.env` などリポジトリ管理外のファイルに置き、`.gitignore` で除外しています。
- 開発中の元リポジトリは Private のまま維持し、このポートフォリオは Git 履歴を引き継がない新規リポジトリとして作成しています。
- 公開前にキーワード検索・ファイル種別・画像の目視でチェックし、個人情報・実運用データ・秘密情報を含めていません。

詳細: [docs/security-and-privacy.md](docs/security-and-privacy.md)

## 7. このポートフォリオで伝えたいこと

- **AI コーディングエージェントを日常の開発で使いこなしていること**: 4 プロジェクトすべてを Claude Code と開発し、CLAUDE.md・依頼文・教訓・仕様変更ログでルールを積み上げながら、数か月にわたって改善を続けています
- **AI の出力を検証してから使う姿勢**: 動画の台本には多段の検査、学習アプリには採点と検算のアプリ側実装、業務アプリには多観点の監査と実機確認を入れ、「生成されたから採用」にはしていません
- **動くものを作り、運用し続けていること**: 動画 bot は毎朝の定時実行、学習アプリは家庭で、業務アプリは実店舗で日常的に使われています
- **失敗を仕組みに変えていること**: 障害や設計ミスを「何が起きたか・根本原因・再発防止ルール」の形で記録し、fail-open / fail-close の使い分けや金額のスナップショット原則のような判断基準に一般化しています
- **安全に配慮した開発・公開**: 秘密情報と個人データを扱う前提で、環境ファイルの分離、最小権限、Private と Public の分離、公開前の監査を習慣にしています

## 8. 業務での取り組み

本業では製造業の社内SEとして、レガシーWebシステムの移行、コーポレートサイトの再構築、検査・帳票業務の自動化などを担当しています。詳細は職務経歴書でご説明します。

## English Summary

This repository is a recruiting portfolio that presents my personal projects together with how I build them with AI coding agents, mainly Claude Code.
The four projects are a daily YouTube Shorts generation pipeline (Remotion / Python / Claude API), a set of Instagram Reel bots for five accounts sharing one architecture (Python / FFmpeg), a browser-based home tutor app for elementary school students with English as the main subject (FastAPI / Claude API), and a PWA for customers, bookings, and records used daily in a real grooming salon (React / Firebase).
I delegate research, design exploration, implementation, and debugging to the agent, while I own the requirements, the instructions, verification in the real environment, and the final decisions.
Each project keeps its own CLAUDE.md plus records of plans and lessons, so the agent works under accumulated project rules rather than ad-hoc prompts, and generated output is checked by tests, audits, or server-side validation before it is adopted.
Three of the projects run in daily use: scheduled generation on macOS, a family tutor app at home, and a business app in a salon.
The original repositories remain private; this repository contains only newly written documentation with no secrets, personal data, or production data.

---

本リポジトリの文章・図・画像の無断転載はご遠慮ください。All rights reserved.
