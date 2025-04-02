---
title: PaddleOCR
description: PaddleOCR と W&B を統合する方法。
menu:
  default:
    identifier: ja-guides-integrations-paddleocr
    parent: integrations
weight: 280
---

[PaddleOCR](https://github.com/PaddlePaddle/PaddleOCR) は、多言語に対応した、素晴らしい、最先端の、そして実用的なOCRツールを開発し、PaddlePaddle で実装されたモデルのトレーニングをより良く行い、実際に活用できるようにすることを目的としています。PaddleOCR は、OCRに関連する様々な最先端のアルゴリズムをサポートし、産業ソリューションを開発しました。PaddleOCR には、トレーニング と評価メトリクスを、対応するメタデータ と共にモデル のチェックポイント をログ記録するための Weights & Biases のインテグレーションが付属しています。

## ブログ と Colab の例

ICDAR2015 データセット で PaddleOCR を使用してモデル をトレーニングする方法については、[**こちら**](https://wandb.ai/manan-goel/text_detection/reports/Train-and-Debug-Your-OCR-Models-with-PaddleOCR-and-W-B--VmlldzoyMDUwMDIw) を参照してください。また、[**Google Colab**](https://colab.research.google.com/drive/1id2VTIQ5-M1TElAkzjzobUCdGeJeW-nV?usp=sharing) もあり、対応するライブの W&B ダッシュボードは [**こちら**](https://wandb.ai/manan-goel/text_detection) から入手できます。このブログ の中国語版もあります: [**W&B对您的OCR模型进行训练和调试**](https://wandb.ai/wandb_fc/chinese/reports/W-B-OCR---VmlldzoyMDk1NzE4)

## サインアップ して APIキー を作成する

APIキー は、W&B に対してお客様のマシン を認証します。APIキー は、ユーザー プロファイル から生成できます。

{{% alert %}}
より効率的なアプローチとして、[https://wandb.ai/authorize](https://wandb.ai/authorize) に直接アクセスして APIキー を生成できます。表示された APIキー をコピーして、パスワード マネージャー などの安全な場所に保存してください。
{{% /alert %}}

1. 右上隅にあるユーザー プロファイル アイコン をクリックします。
2. [**User Settings**] を選択し、[**API Keys**] セクション までスクロールします。
3. [**Reveal**] をクリックします。表示された APIキー をコピーします。APIキー を非表示にするには、ページ をリロードします。

## `wandb` ライブラリ をインストール してログイン する

`wandb` ライブラリ をローカル にインストール してログイン するには:

{{< tabpane text=true >}}
{{% tab header="コマンドライン" value="cli" %}}

1. `WANDB_API_KEY` [環境変数]({{< relref path="/guides/models/track/environment-variables.md" lang="ja" >}}) を APIキー に設定します。

    ```bash
    export WANDB_API_KEY=<your_api_key>
    ```

2. `wandb` ライブラリ をインストール してログイン します。

    ```shell
    pip install wandb

    wandb login
    ```

{{% /tab %}}

{{% tab header="Python" value="python" %}}

```bash
pip install wandb
```
```python
import wandb
wandb.login()
```

{{% /tab %}}

{{% tab header="Python notebook" value="notebook" %}}

```notebook
!pip install wandb

import wandb
wandb.login()
```

{{% /tab %}}
{{< /tabpane >}}

## `config.yml` ファイル に wandb を追加する

PaddleOCR では、yaml ファイル を使用して構成変数 を指定する必要があります。構成 yaml ファイル の末尾に次のスニペット を追加すると、すべてのトレーニング と検証メトリクス が、モデル チェックポイント と共に W&B ダッシュボード に自動的に記録されます。

```python
Global:
    use_wandb: True
```

[`wandb.init`]({{< relref path="/ref/python/init" lang="ja" >}}) に渡したい追加のオプション の 引数 は、yaml ファイル の `wandb` ヘッダー の下に追加することもできます。

```
wandb:  
    project: CoolOCR  # (オプション) これは wandb プロジェクト名 です
    entity: my_team   # (オプション) wandb team を使用している場合は、ここに team 名を渡すことができます
    name: MyOCRModel  # (オプション) これは wandb run の名前です
```

## `config.yml` ファイル を `train.py` に渡す

yaml ファイル は、PaddleOCR リポジトリ で利用可能な [トレーニング スクリプト](https://github.com/PaddlePaddle/PaddleOCR/blob/release/2.5/tools/train.py) への 引数 として提供されます。

```bash
python tools/train.py -c config.yml
```

Weights & Biases をオンにして `train.py` ファイル を実行すると、W&B ダッシュボード に移動するためのリンク が生成されます。

{{< img src="/images/integrations/paddleocr_wb_dashboard1.png" alt="" >}}

{{< img src="/images/integrations/paddleocr_wb_dashboard2.png" alt="" >}}

{{< img src="/images/integrations/paddleocr_wb_dashboard3.png" alt="W&B Dashboard for the Text Detection Model" >}}

## フィードバック または問題点

Weights & Biases のインテグレーションに関するフィードバック や問題がある場合は、[PaddleOCR GitHub](https://github.com/PaddlePaddle/PaddleOCR) で issue をオープン するか、<a href="mailto:support@wandb.com">support@wandb.com</a> にメール でご連絡ください。
