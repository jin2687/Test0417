---
description: 最新のオープンAIモデル(LLM/画像/音声/マルチモーダル)を調査し、レポートとGitHub Issueを生成する週次ワークフロー
allowed-tools:
  - WebSearch
  - WebFetch
  - Read
  - Write
  - Edit
  - Glob
  - Grep
  - Bash
  - mcp__github__issue_write
  - mcp__github__issue_read
  - mcp__github__list_issues
---

# /research-all — 週次AIモデル調査ワークフロー

最新のオープンAIモデルを6カテゴリで調査し、Markdownレポートをリポジトリにコミットした上で、サマリーをGitHub Issueとして投稿する。

## 実行日と出力パス

- 今日の日付: `!date +%Y-%m-%d` を使う(変数 `TODAY` として扱う)
- 週次スナップショット: `reports/{TODAY}-{category}.md`
- 累積マスター: `reports/latest-{category}.md`
- 週次サマリー: `reports/weekly-summary/{TODAY}.md`

## 調査対象カテゴリ(6つ)

| slug | 日本語名 | 対象 |
|---|---|---|
| `llm` | LLM(テキスト生成) | チャット・推論・コード生成を含む言語モデル |
| `image-gen` | 画像生成 | T2I、I2I、ControlNet類 |
| `image-recognition` | 画像認識 | Vision基盤、OCR、検出、セグメンテーション |
| `audio-gen` | 音声生成 | TTS、音声クローン、音楽生成 |
| `audio-recognition` | 音声認識 | ASR、話者認識、音声理解 |
| `video-multimodal` | 動画・マルチモーダル | T2V、動画理解、any-to-any モデル |

## ステップ

### 1. 既知モデルリストの読み込み
各カテゴリについて `reports/latest-{category}.md` が存在すれば読む。
存在しなければ新規作成扱い。
ここで把握したモデル名を「既知リスト」としてメモリに保持する。

### 2. WebSearch による調査
各カテゴリについて、**直近7日間**を対象に以下を検索:

- `"new open source {category keywords} model {YYYY-MM}"`
- `"huggingface trending {category keywords}"`
- `"{category keywords} release {this week}"`
- カテゴリ固有の追加クエリ:
  - LLM: `"new LLM release"`, `"Qwen"`, `"Llama"`, `"Mistral"`, `"DeepSeek"`
  - 画像生成: `"FLUX"`, `"Stable Diffusion"`, `"image generation model release"`
  - 画像認識: `"vision language model"`, `"VLM release"`, `"OCR model"`
  - 音声生成: `"TTS model release"`, `"voice cloning open"`, `"music generation model"`
  - 音声認識: `"ASR model release"`, `"speech recognition open"`, `"Whisper alternative"`
  - 動画・マルチモーダル: `"text to video model"`, `"multimodal model release"`, `"any-to-any model"`

信頼性の高いソース優先:
1. Hugging Face の公式ページ
2. 公式ブログ(Meta AI、Mistral、Stability AI、Black Forest Labs、Alibaba、Tencent、DeepSeek 等)
3. GitHub のリリース
4. arXiv
5. 報道(TechCrunch、VentureBeat 等)は二次情報として扱う

### 3. 記述ルール(幻覚防止)

**厳守**:
- すべての主張に **公式ソースURL** を併記する。URLが確認できない情報は書かない
- ベンチマーク数値は**公式発表のみ**を引用。独自評価を書かない
- 「発表済みだが未公開」と「重み公開済み」を必ず区別する
- ライセンスは公式の表記をそのまま引用(Apache 2.0 / MIT / 非商用カスタム等)
- 既知リストに含まれるモデルは「更新」扱いとし、差分(新バージョン、機能追加)のみ記述

### 4. モデルごとの記述テンプレート

```markdown
### {モデル名} (v{バージョン})

- **組織**: {組織名}
- **公開日**: {YYYY-MM-DD}
- **ライセンス**: {ライセンス} {⚠️ 非商用 / ✅ 商用可 / [API-only]}
- **サイズ**: {パラメータ数} / 必要VRAM: {目安}
- **できること**:
  - {具体的ユースケース1}
  - {具体的ユースケース2}
  - {具体的ユースケース3}
- **ベンチマーク/比較**: {公式発表の数値と比較対象}
- **動かし方**: {ローカル / HFインファレンス / API など}
- **リンク**: [HF]({url}) / [GitHub]({url}) / [論文]({url}) / [公式ブログ]({url})
- **注目度**: 🔥 / ⭐ / (無印)
- **ステータス**: 🆕 新規 / 🔄 更新
```

### 5. 週次スナップショットの出力

`reports/{TODAY}-{category}.md` に書き出す:

```markdown
# {カテゴリ名} 週次レポート — {TODAY}

## サマリー
- 新規: {N}件
- 更新: {M}件
- 今週の注目: {model_name}

## 新規モデル
{モデルごとのテンプレ}

## 更新モデル
{モデルごとのテンプレ}

## 情報ソース
- {使用した主要URL一覧}
```

### 6. 累積マスターの更新

`reports/latest-{category}.md` を**追記で更新**:
- 先頭に「最終更新: {TODAY}」を置く
- 新規モデルを最新順で上に追加
- 既知モデルのエントリにバージョン更新があれば差し替え
- 古いエントリは削除せず、可読性のため年月で見出し分割

### 7. 週次サマリーの出力

`reports/weekly-summary/{TODAY}.md` に全カテゴリ横断のサマリーを書く:

```markdown
# 週次AIモデルサマリー — {TODAY}

## 全体統計
- 新規: {合計}件 / 更新: {合計}件

## 今週の注目 TOP3(カテゴリ横断)
1. [{カテゴリ}] {モデル名} — {1行要約}
2. ...
3. ...

## カテゴリ別内訳
- LLM: 新規{N}件 / 更新{M}件
- 画像生成: ...
- 画像認識: ...
- 音声生成: ...
- 音声認識: ...
- 動画・マルチモーダル: ...

## 詳細レポートへのリンク
- [LLM]({TODAY}-llm.md)
- [画像生成]({TODAY}-image-gen.md)
- ...
```

### 8. Git コミット

変更をステージしてコミット:

```bash
git add reports/
git commit -m "週次AIモデルレポート {TODAY}

新規: {合計N}件 / 更新: {合計M}件
カテゴリ: LLM({n}), 画像生成({n}), 画像認識({n}), 音声生成({n}), 音声認識({n}), 動画・マルチモーダル({n})"
```

`git push -u origin claude/ai-model-tracking-workflow-IIa4q` で push。

### 9. 前週 Issue のクローズ

`mcp__github__list_issues` でラベル `weekly-ai-report` のオープンIssueを取得し、
今回作成する新Issue以外はクローズ(`mcp__github__issue_write` の `update` アクション)。

### 10. GitHub Issue の作成

`mcp__github__issue_write` で新規作成:

- **タイトル**: `📊 週次AIモデルレポート {TODAY}`
- **ラベル**: `weekly-ai-report`
- **本文**:

```markdown
## 📊 週次AIモデルレポート ({TODAY})

### 今週の概要
- 🆕 新規モデル: **{合計N}件**
- 🔄 更新: **{合計M}件**

### 🔥 今週の注目 TOP3
1. **[{カテゴリ}] {モデル名}** — {1-2行の説明}
   - ライセンス: {ライセンス}
   - [詳細]({HF/GitHub URL})
2. ...
3. ...

### 📂 カテゴリ別内訳
| カテゴリ | 新規 | 更新 |
|---|---|---|
| LLM | {n} | {m} |
| 画像生成 | {n} | {m} |
| 画像認識 | {n} | {m} |
| 音声生成 | {n} | {m} |
| 音声認識 | {n} | {m} |
| 動画・マルチモーダル | {n} | {m} |

### 📁 詳細レポート
- [週次サマリー](../blob/claude/ai-model-tracking-workflow-IIa4q/reports/weekly-summary/{TODAY}.md)
- [LLM](../blob/claude/ai-model-tracking-workflow-IIa4q/reports/{TODAY}-llm.md)
- [画像生成](../blob/claude/ai-model-tracking-workflow-IIa4q/reports/{TODAY}-image-gen.md)
- [画像認識](../blob/claude/ai-model-tracking-workflow-IIa4q/reports/{TODAY}-image-recognition.md)
- [音声生成](../blob/claude/ai-model-tracking-workflow-IIa4q/reports/{TODAY}-audio-gen.md)
- [音声認識](../blob/claude/ai-model-tracking-workflow-IIa4q/reports/{TODAY}-audio-recognition.md)
- [動画・マルチモーダル](../blob/claude/ai-model-tracking-workflow-IIa4q/reports/{TODAY}-video-multimodal.md)

---
*このレポートは `/research-all` コマンドで自動生成されています。*
```

## エラー時の挙動

- いずれかのカテゴリでWebSearchが失敗 → そのカテゴリのみスキップ、Issue本文に「⚠️ {カテゴリ}は取得失敗」を追記
- git push 失敗 → ネットワークエラーなら最大4回リトライ(2s→4s→8s→16s)。それでも失敗ならIssueに「push失敗、手動確認要」と追記
- Issue作成失敗 → Markdownファイルはコミット済みなので致命的ではない。ログに残して終了

## 注意

- **商用不可ライセンスのモデル**: 除外せず、`⚠️ 非商用` ラベルで明記して含める
- **API専用モデル**: Claude、GPT、Gemini 等の超注目モデルは `[API-only]` ラベルで含める。それ以外は重み公開モデルを優先
- **言語**: 日本語ベース。モデル名・ベンチ名・ライセンス名は英語のまま
