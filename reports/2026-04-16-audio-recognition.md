# 音声認識 週次レポート — 2026-04-16

## サマリー
- 新規: 3件(Cohere Transcribe, Parakeet-unified-en, Nemotron 3 VoiceChat)
- 更新: 0件
- 今週の注目: **Cohere Transcribe** — 2B で Open ASR Leaderboard #1、Whisper Large v3 / ElevenLabs Scribe v2 / Qwen3-ASR-1.7B を上回る

## 新規モデル

### Cohere Transcribe

- **組織**: Cohere
- **公開日**: 2026-03-31
- **ライセンス**: Apache 2.0 ✅ 商用可
- **サイズ**: 2B / Conformer ベース(90%以上のパラメータがエンコーダ)/ Consumer GPU で動作
- **できること**:
  - 英語主体の高精度 ASR(14 言語対応: 欧州・AIPAC・MENA)
  - 会議議事録、スピーチ分析、リアルタイム顧客サポート
  - オンプレ導入(フル制御可)または Cohere Model Vault 経由でマネージド実行
- **ベンチマーク/比較**: Open ASR Leaderboard #1、WER 平均 5.42 %(Whisper Large v3 / ElevenLabs Scribe v2 / Qwen3-ASR-1.7B を超過、公式発表)
- **動かし方**: ローカル / HF / Cohere Model Vault
- **リンク**: [公式ブログ](https://cohere.com/blog/transcribe) / [HF 発表](https://huggingface.co/blog/CohereLabs/cohere-transcribe-03-2026-release) / [TechCrunch](https://techcrunch.com/2026/03/26/cohere-launches-an-open-source-voice-model-specifically-for-transcription/)
- **注目度**: 🔥
- **ステータス**: 🆕 新規

### NVIDIA Parakeet-unified-en-0.6b

- **組織**: NVIDIA
- **公開日**: 2026年4月(具体日は公式未明記)
- **ライセンス**: NVIDIA オープンライセンス(要確認)
- **サイズ**: 600M / Consumer GPU で動作
- **できること**:
  - 英語の高品質オフラインおよびストリーミング ASR を単一モデルで実現
  - 句読点・大文字小文字復元を内蔵
  - リアルタイム・大量バッチの両方に対応
- **ベンチマーク/比較**: HF マルチリンガル ASR リーダーボードで高スループット実績(Parakeet-tdt-0.6b-v3 系統)
- **動かし方**: HF / NeMo Framework
- **リンク**: [NVIDIA Technical Blog (Canary/Parakeet 関連)](https://developer.nvidia.com/blog/nvidia-speech-and-translation-ai-models-set-records-for-speed-and-accuracy/) / [HF: nvidia/parakeet-tdt-0.6b-v2](https://huggingface.co/nvidia/parakeet-tdt-0.6b-v2)
- **注目度**: ⭐
- **ステータス**: 🆕 新規

### NVIDIA Nemotron 3 VoiceChat (Early Access)

- **組織**: NVIDIA
- **公開日**: 2026-03(Early Access)
- **ライセンス**: 要確認(Early Access)
- **サイズ**: Nemotron Nano v2 LLM バックボーン + speech / TTS デコーダ
- **できること**:
  - 全二重(full-duplex)の自然な音声対話
  - 割り込み可能な低レイテンシ応答
  - 音声理解 + 生成の統合
- **ベンチマーク/比較**: 公式ブログで「低レイテンシで自然な割り込み対応」を主張
- **動かし方**: NVIDIA Early Access 登録
- **リンク**: [NVIDIA Blog: Speech AI Dataset/Models](https://blogs.nvidia.com/blog/speech-ai-dataset-models/)
- **注目度**: ⭐
- **ステータス**: 🆕 新規(EA)

## 継続参照

### IBM Granite Speech 3.3 8B

- Hugging Face Open ASR Leaderboard 上位(Cohere Transcribe に先立ちトップ実績)
- リンク: [IBM Research blog](https://research.ibm.com/blog/granite-speech-recognition-hugging-face-chart)

### Meta Omnilingual ASR

- 1,600 言語対応のマルチリンガル ASR 研究発表
- リンク: [Meta AI](https://ai.meta.com/research/publications/omnilingual-asr-open-source-multilingual-speech-recognition-for-1600-languages/)

### OLMoASR (Ai2)

- オープン音声認識モデルシリーズ
- リンク: [Ai2 Blog](https://allenai.org/blog/olmoasr)

## 情報ソース

- [Cohere Transcribe blog](https://cohere.com/blog/transcribe)
- [HF: Cohere Transcribe release](https://huggingface.co/blog/CohereLabs/cohere-transcribe-03-2026-release)
- [TechCrunch: Cohere voice model](https://techcrunch.com/2026/03/26/cohere-launches-an-open-source-voice-model-specifically-for-transcription/)
- [NVIDIA Developer Blog](https://developer.nvidia.com/blog/nvidia-speech-and-translation-ai-models-set-records-for-speed-and-accuracy/)
- [NVIDIA Blogs: Speech AI](https://blogs.nvidia.com/blog/speech-ai-dataset-models/)
- [Open ASR Leaderboard (HF)](https://huggingface.co/spaces/hf-audio/open_asr_leaderboard)
- [Northflank: Best open source STT 2026](https://northflank.com/blog/best-open-source-speech-to-text-stt-model-in-2026-benchmarks)
- [Gladia: Best open-source STT 2026](https://www.gladia.io/blog/best-open-source-speech-to-text-models)
