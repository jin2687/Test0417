# 画像認識 週次レポート — 2026-04-16

## サマリー
- 新規: 3件(Nanonets-OCR-3, InternVL-U, GLM-OCR)
- 更新: 1件(Qwen3-VL 軽量版)
- 今週の注目: **GLM-OCR** (Zhipu AI) — 0.9B で Qwen3-VL-235B 超の OCR 性能、VRAM 4GB で動作

## 新規モデル

### Nanonets-OCR-3

- **組織**: Nanonets
- **公開日**: 2026-04-09
- **ライセンス**: クローズド [API-only]
- **サイズ**: 35B MoE / 必要VRAM: 60GB+(自社ホスト想定)
- **できること**:
  - 文書 OCR + レイアウト理解
  - バウンディングボックス + 信頼度スコア付与
  - ネイティブ VQA(文書質問応答)
  - エージェントスタックとの統合前提
- **ベンチマーク/比較**: グローバル OCR ベンチで #1(公式発表、OCR-2 比 約2倍高速)
- **動かし方**: API / 独自 SDK
- **リンク**: [公式発表](https://nanonets.com/research/nanonets-ocr-3) / [IssueWire](https://www.issuewire.com/nanonets-ocr-3-the-new-state-of-the-art-ocr-model-built-for-the-agentic-stack-1861814169403863)
- **注目度**: 🔥
- **ステータス**: 🆕 新規

### InternVL-U (Unified Multimodal)

- **組織**: Shanghai AI Lab (OpenGVLab)
- **公開日**: 2026-03-06
- **ライセンス**: MIT ✅ 商用可
- **サイズ**: 4B / 必要VRAM: 8〜12GB
- **できること**:
  - マルチモーダル理解・推論
  - Text-to-Image 生成
  - 画像編集
  - マルチ画像入力
- **ベンチマーク/比較**: 統合オープンソースベースライン超過(公式発表)
- **動かし方**: ローカル / HF Transformers
- **リンク**: [GitHub](https://github.com/OpenGVLab/InternVL-U) / [HF](https://huggingface.co/OpenGVLab/InternVL-U)
- **注目度**: ⭐
- **ステータス**: 🆕 新規

### GLM-OCR

- **組織**: Zhipu AI (Z.ai)
- **公開日**: 2026-03-11
- **ライセンス**: MIT(レイアウト解析は Apache 2.0)✅ 商用可
- **サイズ**: 0.9B / 必要VRAM: 4GB
- **できること**:
  - 文書解析・OCR
  - キー情報抽出 (KIE)
  - 日本語を含む 32 言語対応
  - 低消費電力(エッジ可)
- **ベンチマーク/比較**: OmniDocBench v1.5 で 94.62 点(公式発表 / Qwen3-VL-235B 比 パラメータ約260分の1)
- **動かし方**: ローカル / HF Transformers / API($0.03 / 1M tok)
- **リンク**: [HF](https://huggingface.co/zai-org/GLM-OCR) / [MarkTechPost](https://www.marktechpost.com/2026/03/15/zhipu-ai-introduces-glm-ocr-a-0-9b-multimodal-ocr-model-for-document-parsing-and-key-information-extraction-kie/)
- **注目度**: 🔥
- **ステータス**: 🆕 新規

## 更新モデル

### Qwen3-VL (4B / 8B Compact Dense)

- **組織**: Alibaba Qwen Team
- **公開日**: 2026年4月初旬
- **ライセンス**: Apache 2.0 ✅ 商用可
- **サイズ**: 4B / 8B(各 Instruct / Thinking 版) / 必要VRAM: 6〜12GB
- **できること**:
  - 長文書・長動画理解(256K 〜 1M context)
  - 32 言語 OCR
  - 2D / 3D 空間グラウンディング
  - ビジュアル・コーディング / GUI エージェント
- **ベンチマーク/比較**: 235B フル版と同等の機能範囲を軽量で実現(公式発表)
- **動かし方**: ローカル / vLLM / FP8 量子化版あり
- **リンク**: [GitHub](https://github.com/QwenLM/Qwen3-VL) / [Qwen Research](https://qwen.ai/research/)
- **注目度**: 🔥
- **ステータス**: 🔄 更新(軽量版追加)

## 情報ソース

- [Hugging Face State of Open Source Spring 2026](https://huggingface.co/blog/huggingface/state-of-os-hf-spring-2026)
- [GLM-OCR on HF](https://huggingface.co/zai-org/GLM-OCR)
- [InternVL-U on GitHub](https://github.com/OpenGVLab/InternVL-U)
- [Nanonets OCR-3](https://nanonets.com/research/nanonets-ocr-3)
- [Qwen3-VL on GitHub](https://github.com/QwenLM/Qwen3-VL)
