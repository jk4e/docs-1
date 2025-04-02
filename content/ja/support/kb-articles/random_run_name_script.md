---
title: How do I get the random run name in my script?
menu:
  support:
    identifier: ja-support-kb-articles-random_run_name_script
support:
- experiments
toc_hide: true
type: docs
url: /support/:filename
---

現在の run を保存するには、`wandb.run.save()` を呼び出します。名前を取得するには、`wandb.run.name` を使用します。
