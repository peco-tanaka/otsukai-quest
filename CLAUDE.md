# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## プロジェクト概要

**おつかいクエスト** — 買い物をモンスター討伐に見立てたRPG風ゲーミフィケーション買い物メモPWA。
スマホ前提の1画面完結アプリ。個人開発、コスト¥0が目標。

## 技術スタック

- **Next.js (App Router)** + TypeScript
- **Vercel** でホスティング
- **localStorage** でデータ永続化（認証なし、Supabaseは Phase 2）
- **PWA manifest** でホーム画面追加対応

## 開発コマンド

```bash
npm run dev       # 開発サーバー起動
npm run build     # プロダクションビルド
npm run lint      # ESLint実行
```

## アーキテクチャ

### Repository パターン

データアクセス層を抽象化し、Phase 2 でのバックエンド移行に備える。

```
コンポーネント → Repository（抽象層） → localStorage（MVP）
                                     → Supabase（Phase 2）
```

### データ設計

localStorage キー: `otsukai-quest-items`

```json
[{ "id": "UUID", "name": "牛乳", "createdAt": "ISO 8601" }]
```

### 画面構成（1画面完結）

- **上部固定**: バトルエリア（勇者 vs モンスター、1アイテム=1モンスター）
- **中央スクロール**: アイテムリスト（チェックボックス付き）
- **下部固定**: アイテム追加フォーム

## 設計方針

- モバイルファースト（iOS Safari, Android Chrome）
- デザイン: ポップ・カジュアル・RPGテイスト
- 初回表示 3秒以内
- チェックで討伐アニメーション後にリストから削除
- 全アイテム購入完了でクエストクリア状態
