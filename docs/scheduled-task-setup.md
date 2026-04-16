# Scheduled Task セットアップガイド

`/research-all` コマンドを定期実行して、継続的に最新AIモデル情報を収集・報告するためのセットアップ手順。

## 前提

- 本リポジトリが claude.ai/code に接続済みであること
- ブランチ `claude/ai-model-tracking-workflow-IIa4q` にコマンド定義がコミット済みであること
- GitHub MCP サーバー経由でIssue作成権限があること

## 手順

### 1. claude.ai/code でリポジトリを開く

https://claude.ai/code にアクセスし、本リポジトリ (`jin2687/test0417`) を選択。

### 2. Scheduled Task を作成

リポジトリ画面の **Schedule** メニュー(または同等のUI)から新規スケジュールを作成:

| 項目 | 値 |
|---|---|
| **名前** | `weekly-ai-model-research` |
| **ブランチ** | `claude/ai-model-tracking-workflow-IIa4q` |
| **実行タイミング** | 毎週 月曜 09:00 JST(= 00:00 UTC) |
| **起動プロンプト** | `/research-all` |

### 3. 動作確認(手動トリガー)

初回は **Run now** でその場実行し、以下を確認:

- [ ] `reports/{TODAY}-llm.md` 等の週次スナップショットが作成された
- [ ] `reports/latest-{category}.md` 累積マスターが作成/更新された
- [ ] `reports/weekly-summary/{TODAY}.md` が作成された
- [ ] ブランチに自動コミットされた
- [ ] GitHub Issue(タイトル `📊 週次AIモデルレポート {TODAY}`)が作成された

### 4. 通知の受け取り方

GitHub Issue 経由で通知を受け取るために:

1. リポジトリの **Watch** 設定で `Custom > Issues` を有効化
2. GitHub の通知設定でメール or Web通知を有効に
3. モバイルなら GitHub アプリを入れておく

これで週次Issueの作成時に自動通知が届く。

### 5. 前週Issueの扱い

- `/research-all` は実行時に **ラベル `weekly-ai-report` のオープンIssueを自動クローズ**する
- 過去の履歴はクローズ済みIssueとしてGitHubに残り続ける
- 履歴を見たい場合は Issues 画面で `label:weekly-ai-report is:closed` で絞り込み

## 将来の拡張

### Slack 通知の追加

Slack Incoming Webhook を使う場合:

1. https://api.slack.com/apps で App を作成
2. Incoming Webhooks を有効化 → 通知先チャンネル選択 → Webhook URL 取得
3. claude.ai/code のリポジトリ設定で環境変数 `SLACK_WEBHOOK_URL` を登録
4. `.claude/commands/research-all.md` の末尾にSlack通知ステップを追加

### カテゴリ別コマンドの追加

全カテゴリ一括ではなく個別に叩きたい場合、
`.claude/commands/research-{category}.md` を作成し、該当カテゴリのみを実行する形に分割できる。

### 頻度変更

週次が多すぎる/少なすぎる場合はスケジュール設定で調整:

- 隔週: 毎月 第1・第3月曜
- 日次: 毎日 09:00(ただし新規が少ない日はIssue本文がスカスカになる)
- 月次: 毎月 第1月曜

## トラブルシューティング

| 症状 | 対処 |
|---|---|
| Scheduled Task が実行されない | claude.ai/code 側のスケジュール設定と、対象ブランチが正しいか確認 |
| WebSearch が失敗する | 一時的な障害の可能性。翌週に自動的に再試行される。急ぎなら手動 `/research-all` を実行 |
| Issue が作成されない | GitHub MCP 権限を確認。コミット自体は成功している可能性が高いので `reports/` を直接確認 |
| 内容の質が低い | `.claude/commands/research-all.md` の検索クエリやソース優先順位を調整 |
