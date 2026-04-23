# AI Company OS — Claude Code AI会社運営フレームワーク

## 概要

Claude Codeを使ってAI会社を立ち上げ・運営するためのフレームワーク。
AIエージェントが実業務を担い、オーナー（人間）はエスカレーション時のみ判断する組織構造を定義する。

---

## AI組織構造

```
オーナー（人間）
    │ 指示 / エスカレーション時のみ
    ▼
CEO AIエージェント  ← 全体統括・委任・ファイナルチェック
    │                       ↑ 週次レポート
    │               経営管理部（財務・キャパ・攻守）
    ▼
統括マネージャー  ← 部門指示・品質チェック・差し戻し
    │
    ├── [AI情報・企画部]  — AIトレンド収集・新サービス設計（月2回）
    ├── [マーケティング部] — コンテンツ・インバウンド集客（週1回）
    ├── 営業部            — アウトバウンドメール・商談（毎日）
    ├── リサーチ部         — 候補社調査・スコアリング（必要時）
    ├── 資料制作部         — 提案書・テンプレート・教材（必要時）
    └── ナレッジ管理部     — 知識蓄積・ドキュメント管理（週1回）
```

---

## 品質チェックフロー

```
部門 → 統括マネージャー（1次チェック）
  不合格 → 部門へ差し戻し（最大2回）
  合格 → CEO AIへ承認報告

CEO AI（ファイナルチェック）
  不合格 → 統括マネージャーへ差し戻し（最大2回）
  合格 → オーナーへ完了報告
```

---

## セットアップ

### 1. グローバルエージェントを配置する

```bash
cp global/bizorg-ceo.md ~/.claude/agents/
cp global/bizorg-manager.md ~/.claude/agents/
cp global/bizorg-finance.md ~/.claude/agents/
cp global/bizorg-ai-strategy.md ~/.claude/agents/
cp global/bizorg-marketing.md ~/.claude/agents/
```

### 2. プロジェクトリポジトリに適用する

各プロジェクトリポジトリの `org/agents/` に `templates/` からコピー＆カスタマイズ。

```bash
cp templates/sales-agent.md /path/to/project/org/agents/sales-agent.md
# [プロジェクト固有の情報] を置き換える
```

### 3. 運用開始

Claude Codeで「[bizorg-ceo]このプロジェクトのXXをやってください」と指示を出す。

---

## リポジトリ構造

```
├── README.md                   # このファイル
├── org/                        # コアエージェント定義
│   ├── structure.md            # 組織全体図・フロー
│   ├── org-chart.md            # 組織図（詳細版）
│   └── agents/
│       ├── ceo-ai.md           # CEO AIエージェント
│       ├── general-manager.md  # 統括マネージャー
│       ├── bizops-agent.md     # 経営管理部
│       ├── ai-strategy-agent.md
│       └── marketing-agent.md
├── global/                     # ~/.claude/agents/にコピーするファイル
│   ├── bizorg-ceo.md
│   ├── bizorg-manager.md
│   ├── bizorg-finance.md
│   ├── bizorg-ai-strategy.md
│   └── bizorg-marketing.md
└── templates/                  # プロジェクト固有部門のテンプレート
    ├── sales-agent.md
    ├── research-agent.md
    ├── knowledge-agent.md
    ├── materials-agent.md
    ├── ai-strategy-agent.md
    └── marketing-agent.md
```

---

## エスカレーション条件（オーナー判断が必要）

- 月額10万円超の発注・契約・課金
- 実在する顧客への初回コンタクト実行
- 新しいサービス価格・プランの正式決定
- 本番データの書き込み・削除
- 新規事業の立ち上げ・撤退判断
- 成果物が2回差し戻し後も改善されない

---

## 適用プロジェクト例

| プロジェクト | リポジトリ | 適用部門 |
|---|---|---|
| 葬儀社向け追悼動画支援 | funeral-sales-support | 営業部・リサーチ部・ナレッジ管理部・資料制作部 |
