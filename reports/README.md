# AI モデル調査レポート

`/research-all` コマンドによって自動生成される、最新オープンAIモデルの週次調査レポート。

## ディレクトリ構成

```
reports/
├── README.md                        # このファイル
├── latest-llm.md                    # LLM の累積マスター(最新順)
├── latest-image-gen.md              # 画像生成の累積マスター
├── latest-image-recognition.md      # 画像認識の累積マスター
├── latest-audio-gen.md              # 音声生成の累積マスター
├── latest-audio-recognition.md      # 音声認識の累積マスター
├── latest-video-multimodal.md       # 動画・マルチモーダルの累積マスター
│
├── YYYY-MM-DD-{category}.md         # 週次スナップショット(カテゴリ別)
│
└── weekly-summary/
    └── YYYY-MM-DD.md                # 週次サマリー(カテゴリ横断)
```

## ファイルの使い分け

| ファイル | 目的 | 更新タイミング |
|---|---|---|
| `latest-{category}.md` | そのカテゴリの「現時点の全体像」 | 毎週の実行で追記・更新 |
| `{TODAY}-{category}.md` | その週に見つかった差分スナップショット | 毎週新規作成 |
| `weekly-summary/{TODAY}.md` | カテゴリ横断の注目ダイジェスト | 毎週新規作成 |

## カテゴリ一覧

| slug | 日本語名 |
|---|---|
| `llm` | LLM(テキスト生成) |
| `image-gen` | 画像生成 |
| `image-recognition` | 画像認識 |
| `audio-gen` | 音声生成 |
| `audio-recognition` | 音声認識 |
| `video-multimodal` | 動画・マルチモーダル |

## 手動実行

Claude Code のセッション内で:

```
/research-all
```

## 定期実行

`docs/scheduled-task-setup.md` を参照。
