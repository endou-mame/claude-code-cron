# Claude Code Cron Trigger

既存のClaude Code Actionを深夜帯に自動実行するための軽量トリガーシステムです。

## 概要

指定したラベルが付いたGitHub issueに`@claude`メンションを自動的に追加することで、既存のClaude Code Actionをトリガーします。

## 特徴

- 🌙 日本時間の深夜帯（1時〜5時）に自動実行
- 🏷️ 特定のラベルが付いたissueのみを処理
- 🔄 重複処理を防ぐラベル管理
- 📦 単一ファイルで完結（追加の依存関係なし）
- ⚡ セットアップは1ファイルのコピーのみ

## セットアップ

### 前提条件

- リポジトリに既存のClaude Code Action (`claude.yml`) が設定されていること
- `ANTHROPIC_API_KEY`がGitHub Secretsに設定されていること

### インストール

1. `.github/workflows/claude-code-cron.yml`をあなたのリポジトリの同じパスにコピー

以上！これだけで動作します。

### 設定（オプション）

Repository variablesで以下を設定できます：

- `CLAUDE_PROCESS_LABELS`: 処理対象のラベル（デフォルト: `claude-code`）
- `CLAUDE_MAX_ISSUES`: 一度に処理する最大issue数（デフォルト: `5`）

## 動作の仕組み

1. 指定されたラベルが付いたopen状態のissueを検出
2. 既に`claude-processed`ラベルが付いているissueはスキップ
3. 各issueに`@claude`メンションを含むコメントを追加
4. `claude-processing`ラベルを追加して処理中であることを示す
5. 既存のClaude Code Actionが起動し、コード修正とPR作成を実行

## 実行タイミング

以下の時間に自動実行されます（日本時間）：
- 01:23
- 02:47
- 03:11
- 04:31

手動実行も可能：GitHub Actionsの画面から「Run workflow」をクリック

## ラベルの意味

- `claude-code`: 処理対象のissue（設定で変更可能）
- `claude-processing`: 現在処理中
- `claude-processed`: 処理済み（Claude Code Actionで追加されることを想定）

## ライセンス

MIT