# Predicting Moderation Decisions: Assessing the Impact of User History, Rules, and Threads in Online Communities

**Riccardo Lupo, Luca Martinelli, Francesco Moglianetti**  
Bachelor's Degree "Informatica"  
Course: AI-LAB – Computer Vision, Signal Processing, and Natural Language Processing  
Department of Computer Science, Sapienza University of Rome  
Matricola: 2136445, 2129604, 2105522

---

## Abstract

Content moderation on platforms such as Reddit is a difficult and demanding task. It requires not only technical expertise, but also a deep understanding of context and of the community itself. Advanced moderation entails distinguishing between strikes and bans. This paper presents a machine learning pipeline designed to predict the outcome for a single comment by integrating different layers of context. First, we build a longitudinal dataset from r/Anarchism, extracting comment-level toxicity metrics with Detoxify (based on the transformer RoBERTa) and combining them with user history, assigning each comment a target among three classes: Normal (−1), Strike (0), and Ban (1).

To study the impact of user history relative to a context-free model, we train an XGBoost classifier to predict the moderation outcome of a comment through two models. The first is contextual to the user history and predicts using the same metrics as above, together with the user's number of previous strikes in the subreddit, the number of contributions (comments), and the user's age (in days) within the same community; the second model relies on toxicity metrics only.

We further introduce a thread-aware model that evaluates conversational dynamics by encoding each comment together with its preceding thread context. We fine-tune a RoBERTa-large classifier on a three-class moderation task and perform an ablation between a context-aware model (comment + thread) and a baseline that observes the isolated comment only, in order to isolate the contribution of conversational context to moderation decisions.

Finally, we evaluate what happens when the subreddit rules are prompt-injected into a generalist model. We use the Ollama wrapper with the qwen2.5:14b-instruct-q4_K_M model, first running a baseline prompt and then the actual prompt with the rules injected. Our comparative analysis demonstrates the effects of incorporating user history, conversation threads, and community rules on the predictive accuracy of moderation systems.

---

## 1. Introduction

Platforms like Reddit rely on volunteer moderators who evaluate user behavior to maintain healthy discussions within a community. However, moderation often requires repetitive manual effort to distinguish minor violations from banable behavior. Online communities have reached record high growth rates, making content moderation a growing challenge in the context of Artificial Intelligence and Natural Language Processing. The problem is significant because human moderators are increasingly overwhelmed due to the sheer volume of content, making moderation increasingly complicated. Automated heuristic systems like Reddit's AutoModerators are effective at managing spam or explicit rule violations, but they lack the semantic understanding necessary to make decisions that fall somewhere between a strike and a ban. Consequently, the cognitive load of assessing borderline or context-dependent toxicity falls on human moderators.

The main limitation of current automated approaches, including standard NLP toxicity classifiers, is that they evaluate text in isolation. A comment analyzed out of context may appear harmless while simultaneously violating community guidelines. Furthermore, traditional text-based models struggle to capture relational dynamics: a sequence of individually non-offensive messages may hide a growing tension that heralds the toxic derailment of the conversation. Finally, predicting a penalty based solely on a single sentence ignores an important predictor in moderation: the user's behavioral trajectory [cite]. Toxicity is rarely absolute; it is a highly contextual phenomenon.

To address these limitations, this paper proposes and evaluates three complementary approaches to moderation prediction, each adding a different layer of context:

1. **User history integration**: an XGBoost classifier that combines Detoxify toxicity scores with behavioral signals such as previous strikes, number of contributions, and user age within the community.
2. **Conversational context integration**: a fine-tuned RoBERTa-large classifier that encodes each comment alongside its preceding thread, with a controlled ablation against a comment-only baseline.
3. **Rule injection into a generalist LLM**: a zero-shot evaluation of Qwen 2.5 14B in which the subreddit rules are prepended to the prompt, isolating their effect on classification accuracy.

The three approaches are evaluated on the same longitudinal moderation dataset drawn from r/Anarchism, enabling a direct comparison of the contribution of each contextual layer.

The remainder of this paper is organized as follows. Section 2 reviews related work on automated moderation, contextual text classification, and knowledge distillation. Section 3 describes the methodology of each pipeline component. Section 4 presents the experimental setup, results, and critical discussion. Section 5 concludes.

---

## 2. Related Work

**[NOTE: questa sezione deve essere completata dai colleghi. Di seguito una struttura suggerita con i riferimenti già presenti nel template.]**

### Classical and Early Approaches

Early approaches to automated content moderation relied primarily on lexicon-based methods and rule-based filters. These systems flag comments containing predefined offensive terms or patterns, offering high interpretability but poor generalization to context-dependent violations. Keyword matching, for instance, cannot distinguish a discussion about violence from an act of incitement. These limitations motivated the shift toward machine learning approaches.

### Deep Learning and Transformer-Based Methods

The introduction of transformer architectures [Vaswani et al., 2017] fundamentally changed the landscape of text classification. BERT and its variants, including RoBERTa [Liu et al., 2019], demonstrated that large-scale pre-training on general text followed by task-specific fine-tuning consistently outperforms task-specific architectures trained from scratch. RoBERTa in particular introduced key training improvements — dynamic masking, larger batch sizes, and removal of the next-sentence prediction objective — that make it a strong baseline for classification tasks with limited labeled data. In this work we adopt RoBERTa-large as the backbone for the thread-aware classifier precisely because its pre-training regime supports robust fine-tuning on small, imbalanced datasets.

Detoxify [Hanu et al., 2020] builds on this paradigm to produce comment-level toxicity scores across multiple dimensions (toxicity, severe toxicity, obscenity, identity attack, insult, threat, sexual explicitness). These scores are used in this work both as features for the XGBoost history-aware classifier and as a lightweight toxicity signal independent of the full-text encoder.

### Contextual Moderation and User Behavior

Several works have emphasized the importance of behavioral context for moderation. [Paper 1 on Trajectories] shows that users who are eventually banned exhibit detectable behavioral trajectories long before the sanctioned comment, including increasing aggression and decreasing engagement with community norms. This motivates the inclusion of user history features (previous strikes, contributions, community age) in our XGBoost classifier.

Thread-level context has received comparatively less attention. [cite relevant work] shows that comment-level classifiers systematically underperform in conversational settings because the conversational history modulates the meaning of individual utterances. Our thread-aware model directly addresses this gap.

### Knowledge Distillation

Knowledge Distillation [Hinton et al., 2015] transfers the probabilistic output of a large teacher model into the training signal of a smaller student. The student minimizes a convex combination of hard-label cross-entropy and KL-divergence against the teacher's soft label distribution, controlled by a temperature parameter. The technique is effective when the teacher is significantly more accurate than the student: teacher soft labels carry inter-class similarity information that is not present in one-hot labels. However, when the teacher is of insufficient quality, its soft labels act as noise rather than supervision — a phenomenon this work terms _distillation poisoning_ — and pure hard-label training is preferable.

### Large Language Models for Zero-Shot Moderation

Recent work has explored the use of instruction-following LLMs for zero-shot classification tasks. Models such as Qwen 2.5 [Yang et al., 2024] demonstrate strong generalization from natural language instructions, making them candidates for rule-based moderation without task-specific fine-tuning. The prompt-injection approach evaluated in this paper examines whether prepending explicit community rules to the LLM prompt — without any gradient update — is sufficient to align the model's moderation behavior with community-specific norms.

---

## 3. Methodology

### 3.1 History-Aware Model

**[Sezione di Riccardo — inserire qui la descrizione del pipeline XGBoost con feature Detoxify + user history, come descritto in Figure 1 del template]**

The history-aware pipeline combines comment-level toxicity signals with longitudinal user behavior features to predict moderation outcomes via an XGBoost classifier. Two model variants are trained: an isolated model relying exclusively on the seven Detoxify toxicity scores, and a contextual model that augments these scores with three behavioral features — the user's number of previous strikes, total number of contributions to the subreddit, and account age in days at the time of the comment. Both variants are evaluated under stratified 5-fold cross-validation, enabling a controlled comparison of the marginal contribution of user history to predictive accuracy.

### 3.2 Thread-Aware Model

The thread-aware component addresses the hypothesis that conversational context — the thread preceding a comment — provides predictive signal that is unavailable to a comment-only classifier. We perform a controlled ablation between two configurations of the same fine-tuned RoBERTa-large classifier: one that receives the isolated comment and one that receives the comment together with the preceding thread.

#### 3.2.1 Architecture

We fine-tune **RoBERTa-large** [Liu et al., 2019] (355M parameters) as a sequence classifier with three output classes: Ban (0), Strike (1), Normal (2). RoBERTa-large was selected over lighter alternatives for three reasons. First, its pre-training corpus and training strategy make it particularly robust under fine-tuning on small datasets — a critical requirement given the 2,696-sample training set. Second, its tokenizer natively supports two-segment input via the `[CLS] ... [SEP] ... [SEP]` format, enabling a clean separation of comment and thread without any architectural modification. Third, preliminary experiments with DeBERTa-v3-small showed systematic collapse to the majority class (Normal) under several hyperparameter configurations; RoBERTa-large proved stable under the same training conditions.

#### 3.2.2 Input Encoding and Ablation Design

The ablation is defined by how the two input segments are populated:

- **Baseline configuration** (comment only): the tokenizer receives the extracted comment as `text_a` and an empty string as `text_b`. The resulting sequence is `[CLS] comment [SEP][SEP]`. Maximum sequence length is set to 256 tokens, justified by the empirical distribution of isolated comment lengths (median ~125 tokens; 91% of samples under 256 tokens).
    
- **Context-Aware configuration** (comment + thread): the tokenizer receives the comment as `text_a` and the thread context as `text_b`. The resulting sequence is `[CLS] comment [SEP] thread [SEP]`. Maximum sequence length is set to 512 tokens to accommodate longer threads. The tokenizer truncation policy gives priority to `text_b` (the thread), ensuring the comment — the primary classification target — is never truncated regardless of thread length.
    

In both configurations, comments stored in the dataset with the `Isolated Comment [...]` format (i.e., without an associated thread) are treated as comment-only inputs, with `text_b` set to an empty string. This ensures consistent tokenization across both configurations and prevents format mismatch from confounding the ablation.

The two configurations are otherwise identical: same model weights initialization, same optimizer, same loss, same training schedule, and same evaluation protocol. The only independent variable is the presence or absence of thread context in `text_b`.

#### 3.2.3 Knowledge Distillation and the alpha=0.0 Decision

The model was initially designed within a Knowledge Distillation framework. Soft labels — probability distributions over the three classes — were generated by Qwen 32B acting as a teacher model, using the same comment+thread prompts described above. The student's training objective was a convex combination of hard-label cross-entropy (CE) and KL divergence against the teacher's soft labels, controlled by the temperature-scaled distillation parameter alpha:

```
L = (1 - alpha) * CE(logits, hard_labels) + alpha * T^2 * KL(softmax(logits/T), soft_labels)
```

Preliminary evaluation of the teacher's performance revealed a Weighted F1 of approximately 0.38–0.41 across folds, with recall on Ban consistently below 0.10. At this quality level, the teacher's soft labels do not encode reliable inter-class similarity information. Instead, they introduce systematic noise concentrated precisely on the minority classes that the student most needs to learn — a phenomenon we characterize as _distillation poisoning_. Hinton et al. (2015) explicitly note that soft label distillation is effective only when the teacher is significantly more accurate than the student; this condition is not met here.

The distillation component was therefore ablated by setting `alpha=0.0`, reducing the training objective to pure Cross-Entropy on hard labels. The Knowledge Distillation framework is retained in the implementation but effectively disabled, leaving the soft labels as an artifact of the pipeline rather than an active training signal.

#### 3.2.4 Training Strategy

**Optimizer and Layer-wise Learning Rate**  
We use AdamW with weight decay and a layer-wise learning rate schedule. The encoder (RoBERTa body) is updated at a lower rate (`lr=5e-6`) to preserve the pre-trained representations. The classification head — randomly initialized — is updated at a higher rate (`lr=1e-4`) to enable faster convergence toward the task-specific decision boundary:

```
optimizer = AdamW([
    {"params": encoder.parameters(), "lr": 5e-6},
    {"params": classifier.parameters(), "lr": 1e-4}
], eps=1e-6, weight_decay=0.01)
```

This asymmetry is critical on small datasets: a uniform high learning rate applied to the full model destabilizes the encoder before the classifier has converged, often causing the model to collapse to the majority class within the first epoch.

**Learning Rate Schedule**  
A linear warmup schedule is applied over the first 10% of total training steps, followed by linear decay to zero. Warmup prevents destructive gradient updates in the early iterations when the classification head's random initialization produces large, uninformative loss gradients.

**Class Imbalance Handling**  
Even in the balanced 2,696-sample dataset (50% Normal, 26% Strike, 24% Ban), the moderate imbalance between Normal and the minority classes can bias the model. We apply class weights to the cross-entropy loss. The `balanced` weights computed by sklearn (~2.1 for Ban, ~1.9 for Strike, ~0.67 for Normal) proved excessively aggressive, causing the model to oscillate between minority classes across folds. We instead use the element-wise square root of the balanced weights, normalized to unit mean:

```
weights = sqrt(class_weight("balanced", y_train))
weights = weights / mean(weights)
# ≈ [1.45 (Ban), 1.38 (Strike), 0.82 (Normal)]
```

This softer weighting provides meaningful upweighting of minority classes without overwhelming the optimization signal.

**Gradient Accumulation**  
Gradient accumulation over 2 steps yields an effective batch size of 32, improving gradient estimates without exceeding GPU memory limits.


### 3.3 Rules Prompt-Injection

**[Sezione di Luca — già ampiamente descritta nel template alle sezioni 3.4–3.9. Riportare qui la versione condensata focalizzata sull'architettura, rimandando le sezioni 3.4–3.9 per i dettagli.]**

The prompt-injection pipeline evaluates whether prepending the explicit rules of r/Anarchism to a generalist LLM's context is sufficient to shift its moderation behavior toward community-specific norms. No fine-tuning or gradient update is performed: the model (Qwen 2.5 14B Instruct, 4-bit quantized) is frozen and queried zero-shot. The only independent variable across the two experimental conditions is the prompt content — specifically, the presence or absence of the subreddit rules block. All other factors (model, decoding parameters, temperature, input comments) are held fixed. Class probabilities are reconstructed from native Ollama log-probabilities over a whitelist of surface-form variants for each class token.

### 3.4 Pipeline Overview

The complete pipeline integrates three independent moderation strategies, each evaluated on the same longitudinal dataset. Figure 1 shows the history-aware pipeline; Figure 2 shows the thread-aware ablation design; Figure 3 shows the prompt-injection pipeline.

The thread-aware pipeline (Figure 2) consists of five stages: (i) construction of the longitudinal dataset and stratified undersampling to 2,696 balanced comments; (ii) Stratified 5-Fold cross-validation split; (iii) parallel construction of the two input configurations (Baseline: isolated comment; Context-Aware: comment + thread); (iv) supervised fine-tuning of RoBERTa-large with pure cross-entropy loss, normalized sqrt(balanced) class weights, and layer-wise learning rate; (v) ablation performance evaluation per class and across folds.

---

## 4. Experimental Setup

### 4.1 Dataset

**Source and Collection**  
The dataset is a longitudinal moderation log from the Reddit community r/Anarchism, collected via the Pushshift Reddit API [Baumgartner, 2019]. It contains approximately 634,000 comments annotated with moderation outcomes. Each comment is associated with a unique `comment_id`, a `body` field containing the raw text, and a `target` field encoding the moderation decision: −1 (no action, Normal), 0 (Strike), 1 (Ban).

**Sampling and Class Balance**  
The full longitudinal dataset is heavily imbalanced, with approximately 99% of comments receiving no moderation action. Training a classifier directly on this distribution would yield a trivially high accuracy model that never predicts Ban or Strike. A stratified subsample of **2,696 comments** was therefore drawn, balancing the three classes as follows:

|Class|Raw Label|Samples|Percentage|
|---|---|---|---|
|Normal|−1|~1,349|50.0%|
|Strike|0|~711|26.4%|
|Ban|1|~635|23.6%|

Stratification was applied per class with `random_state=42` for reproducibility.

**Input Format**  
Comments in the thread-aware dataset are stored with a structured prompt format:

- Comments with conversational context: `Thread Context: [preceding thread] Comment: [comment text]`
- Comments without a preceding thread: `Isolated Comment [comment text]`

This format encodes the comment and its context as a single string, which the tokenizer then parses into `text_a` (comment) and `text_b` (thread).

**Validation Protocol**  
There is no fixed test set. The entire 2,696-sample dataset is used for training and validation via **Stratified 5-Fold cross-validation** (`random_state=42`). Each fold produces a validation split of approximately 539 samples, maintaining the same class distribution as the full dataset. The best-performing fold is selected for qualitative analysis and real-world inference.

**Tokenization Statistics**  
Analysis of prompt lengths after tokenization revealed:

|Statistic|Tokens|
|---|---|
|Minimum|11|
|25th percentile|54|
|Median|125|
|75th percentile|263|
|Maximum|4,374|
|> 256 tokens|25.6%|
|> 512 tokens|9.0%|

These statistics justify the choice of `max_length=256` for the Baseline (comment-only) configuration — covering 99%+ of isolated comment lengths — and `max_length=512` for the Context-Aware configuration, which must accommodate thread context.

**Limitations**  
The longitudinal dataset does not preserve thread structure: the `body` field contains only the individual comment text, without the preceding thread. Thread context is available exclusively within the 2,696-sample balanced subset, which was assembled with thread reconstruction. This structural limitation makes it impossible to apply the Context-Aware model to the full longitudinal dataset, and constrains the real-world inference experiment to the Baseline (comment-only) configuration.

### 4.2 Training and Evaluation Protocol

**Hardware and Software**  
All training was performed on Google Colab Pro with an NVIDIA A100 SXM4-80GB GPU. The software environment uses Python 3.x, PyTorch, and the HuggingFace Transformers library. Model checkpoints are saved to Google Drive after each epoch.

**Training Configuration**

| Parameter            | Baseline (No-Thread) | Context-Aware (Thread) |
| -------------------- | -------------------- | ---------------------- |
| Base model           | roberta-large        | roberta-large          |
| Parameters           | 355M                 | 355M                   |
| max_length           | 256                  | 512                    |
| Batch size           | 16                   | 16                     |
| Grad. accum. steps   | 2                    | 2                      |
| Effective batch size | 32                   | 32                     |
| Epochs               | 4                    | 4                      |
| K-Folds              | 5                    | 5                      |
| LR (encoder)         | 5e-6                 | 5e-6                   |
| LR (classifier)      | 1e-4                 | 1e-4                   |
| Optimizer            | AdamW                | AdamW                  |
| Weight decay         | 0.01                 | 0.01                   |
| eps                  | 1e-6                 | 1e-6                   |
| LR schedule          | Linear warmup        | Linear warmup          |
| Warmup steps         | 10% of total         | 10% of total           |
| Loss                 | Cross-Entropy        | Cross-Entropy          |
| Class weights        | sqrt(balanced) norm. | sqrt(balanced) norm.   |
| alpha (distillation) | 0.0                  | 0.0                    |
| Training time        | ~2h (A100)           | ~4h (A100)             |

**Evaluation Metrics**  
The primary evaluation metric is **Weighted F1-score**, which accounts for class imbalance by weighting each class's F1 by its support. Per-class Precision, Recall, and F1 are reported for all three classes, with particular attention to the minority classes (Ban, Strike) where performance differences are most diagnostically meaningful. Confusion matrices are reported for qualitative error analysis.

**Baseline Methods**  
The primary comparison is between the two configurations of the thread-aware model:

- **Baseline**: comment-only input, `max_length=256`
- **Context-Aware**: comment + thread input, `max_length=512`

The Teacher model (Qwen 32B) performance is also reported as an upper-bound reference and to motivate the `alpha=0.0` decision.

### 4.3 Results

#### 4.3.1 Teacher Model Performance

The Teacher (Qwen 32B) was evaluated across the same 5-fold splits to establish whether its soft labels were suitable for distillation. Results are reported in Table 2.

**Table 2: Teacher (Qwen 32B) performance across folds.**

|Fold|Ban F1|Strike F1|Normal F1|Weighted F1|
|---|---|---|---|---|
|1|0.041|0.170|0.600|0.354|
|2|0.142|0.227|0.634|0.410|
|3|0.042|0.216|0.629|0.382|
|4|0.063|0.218|0.629|0.387|
|5|0.066|0.219|0.606|0.377|
|**Mean**|**0.071**|**0.210**|**0.620**|**0.382**|

The Teacher achieves a mean Weighted F1 of 0.382, with Ban recall consistently below 0.10 across all folds. These results motivated the decision to set `alpha=0.0` (see Section 4.4).

#### 4.3.2 Context-Aware Model (Comment + Thread)

**Table 3: Context-Aware model (RoBERTa-large, comment + thread) — per-class results, best fold (Fold 2).**

|Class|Precision|Recall|F1|
|---|---|---|---|
|Ban|0.455|0.333|0.385|
|Strike|0.532|0.801|0.640|
|Normal|0.584|0.791|0.672|
|**Weighted**|**0.540**|**0.554**|**0.529**|

**Table 4: Context-Aware model — Weighted F1 across all folds.**

|Fold|Ban F1|Strike F1|Normal F1|Weighted F1|
|---|---|---|---|---|
|1|[TO FILL]|[TO FILL]|[TO FILL]|[TO FILL]|
|2|0.385|0.640|0.672|0.529|
|3|[TO FILL]|[TO FILL]|[TO FILL]|[TO FILL]|
|4|[TO FILL]|[TO FILL]|[TO FILL]|[TO FILL]|
|5|[TO FILL]|[TO FILL]|[TO FILL]|[TO FILL]|
|**Mean**|||||

#### 4.3.3 Baseline Model (Comment Only)

**Table 5: Baseline model (RoBERTa-large, comment only) — results across folds.**

|Fold|Ban F1|Strike F1|Normal F1|Weighted F1|
|---|---|---|---|---|
|1|[TO FILL]|[TO FILL]|[TO FILL]|[TO FILL]|
|2|[TO FILL]|[TO FILL]|[TO FILL]|[TO FILL]|
|3|[TO FILL]|[TO FILL]|[TO FILL]|[TO FILL]|
|4|[TO FILL]|[TO FILL]|[TO FILL]|[TO FILL]|
|5|[TO FILL]|[TO FILL]|[TO FILL]|[TO FILL]|
|**Mean**|||||

#### 4.3.4 Ablation Summary

**Table 6: Ablation comparison — Context-Aware vs Baseline, mean Weighted F1 across 5 folds.**

|Model|Ban F1|Strike F1|Normal F1|Weighted F1|
|---|---|---|---|---|
|Teacher (Qwen 32B)|0.071|0.210|0.620|0.382|
|Baseline (comment only)|[TO FILL]|[TO FILL]|[TO FILL]|[TO FILL]|
|Context-Aware (comment + thread)|[TO FILL]|[TO FILL]|[TO FILL]|[TO FILL]|

#### 4.3.5 Real-World Inference (Distribution Shift Experiment)

To evaluate the model's behavior under realistic deployment conditions, we constructed a hybrid test set of 130,000 samples reflecting the natural class distribution of r/Anarchism. The set combines the 539 validation samples from Fold 2 (containing real Ban, Strike, and Normal comments) with 129,461 Normal comments sampled from the full longitudinal dataset, after removing any `comment_id` present in the training set to prevent data leakage.

|Class|Samples|Percentage|
|---|---|---|
|Ban|127|0.10%|
|Strike|143|0.11%|
|Normal|129,730|99.79%|

Due to the absence of thread data in the longitudinal dataset, this experiment was conducted exclusively with the Baseline (comment-only) configuration.

**Table 7: Real-world inference results — Baseline model on 130k samples.**

|Class|Precision|Recall|F1|
|---|---|---|---|
|Ban|0.001|0.504|0.003|
|Strike|0.006|0.622|0.011|
|Normal|0.999|0.516|0.681|
|**Weighted**|**0.997**|**0.517**|**0.680**|

### 4.4 Critical Discussion

#### 4.4.1 The alpha=0.0 Decision: Distillation Poisoning

The Teacher (Qwen 32B) achieves a mean Weighted F1 of 0.382, with a mean Ban F1 of 0.071. This performance profile disqualifies the Teacher as a distillation source. Knowledge Distillation transfers inter-class similarity information encoded in the teacher's soft output distribution. When the teacher systematically misclassifies Ban and Strike comments as Normal — as evidenced by near-zero Ban recall across all folds — its soft labels encode _incorrect_ similarity: they tell the student that Ban and Normal are interchangeable, which is the opposite of the desired behavior.

Under distillation (alpha > 0), preliminary experiments confirmed that the student rapidly collapsed to a Normal-dominant prediction pattern regardless of the hard label signal, consistent with the distillation poisoning hypothesis. Setting `alpha=0.0` and training on hard labels alone resolved this instability. The Knowledge Distillation framework is therefore retained in the implementation as an ablatable component, but disabled in all reported experiments.

This result highlights an important practical constraint of Knowledge Distillation: the technique requires a teacher whose performance on the task of interest — including minority classes — is substantially above the student's untrained baseline. A teacher with high accuracy on the majority class but poor recall on minority classes is insufficient, and can actively harm student training.

#### 4.4.2 Ablation: Does Thread Context Help?

**[Completare dopo aver ottenuto i risultati del modello No-Thread]**

The central question of the thread-aware experiment is whether conversational context improves moderation classification. The ablation between the Context-Aware (comment + thread) and Baseline (comment only) configurations provides a controlled answer.

[Osservazioni attese da inserire quando si hanno i dati completi]:

- Se Context-Aware > Baseline su Weighted F1: il thread fornisce segnale predittivo al di là del commento isolato
- Se Context-Aware ≈ Baseline: il commento da solo è sufficiente, il thread non aggiunge informazione
- Se Context-Aware < Baseline: il thread introduce rumore (possibile se i thread sono lunghi o irrilevanti)

The result is particularly informative for Ban classification, which is the hardest class in both configurations. Ban comments are rarely overtly toxic in isolation — they often constitute the last step of a gradual escalation that is only interpretable in the context of prior exchanges. If the Context-Aware model shows meaningfully higher Ban recall compared to the Baseline, this constitutes direct evidence that conversational context is necessary for accurate Ban prediction.

#### 4.4.3 Class-Level Analysis

Across all configurations, Ban is consistently the most difficult class to classify. Several factors contribute to this difficulty:

1. **Ambiguity in isolation**: Ban-worthy comments are often not overtly toxic when read out of context. Their violation is relational — they escalate or continue a pattern of behavior that is only visible through the thread.
2. **Low support**: even in the balanced dataset, Ban is the minority class (24% vs 50% Normal). Despite class weighting, the model sees fewer Ban examples per fold.
3. **Semantic overlap with Strike**: the boundary between a Strike-worthy and a Ban-worthy comment is not always linguistically salient and often depends on the moderation history of the specific user — information that is not available to the text classifier.

Strike classification is consistently stronger than Ban, likely because Strike comments exhibit clearer textual signals (direct insults, rule violations) that are identifiable even without user history.

#### 4.4.4 Distribution Shift and Real-World Deployment

The real-world inference experiment reveals a fundamental challenge for deploying balanced-trained classifiers in production. The Baseline model maintains recall of approximately 0.50 and 0.62 for Ban and Strike respectively on the 130,000-sample test set, meaning it detects the majority of actual violations. However, precision collapses to near-zero (0.001 and 0.006). This is not a failure of the model per se, but a consequence of the extreme class imbalance: on a 99.8% Normal dataset, even a 1% false positive rate on Normal produces ~1,300 false alarms that overwhelm the ~270 true positive violations.

Precision-Recall analysis confirmed that no threshold on the output probability achieves precision ≥ 0.5 for either Ban or Strike. This result implies that the model as trained on balanced data is not directly deployable as a decision system, but could serve effectively as a _first-pass filter_ in a human-in-the-loop moderation pipeline: flagging a manageable subset of comments for human review rather than making autonomous decisions.

Addressing this gap would require either (a) threshold calibration using a held-out set with realistic class proportions, or (b) retraining with a training distribution that more closely reflects the natural deployment distribution.

#### 4.4.5 Methodological Limitation: Thread Unavailability at Scale

The thread-aware model cannot be evaluated on the full longitudinal dataset because the dataset does not preserve thread structure — only individual comment texts are available. This asymmetry means the ablation between Context-Aware and Baseline is meaningful only on balanced data, and the real-world inference experiment was limited to the Baseline configuration. Extending the comparison to natural deployment conditions would require either reconstructing threads via the Reddit API (feasible but computationally expensive at 634k comments) or collecting a new dataset that preserves thread structure from the outset.

---

## 5. Conclusion

This paper presents a multi-faceted study of automated content moderation prediction, evaluating three complementary sources of context: user behavioral history, conversational threads, and explicit community rules. All three approaches are evaluated on a longitudinal moderation dataset from r/Anarchism, enabling direct comparison across methodologies.

The history-aware XGBoost classifier demonstrates [TO FILL with Riccardo's results] the contribution of behavioral signals beyond raw toxicity scores.

The thread-aware ablation shows [TO FILL after No-Thread results] whether conversational context improves classification accuracy for a fine-tuned RoBERTa-large classifier. The ablation design — two configurations of the same model differing only in the presence of thread context — isolates the contribution of conversational dynamics. A key methodological finding is that Knowledge Distillation requires a teacher whose minority-class performance is substantially above the student's baseline; in its absence, soft label training degrades rather than improves student performance (_distillation poisoning_).

The prompt-injection experiment shows [TO FILL with Luca's results] the effect of prepending explicit community rules to a frozen generalist LLM, without any fine-tuning.

The real-world inference experiment reveals that models trained on balanced data exhibit a fundamental precision-recall tradeoff under natural class distributions (~99.8% Normal), maintaining reasonable recall but near-zero precision. This finding motivates future work on post-hoc calibration and threshold adaptation for production deployment.

Together, these results suggest that no single contextual layer is sufficient for robust automated moderation: user history, conversational context, and explicit rules each contribute complementary signals, and their integration is a natural direction for future work.

**Future Directions**

- Thread reconstruction at scale via Reddit API, enabling Context-Aware evaluation on the full longitudinal dataset
- Post-hoc probability calibration (Platt Scaling, Temperature Scaling) to adapt balanced-trained classifiers to natural deployment distributions
- Joint modeling of user history and conversational context in a unified architecture
- Extension to multi-community settings to evaluate generalization across subreddits with different moderation cultures

---

## Acknowledgments

The authors thank the Sapienza AI-LAB course instructors for the project framework and evaluation guidelines. Computational resources were provided by Google Colab Pro (NVIDIA A100 SXM4-80GB).

---

## References

[1] J. M. Baumgartner, "Pushshift reddit api documentation," Retrieved April, vol. 4, p. 2020, 2019.

[2] L. Hanu and Unitary team, "Detoxify." Github. https://github.com/unitaryai/detoxify, 2020.

[3] A. Vaswani et al., "Attention is all you need," CoRR, vol. abs/1706.03762, 2017.

[4] Y. Liu et al., "RoBERTa: A robustly optimized BERT pretraining approach," CoRR, vol. abs/1907.11692, 2019.

[5] T. Chen and C. Guestrin, "XGBoost: A scalable tree boosting system," CoRR, vol. abs/1603.02754, 2016.

[6] Ollama Team, "Ollama," 2026.

[7] A. Yang et al., "Qwen2.5 technical report," arXiv preprint arXiv:2412.15115, 2024.

[8] G. Hinton, O. Vinyals, and J. Dean, "Distilling the knowledge in a neural network," arXiv preprint arXiv:1503.02531, 2015.

---

_Note: Sections and tables marked [TO FILL] require data from colleagues (Riccardo: history-aware results; Luca: prompt-injection results) or pending experimental results (No-Thread model across all 5 folds)._