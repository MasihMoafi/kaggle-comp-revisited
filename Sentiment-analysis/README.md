# Project Report: Deconstructing Disaster Tweets via Deep Learning
**Author:** Masih Moafi  
**Date:** July 2026  
**Context:** Revisiting and benchmarking historical NLP attempts after 3 years to transition from basic architectures to robust, full-parameter transformer fine-tuning.

---

## 1. Project Objective & Intent
The core objective of this project was to establish a rigorous, mathematically sound pipeline to classify whether text tweets describe real emergency disasters or non-disaster scenarios. This session was executed with a strict focus on mastering deep learning fundamentals, verifying network mechanics at every phase, and bypassing traditional shortcuts to beat historical baselines.

---

## 2. Phase 1: Custom Pipeline & Linear Baseline
Before implementing pre-trained architectures, a baseline pipeline was built completely from scratch using standard PyTorch utilities.

* **Tokenizer Architecture:** Developed a custom vocabulary mapping tool with explicit token management (`<PAD>`: 0, `<UNK>`: 1).
* **The Baseline Model:** A standard embedding mapping layer followed by a mean pooling layer across the sequence dimension, crushing the tensor from $(B, T, C)$ to a simple $(B, C)$ linear layer representation.
* **Mathematical Verification:** Per the neural network recipe, initialization was mathematically verified before training. An untrained network should register a starting loss of:
  $$-\ln(0.5) \approx 0.693$$
  Our baseline model successfully registered an initialization loss of `0.6734`.
* **Overfitting Check:** Gradients were verified by isolating one batch. The model successfully compressed training loss down to `0.0103` and hit **100% accuracy**.

---

## 3. Phase 2: Sequence Modeling (Transformer Encoder)
A simple embedding average destroys temporal context. To introduce structural awareness, the model was upgraded to a custom architecture using a **single Transformer Encoder block** and manual positional indexing.

* **Broadcasting Logic:** Utilizing PyTorch's broadcasting engine, a flat 1D sequence tensor was passed to the positional embedding layer, yielding features that seamlessly aligned with the $(B, T, C)$ word tensors during the forward pass.
* **Result:** This custom sequence-aware model pushed peak validation accuracy to **78.07%**.

---

## 4. Phase 3: Supervised Fine-Tuning (SFT) with DistilBERT



* **Architecture Shift:** Transitioned to HuggingFace's **DistilBERT**, utilizing a pre-trained WordPiece vocabulary with specialized `[CLS]` and `[SEP]` tokens.
* **Full Fine-Tuning:** Every parameter was unfrozen and updated using a conservative learning rate ($2 \times 10^{-5}$) to prevent the catastrophic destruction of pre-trained language syntax.
* **Early Stopping:** Monitored validation loss divergence to halt training at the optimal inflection point.

### Final Performance Metrics:
| Epoch | Train Loss | Val Acc | Status |
| :--- | :--- | :--- | :--- |
| 1 | 0.4609 | 83.06% | - |
| 2 | 0.3356 | **83.32%** | **PEAK** |
| 3 | 0.2602 | 82.86% | Overfitting |
| 5 | 0.1377 | 81.42% | Stopped |

<img width="1471" height="829" alt="disaster-tweet-revisited" src="https://github.com/user-attachments/assets/2b9766f3-5110-4f6f-a794-41a4c522cd07" /> 

---

Project's README from three years ago: 

## NLP Project: Sentiment Analysis Using Logistic Regression and Random Forest

### Project Overview

This project focuses on sentiment analysis using text classification techniques, specifically logistic regression and random forest classifiers. The goal is to predict whether a given tweet is indicative of an actual disaster or not. The project is based on the Kaggle competition called "Disaster Tweets," where the dataset and additional information can be found.

### Methods Used

    Lemmatization: The text data is preprocessed using lemmatization, which reduces words to their base form. This helps in standardizing the vocabulary and improving the accuracy of the models.

    Data Processing: The text data is converted to lowercase and spaces are replaced with underscores to ensure consistency and facilitate further analysis.

    Feature Extraction: The TF-IDF (Term Frequency-Inverse Document Frequency) vectorization technique is used to convert the text data into numerical features. This approach calculates the importance of each word in the tweet based on its frequency and rarity across the entire corpus.

    Model Training and Evaluation:
        Logistic Regression: A logistic regression model is trained on the preprocessed text data and corresponding target labels. This model is well-suited for binary classification tasks like sentiment analysis.
        Random Forest: A random forest classifier is trained on the same preprocessed data. Random forests are an ensemble learning method that combines multiple decision trees to make predictions.

    Model Comparison: The classification reports are generated for both logistic regression and random forest models to evaluate their performance. The metrics in the reports provide insights into precision, recall, and F1-score for each class, helping assess the models' effectiveness.

### Best Performing Models

From the various algorithms used, both logistic regression and random forest classifiers demonstrated the best performance.


## 5. Conclusion & Competitive Standing
The final model achieved a legitimate validation accuracy of **83.32%**. By successfully implementing full-parameter SFT, tracking gradient flow, and managing positional embeddings, this project marks a complete transition from introductory, rudimentary scripts to engineering production-capable transformer workflows.

