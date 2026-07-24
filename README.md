---
name: Kaggle Projects Revisited
type: machine-learning experiments revisiting older projects with stronger modern baselines
---

# Kaggle Projects Revisited

**The strongest result in this repository is the Disaster Tweets revisit: a progression from a from-scratch text baseline to a custom Transformer and full DistilBERT fine-tuning.**

The final recorded DistilBERT run reached **83.32% validation accuracy** on the experiment's held-out validation split. The project also records a custom single-block Transformer at **78.07%**, making the progression itself inspectable rather than presenting only the final model.

[Read the Disaster Tweets report →](./Sentiment-analysis/README.md)

## Quick start

```bash
git clone https://github.com/MasihMoafi/kaggle-comp-revisited.git
cd kaggle-comp-revisited
```

Each project is independent. Start with `Sentiment-analysis/` for the strongest current experiment and its recorded metrics.

## Lead project — Disaster Tweets

The Disaster Tweets revisit reconstructs an older NLP project in three stages:

1. **From-scratch baseline** — custom vocabulary, embedding layer, mean pooling, and explicit initialization/overfit checks.
2. **Custom Transformer encoder** — adds sequence structure and reaches **78.07% peak validation accuracy**.
3. **Full DistilBERT fine-tuning** — all parameters unfrozen with early stopping; peak recorded validation accuracy: **83.32%**.

The experiment also preserves the training curve screenshot and epoch-level validation results in [`Sentiment-analysis/README.md`](./Sentiment-analysis/README.md).

These are validation results from this experiment, not a claim of state-of-the-art Disaster Tweets performance.

## Other projects

### [Predicting Housing Prices](./Predicting-Housing-Prices)
Regression-based housing-price prediction.

### [Evaluating Work Hours](./Evaluating-Work-Hours)
An early personal experiment using linear and polynomial regression to analyze work hours.

### [Movie Recommendation](./Movie-recommendation)
Recommendation experiments using content-based methods and K-means clustering.

### [Transfer Learning](./Transfer-Learning)
Computer-vision exercises using pretrained models.

## Current state

### Implemented and evidenced

- Disaster Tweets baseline → custom Transformer → DistilBERT progression.
- Recorded validation metrics and training curve for the Disaster Tweets revisit.
- Four additional historical ML/data-science projects preserved in their own directories.

### Implemented but not fully benchmarked

- The Disaster Tweets result is reported on the project's validation split; the repository does not currently present repeated-seed averages, a Kaggle leaderboard score, or a controlled benchmark against multiple modern pretrained baselines.
- The other projects vary in age and reproducibility quality.

### Planned

No shared repository roadmap is tracked.

The most useful follow-up for Disaster Tweets would be a fixed split/seed, repeated runs, and a direct comparison against a simple pretrained baseline under the same protocol.

### Intentionally unsupported / not claimed

- No unified package or API across the projects.
- No state-of-the-art claim for Disaster Tweets.
- No claim that every historical project reflects current best practice.

## What sets this repository apart

The useful part is the **before/after comparison**: an older ML project was revisited with stronger fundamentals and modern fine-tuning rather than simply replaced or deleted.

For Disaster Tweets, the repository shows the progression from a hand-built baseline to a custom Transformer and then pretrained-model fine-tuning, with measured validation changes at each stage.

## Evals and test series

For Disaster Tweets, the strongest evidence currently available is:

- initialization sanity checking;
- one-batch overfit verification;
- custom Transformer peak validation accuracy of **78.07%**;
- DistilBERT peak validation accuracy of **83.32%**;
- epoch-level validation-loss/accuracy tracking and early stopping.

What this does not establish by itself:

- variance across seeds;
- final hidden-test/Kaggle leaderboard performance;
- superiority to all alternative pretrained models.

Evaluation for the other subprojects remains project-specific.

## Future development

Keep the repository focused on meaningful revisits. A new revisit should show a measurable improvement in method, evaluation discipline, or implementation quality over the original version—not just a newer model name.
