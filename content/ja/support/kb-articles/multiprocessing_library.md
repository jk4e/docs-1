---
title: Does W&B use the `multiprocessing` library?
menu:
  support:
    identifier: ja-support-kb-articles-multiprocessing_library
support:
- experiments
toc_hide: true
type: docs
url: /support/:filename
---

はい、W&B は `multiprocessing` ライブラリを使用します。次のようなエラーメッセージは、問題が発生している可能性を示しています。

```
An attempt has been made to start a new process before the current process 
has finished its bootstrapping phase.
```

これを解決するには、`if __name__ == "__main__":` でエントリポイント保護を追加します。この保護は、スクリプトから直接 W&B を実行する場合に必要です。
