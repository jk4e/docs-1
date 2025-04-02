---
title: Catalyst
description: Pytorch のフレームワークである Catalyst に W&B を統合する方法。
menu:
  default:
    identifier: ja-guides-integrations-catalyst
    parent: integrations
weight: 30
---

[Catalyst](https://github.com/catalyst-team/catalyst) は、再現性 、迅速な実験 、およびコードベースの再利用に重点を置いたディープラーニング のR&D用 PyTorch フレームワーク で、新しいものを創造できます。

Catalyst には、 パラメータ 、 メトリクス 、画像、およびその他の Artifacts を ログ 記録するための W&B インテグレーション が含まれています。

Python と Hydra を使用した例を含む、[インテグレーション のドキュメント](https://catalyst-team.github.io/catalyst/api/loggers.html#catalyst.loggers.wandb.WandbLogger) を確認してください。

## インタラクティブな例

Catalyst と W&B の インテグレーション の動作を確認するには、[example colab](https://colab.research.google.com/drive/1PD0LnXiADCtt4mu7bzv7VfQkFXVrPxJq?usp=sharing) を実行してください。
