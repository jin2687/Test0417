# 動画・マルチモーダル 週次レポート — 2026-04-16

## サマリー
- 新規: 2件(HappyHorse 1.0, Wan 2.7)
- 更新: 1件(LTX-2.3)
- 今週の注目: **HappyHorse 1.0** (Alibaba) — Video Arena で Text-to-Video / Image-to-Video 部門 #1、ただし重み未公開

## 新規モデル

### HappyHorse 1.0

- **組織**: Alibaba (Future Life Lab / Taotian Group)
- **公開日**: 2026-04-10(発表)/ ベンチ登場は 2026-04-01 頃
- **ライセンス**: 未公開(重みは「近日公開予定」とのみ)⚠️
- **サイズ**: 40層統合 Transformer / 詳細パラメータ数は未公開
- **できること**:
  - Text-to-Video(1080p、Elo 1333)
  - Image-to-Video(Elo 1392)
  - 7 言語対応リップシンク生成
  - テキスト・画像・動画・音声の統合処理
- **ベンチマーク/比較**: Artificial Analysis Video Arena で Text-to-Video / Image-to-Video 部門 #1(Seedance 2.0 を約60 Elo 上回る)
- **動かし方**: API のみ(FAL.ai 経由)/ 重み未公開
- **リンク**: [Morningstar/AccessWire](https://www.morningstar.com/news/accesswire/1158274msn/happy-horse-10-surges-to-no1-in-pure-visual-quality-on-artificial-analysis-video-arena) / [CNBC](https://www.cnbc.com/2026/04/10/alibaba-happyhorse-ai-video-model-benchmark-reveal.html) / [FAL.ai](https://fal.ai/happyhorse)
- **注目度**: 🔥
- **ステータス**: 🆕 新規(重みはまだ [API-only])

### Wan 2.7

- **組織**: Alibaba Tongyi Lab
- **公開日**: 2026-04-06
- **ライセンス**: オープンソース ✅ 商用可
- **サイズ**: 150B+ MoE(アクティブ推論時 30〜50B 推定)
- **できること**:
  - Text-to-Video / Image-to-Video(720p、24fps)
  - 思考モードでプロンプト理解を深める
  - 映像品質とモーション精度の向上
- **ベンチマーク/比較**: 具体数値は未公開、Wan 2.2 の後継として「breakthrough」と公式発表
- **動かし方**: HF / ローカル
- **リンク**: [公式発表(FinancialContent)](https://markets.financialcontent.com/stocks/article/abnewswire-2026-4-6-alibaba-launches-wan-27-breakthrough-ai-image-and-video-generation-model-with-thinking-mode) / [wan22.io](https://wan22.io/)
- **注目度**: 🔥
- **ステータス**: 🆕 新規

## 更新モデル

### LTX-2.3

- **組織**: Lightricks
- **公開日**: 2026年3月中
- **ライセンス**: オープンソース(完全オープンウェイト)✅ 商用可
- **サイズ**: 22B / ネイティブ音声・動画同期対応
- **できること**:
  - ネイティブ 4K(最大 50fps)音声同期動画生成
  - Text-to-Video / Image-to-Video
  - デスクトップ動画エディタ統合
- **ベンチマーク/比較**: 「生産環境対応」を公式主張(Wan 2.2、HunyuanVideo-1.5 と競合)
- **動かし方**: ローカル / HF
- **リンク**: [HF](https://huggingface.co/Lightricks/LTX-2) / [GitHub](https://github.com/Lightricks/LTX-2) / [GlobeNewswire](https://www.globenewswire.com/news-release/2026/01/06/3213304/0/en/Lightricks-Open-Sources-LTX-2-the-First-Production-Ready-Audio-and-Video-Generation-Model-With-Truly-Open-Weights.html)
- **注目度**: ⭐
- **ステータス**: 🔄 更新

## 継続参照

### HunyuanVideo-1.5 (Tencent)
- 2025-11-21 リリース、8.3B で HunyuanVideo (13B) 相当品質、Consumer GPU 対応 ✅ 商用可
- リンク: [GitHub](https://github.com/Tencent-Hunyuan/HunyuanVideo-1.5)

### Sora (OpenAI) — サービス終了予告
- 2026-03-24 発表、同月内 API 終了予告
- リンク: [OpenAI](https://openai.com/index/sora-2/)

## 情報ソース

- [Artificial Analysis Video Arena (Morningstar)](https://www.morningstar.com/news/accesswire/1158274msn/happy-horse-10-surges-to-no1-in-pure-visual-quality-on-artificial-analysis-video-arena)
- [CNBC: Alibaba HappyHorse](https://www.cnbc.com/2026/04/10/alibaba-happyhorse-ai-video-model-benchmark-reveal.html)
- [Alibaba Wan 2.7 launch](https://markets.financialcontent.com/stocks/article/abnewswire-2026-4-6-alibaba-launches-wan-27-breakthrough-ai-image-and-video-generation-model-with-thinking-mode)
- [Lightricks LTX-2 release](https://www.globenewswire.com/news-release/2026/01/06/3213304/0/en/Lightricks-Open-Sources-LTX-2-the-First-Production-Ready-Audio-and-Video-Generation-Model-With-Truly-Open-Weights.html)
- [HunyuanVideo-1.5 GitHub](https://github.com/Tencent-Hunyuan/HunyuanVideo-1.5)
- [HF Text-to-Video](https://huggingface.co/models?pipeline_tag=text-to-video)
