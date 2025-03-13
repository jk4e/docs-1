---
description: W&B Quickstart
menu:
  default:
    identifier: quickstart_models
    parent: guides
title: W&B Quickstart
url: quickstart
weight: 2
---
Install W&B and track machine learning experiments quickly.

## Sign up and create an API key

An API key authenticates the machine with W&B. Generate an API key from your user profile.

{{% alert %}}
For a streamlined approach, generate an API key directly at [https://wandb.ai/authorize](https://wandb.ai/authorize). Copy the displayed API key and save it in a secure location, such as a password manager.
{{% /alert %}}

1. Click your user profile icon in the upper right corner.
1. Select **User Settings**, then scroll to the **API Keys** section.
1. Click **Reveal**. Copy the displayed API key. To hide the API key, reload the page.

## Install the `wandb` library and log in

To install the `wandb` library locally and log in:

{{< tabpane text=true >}}
{{% tab header="Command Line" value="cli" %}}

1. Set the `WANDB_API_KEY` [environment variable]({{< relref "/guides/models/track/environment-variables.md" >}}) to your API key.

    ```bash
    export WANDB_API_KEY=<your_api_key>
    ```

1. Install the `wandb` library and log in.

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

## Start a run and track hyperparameters

Initialize a W&B Run object in a Python script or notebook using [`wandb.init()`]({{< relref "/ref/python/run.md" >}}), and pass a dictionary with hyperparameter names and values to the `config` parameter:

```python
run = wandb.init(
    project="my-awesome-project",
    config={
        "learning_rate": 0.01,
        "epochs": 10,
    },
)
```

A [run]({{< relref "/guides/models/track/runs/" >}}) is the basic building block of W&B, used for [tracking metrics]({{< relref "/guides/models/track/" >}}), [creating logs]({{< relref "/guides/core/artifacts/" >}}), and more.

## Put it all together

Here is an example of a complete training script:

```python
# train.py
import wandb
import random  # for demo

wandb.login()

epochs = 10
lr = 0.01

run = wandb.init(
    project="my-awesome-project",
    config={
        "learning_rate": lr,
        "epochs": epochs,
    },
)

offset = random.random() / 5
print(f"lr: {lr}")

# Simulating a training run
for epoch in range(2, epochs):
    acc = 1 - 2**-epoch - random.random() / epoch - offset
    loss = 2**-epoch + random.random() / epoch + offset
    print(f"epoch={epoch}, accuracy={acc}, loss={loss}")
    wandb.log({"accuracy": acc, "loss": loss})

# run.log_code()
```

Navigate to the W&B App at [https://wandb.ai/home](https://wandb.ai/home) to view how the logged metrics (accuracy and loss) improved during training.

{{< img src="/images/quickstart/quickstart_image.png" alt="Shows the loss and accuracy that was tracked from runs." >}}

The image above shows the tracked loss and accuracy from each run. Each run object appears in the **Runs** column with a randomly generated name.

## What's next?

Explore the W&B ecosystem.

1. Check out [W&B Integrations]({{< relref "guides/integrations/" >}}) for information on integrating W&B with ML frameworks, libraries, or services.
2. Organize runs, embed visualizations, describe findings, and share updates with collaborators using [W&B Reports]({{< relref "/guides/core/reports/" >}}).
3. Create [W&B Artifacts]({{< relref "/guides/core/artifacts/" >}}) to track datasets, models, dependencies, and results throughout the machine learning pipeline.
4. Automate hyperparameter searches and explore potential models with [W&B Sweeps]({{< relref "/guides/models/sweeps/" >}}).
5. Understand datasets, visualize model predictions, and share insights in a [central dashboard]({{< relref "/guides/models/tables/" >}}).
6. Visit W&B AI Academy for hands-on courses about LLMs, MLOps, and W&B Models at [courses](https://wandb.me/courses).