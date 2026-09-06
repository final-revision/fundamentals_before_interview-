# About AI/ML — Interview Fundamentals

> A practical interview-preparation guide for an entry-level AI/ML Engineer.  
> Focus: fundamentals, common interview questions, short answers, and concepts you should be able to explain clearly.

---

## 1. AI, ML, Deep Learning, GenAI — The Big Picture

### Q1. What is Artificial Intelligence (AI)?
**Answer:** AI is the broader field of building systems that can perform tasks that normally require human intelligence, such as reasoning, perception, language understanding, decision-making, and learning.

### Q2. What is Machine Learning (ML)?
**Answer:** Machine Learning is a subset of AI where systems learn patterns from data and use those patterns to make predictions or decisions instead of being explicitly programmed for every rule.

### Q3. What is Deep Learning?
**Answer:** Deep Learning is a subset of ML that uses multi-layer neural networks to learn complex patterns, especially from large datasets such as images, audio, and text.

### Q4. What is Generative AI?
**Answer:** Generative AI refers to models that can generate new content such as text, images, audio, video, or code based on learned patterns.

### Q5. How are AI, ML, Deep Learning, and Generative AI related?

```text
Artificial Intelligence
│
└── Machine Learning
    │
    └── Deep Learning
        │
        ├── Computer Vision
        ├── NLP
        └── Many Generative AI models
```

**Important:** Generative AI is not simply a direct "child" of deep learning in every definition. Modern GenAI systems heavily use deep learning, but GenAI is better understood as an application/model family focused on generation.

---

# 2. Types of Machine Learning

### Q6. What are the main types of Machine Learning?

1. **Supervised Learning**
2. **Unsupervised Learning**
3. **Semi-Supervised Learning**
4. **Self-Supervised Learning**
5. **Reinforcement Learning**

### Q7. What is Supervised Learning?
The model learns from labeled data.

```text
Input X + Correct Output Y → Model → Prediction
```

Examples:
- Spam vs. not spam
- House price prediction
- Disease classification
- Image classification

Common algorithms:
- Linear Regression
- Logistic Regression
- Decision Tree
- Random Forest
- SVM
- KNN
- Neural Networks

### Q8. What is Unsupervised Learning?
The model receives data without target labels and tries to discover patterns or structure.

Examples:
- Customer segmentation
- Anomaly detection
- Dimensionality reduction

Common algorithms:
- K-Means
- DBSCAN
- Hierarchical Clustering
- PCA

### Q9. What is Reinforcement Learning?
An agent learns by interacting with an environment and receiving rewards or penalties.

```text
Agent → Action → Environment
  ↑                  ↓
  └──── Reward ──────┘
```

Examples:
- Game-playing agents
- Robotics
- Recommendation/decision systems

### Q10. What is Self-Supervised Learning?
The model creates learning signals from the data itself instead of requiring manually labeled examples.

Example:
- Predicting a missing word/token in text.

Modern large language models heavily rely on self-supervised learning during pretraining.

---

# 3. Basic ML Terminology

### Q11. What are features and labels?

- **Feature:** An input variable used by the model.
- **Label/Target:** The value the model is trying to predict.

Example:

| Age | Salary | Purchased |
|---:|---:|---|
| 22 | 30000 | No |
| 35 | 80000 | Yes |

`Age` and `Salary` are features. `Purchased` is the target.

### Q12. What is a dataset?
A dataset is a collection of observations/examples used for analysis or model training.

### Q13. What is a sample/observation?
One individual record in a dataset.

### Q14. What is a model?
A model is a mathematical/computational representation that learns patterns from data to make predictions or decisions.

### Q15. What are parameters and hyperparameters?

**Parameters**
- Learned from data.
- Example: weights in linear regression or neural networks.

**Hyperparameters**
- Set before/during training.
- Example: learning rate, tree depth, number of trees, batch size.

---

# 4. Train, Validation, and Test Data

### Q16. Why do we split data?

To measure whether the model generalizes to unseen data.

Typical split:

```text
Dataset
├── Training Set     → Learn parameters
├── Validation Set   → Tune/select model
└── Test Set         → Final unbiased evaluation
```

A common starting point might be 70/15/15 or 80/10/10, but there is no universal split.

### Q17. What is training data?
Data used to learn the model's parameters.

### Q18. What is validation data?
Data used during model development for hyperparameter tuning, model selection, threshold selection, and similar decisions.

### Q19. What is test data?
Data kept separate for final evaluation after development choices are complete.

### Q20. What is data leakage?
Data leakage occurs when information that should not be available to the model at prediction time influences training or evaluation.

**Example:** Using a patient's post-treatment information to predict whether they will need treatment.

**Why it is dangerous:** It can produce unrealistically high evaluation scores.

---

# 5. Regression vs Classification

### Q21. What is Regression?
Regression predicts a continuous numerical value.

Examples:
- House price
- Temperature
- Sales
- Salary

### Q22. What is Classification?
Classification predicts a category/class.

Examples:
- Spam / Not Spam
- Fraud / Not Fraud
- Cat / Dog
- Positive / Negative

### Q23. Binary vs Multiclass vs Multilabel classification

**Binary:** Two classes  
Example: Fraud / Not Fraud

**Multiclass:** One of many classes  
Example: Cat / Dog / Horse

**Multilabel:** Multiple labels can be true simultaneously  
Example: An image can contain `car`, `road`, and `person`.

---

# 6. Linear Regression

### Q24. What is Linear Regression?
A supervised learning algorithm used to predict a continuous value by modeling a relationship between input features and a target.

Simple form:

```text
y = mx + b
```

Multiple linear regression:

```text
y = b0 + b1x1 + b2x2 + ... + bnxn
```

### Q25. What is the purpose of the loss function in regression?
It measures how different predictions are from actual values.

A common loss is **Mean Squared Error (MSE)**:

```text
MSE = (1/n) Σ(y - ŷ)²
```

### Q26. What is R²?
R² measures the proportion of variance in the target explained by the model relative to a baseline mean predictor.

Important:
- Higher is generally better for comparable evaluation settings.
- It can be negative on unseen data.
- It should not be used alone.

---

# 7. Logistic Regression

### Q27. Is Logistic Regression a regression or classification algorithm?
Despite its name, Logistic Regression is primarily used for classification, especially binary classification.

It produces a probability using the sigmoid function:

```text
σ(z) = 1 / (1 + e^-z)
```

The probability can then be converted into a class using a decision threshold.

### Q28. What is the sigmoid function?
It maps a real-valued number into the range `(0, 1)`.

---

# 8. Decision Trees

### Q29. What is a Decision Tree?
A tree-based model that makes predictions by repeatedly splitting data using feature-based rules.

```text
             Age > 30?
             /       \
           Yes        No
           /           \
       High income    Low income
```

### Q30. What is Gini impurity?
A measure of how mixed the classes are in a node.

```text
Gini = 1 - Σ pᵢ²
```

Lower impurity means a purer node.

### Q31. What is entropy?
Entropy measures uncertainty/impurity in a node.

```text
H = -Σ pᵢ log₂(pᵢ)
```

Decision-tree algorithms can choose splits based on information gain or related criteria.

### Q32. What is pruning?
Pruning reduces unnecessary tree branches to improve generalization and reduce overfitting.

---

# 9. Random Forest

### Q33. What is Random Forest?
Random Forest is an ensemble of decision trees. Each tree is trained using randomness in samples and/or features, and their predictions are combined.

### Q34. Why is Random Forest better than one Decision Tree in many cases?
A single tree can have high variance and overfit. Combining many diverse trees generally makes predictions more stable.

### Q35. What is ensemble learning?
Ensemble learning combines multiple models to produce a stronger overall model.

Major approaches:
- Bagging
- Boosting
- Stacking

---

# 10. Overfitting and Underfitting

### Q36. What is Overfitting?
The model learns the training data too closely, including noise, and performs poorly on unseen data.

```text
Training performance → Very high
Test performance     → Poor
```

### Q37. What is Underfitting?
The model is too simple to capture important patterns.

```text
Training performance → Poor
Test performance     → Poor
```

### Q38. How can you reduce overfitting?

Common approaches:
- More representative training data
- Regularization
- Cross-validation
- Feature selection
- Data augmentation
- Early stopping
- Dropout
- Simpler models
- Tree pruning
- Ensembling

---

# 11. Bias and Variance

### Q39. What is Bias?
Bias is error caused by overly simplistic assumptions in a model.

High bias often leads to underfitting.

### Q40. What is Variance?
Variance is sensitivity to the particular training dataset.

High variance often leads to overfitting.

### Q41. Explain the Bias-Variance Tradeoff.
Increasing model complexity can reduce bias but may increase variance. The goal is to find a model complexity that generalizes well.

```text
Too simple ←──── Good generalization ────→ Too complex
High Bias                         High Variance
```

---

# 12. Cross-Validation

### Q42. What is Cross-Validation?
A method for estimating model performance by training and evaluating across multiple splits of the training data.

### Q43. What is K-Fold Cross-Validation?

The dataset is divided into K folds.

```text
Fold 1 | Fold 2 | Fold 3 | Fold 4 | Fold 5

Run 1: Test on Fold 1
Run 2: Test on Fold 2
Run 3: Test on Fold 3
Run 4: Test on Fold 4
Run 5: Test on Fold 5
```

The results are then aggregated.

### Q44. Why use cross-validation?
It gives a more robust estimate of generalization than relying on a single train/validation split.

**Important:** For time-series data, ordinary random K-fold splitting can be inappropriate because it may violate temporal ordering.

---

# 13. Feature Engineering

### Q45. What is Feature Engineering?
Creating, transforming, or selecting useful input features to improve model performance.

Examples:
- Extracting day/month from a date
- Creating age from date of birth
- Log-transforming skewed values
- Creating interaction features

### Q46. What is Feature Selection?
Selecting the most useful features while removing irrelevant or redundant ones.

Benefits:
- Less noise
- Faster training
- Simpler models
- Sometimes better generalization

### Q47. What is dimensionality reduction?
Reducing the number of input dimensions while preserving useful information.

Example:
- PCA
- Autoencoders

---

# 14. Data Preprocessing

### Q48. Why is preprocessing important?
Raw data may contain:
- Missing values
- Outliers
- Duplicate records
- Incorrect formats
- Categorical values
- Different feature scales

Preprocessing makes data suitable for modeling.

### Q49. What is normalization?
Normalization commonly rescales values to a bounded range such as `[0, 1]`.

```text
x' = (x - min(x)) / (max(x) - min(x))
```

### Q50. What is standardization?
Standardization transforms a feature to approximately zero mean and unit variance.

```text
z = (x - μ) / σ
```

### Q51. Normalization vs Standardization

**Normalization**
- Often maps to a fixed range.
- Useful for certain algorithms and neural-network inputs.

**Standardization**
- Centers around zero and scales by standard deviation.
- Commonly useful for linear models, SVM, KNN, and neural networks.

Tree-based models usually do not require feature scaling.

---

# 15. Categorical Data

### Q52. How do you convert categorical variables into numbers?

Common techniques:
- One-Hot Encoding
- Ordinal Encoding
- Target Encoding
- Embeddings

### Q53. What is One-Hot Encoding?
It creates separate binary columns for categories.

```text
Color
Red
Blue
Green

→
Red  Blue  Green
1     0      0
0     1      0
0     0      1
```

### Q54. When can one-hot encoding become problematic?
When a categorical feature has very high cardinality, it can create a huge sparse feature matrix.

---

# 16. Missing Values

### Q55. How can you handle missing data?

Options:
- Remove rows
- Remove columns
- Mean/median/mode imputation
- Model-based imputation
- KNN imputation
- Add a missing-indicator feature

The correct approach depends on why values are missing and the modeling problem.

### Q56. Mean vs Median Imputation
Median is generally more robust to extreme outliers than mean.

---

# 17. Outliers

### Q57. What is an outlier?
An observation that is unusually far from the typical values in the dataset.

### Q58. How can you detect outliers?
Common approaches:
- IQR method
- Z-score
- Visualization
- Domain-specific rules
- Isolation Forest

### Q59. Should every outlier be removed?
No. An outlier can be:
- A data error
- A legitimate rare event
- The signal you are actually trying to detect

---

# 18. Classification Metrics

### Q60. What is a Confusion Matrix?

For binary classification:

| | Predicted Positive | Predicted Negative |
|---|---:|---:|
| Actual Positive | TP | FN |
| Actual Negative | FP | TN |

### Q61. What is Accuracy?

```text
Accuracy = (TP + TN) / (TP + TN + FP + FN)
```

It is the fraction of predictions that are correct.

### Q62. What is Precision?

```text
Precision = TP / (TP + FP)
```

Of the cases predicted positive, how many were actually positive?

### Q63. What is Recall?

```text
Recall = TP / (TP + FN)
```

Of the actual positive cases, how many did the model identify?

### Q64. What is F1 Score?

```text
F1 = 2 × Precision × Recall / (Precision + Recall)
```

It is the harmonic mean of precision and recall.

### Q65. Precision vs Recall — when do you care about each?

**High precision:** False positives are costly.  
Example: A system where wrongly flagging a legitimate transaction is expensive.

**High recall:** False negatives are costly.  
Example: Screening for a serious condition where missing a true case is costly.

### Q66. What is a good metric for imbalanced data?
There is no single universal answer. Accuracy can be misleading. Depending on the objective, consider:
- Precision
- Recall
- F1
- PR-AUC
- ROC-AUC
- Class-specific metrics
- Cost-based metrics

---

# 19. ROC-AUC and PR-AUC

### Q67. What is ROC-AUC?
ROC-AUC summarizes the model's ability to rank positive examples above negative examples across classification thresholds.

### Q68. What is PR-AUC?
Precision-Recall AUC summarizes the precision-recall tradeoff across thresholds.

**Important:** For heavily imbalanced positive classes, PR-AUC can be more informative than ROC-AUC.

---

# 20. Loss Functions

### Q69. What is a Loss Function?
A loss function measures how wrong a model's prediction is for training purposes.

The optimizer tries to minimize the loss.

### Q70. Common loss functions

**Regression**
- MSE
- MAE
- Huber Loss

**Binary classification**
- Binary Cross-Entropy / Log Loss

**Multiclass classification**
- Categorical Cross-Entropy

---

# 21. Optimization

### Q71. What is Gradient Descent?
An optimization algorithm that updates model parameters in the direction that reduces the loss.

Conceptually:

```text
Parameter ← Parameter - Learning Rate × Gradient
```

### Q72. What is a Gradient?
The gradient indicates the direction and rate of greatest increase of a function with respect to its parameters.

### Q73. What is Learning Rate?
The learning rate controls how large each optimization update is.

Too high:
- Training may become unstable or overshoot.

Too low:
- Training can be very slow.

### Q74. What is an Epoch?
One complete pass through the training dataset.

### Q75. What is Batch Size?
The number of training examples processed before one parameter update.

### Q76. Batch vs Mini-Batch vs Stochastic Gradient Descent

- **Batch GD:** Uses the entire dataset for one update.
- **Mini-batch GD:** Uses a small batch for each update.
- **SGD:** Uses one example per update.

In practice, mini-batch training is very common.

---

# 22. Regularization

### Q77. What is Regularization?
A technique that discourages overly complex models to improve generalization.

### Q78. L1 vs L2 Regularization

**L1**
```text
Loss + λΣ|w|
```

Can drive some weights exactly to zero, which can perform feature selection.

**L2**
```text
Loss + λΣw²
```

Encourages weights to be small.

### Q79. What is Elastic Net?
Elastic Net combines L1 and L2 regularization.

---

# 23. Neural Networks

### Q80. What is a Neural Network?
A machine learning model composed of interconnected computational units (neurons) organized into layers.

```text
Input Layer → Hidden Layers → Output Layer
```

### Q81. What is a neuron?
A neuron computes a weighted combination of inputs, adds a bias, and applies an activation function.

```text
z = w₁x₁ + w₂x₂ + ... + b
output = activation(z)
```

### Q82. What are weights and biases?
- **Weights:** Control the contribution of inputs.
- **Bias:** Allows the neuron to shift its activation.

### Q83. What is an activation function?
A nonlinear function applied to a neuron's output.

Common functions:
- ReLU
- Sigmoid
- Tanh
- Softmax

### Q84. Why do neural networks need nonlinear activation functions?
Without nonlinear activations, stacking linear layers still results in an overall linear transformation, limiting what the network can learn.

### Q85. What is ReLU?

```text
ReLU(x) = max(0, x)
```

It is widely used in hidden layers.

### Q86. What is Softmax?
Softmax converts logits into a probability distribution across multiple classes.

```text
P(i) = exp(zᵢ) / Σ exp(zⱼ)
```

---

# 24. Forward and Backpropagation

### Q87. What is Forward Propagation?
The process of passing input through the network to calculate predictions.

### Q88. What is Backpropagation?
The process of calculating gradients of the loss with respect to model parameters by applying the chain rule backward through the network.

### Q89. How are neural-network weights updated?

```text
Input
  ↓
Forward Pass
  ↓
Prediction
  ↓
Loss
  ↓
Backpropagation
  ↓
Gradients
  ↓
Optimizer
  ↓
Updated Weights
```

---

# 25. Deep Learning Basics

### Q90. What is CNN?
A Convolutional Neural Network is a neural architecture especially useful for spatial data such as images.

Common applications:
- Image classification
- Object detection
- Segmentation

### Q91. What is RNN?
A Recurrent Neural Network processes sequential data while maintaining a hidden state.

Applications historically include:
- Text
- Time series
- Speech

### Q92. What are LSTM and GRU?
They are gated recurrent architectures designed to better handle long-term dependencies than basic RNNs.

### Q93. What is a Transformer?
A neural-network architecture based primarily on attention mechanisms. Transformers became foundational for modern NLP and many multimodal/generative AI systems.

---

# 26. NLP Fundamentals

### Q94. What is NLP?
Natural Language Processing is the field of AI concerned with processing and understanding human language.

Applications:
- Chatbots
- Translation
- Sentiment analysis
- Information extraction
- Search
- Text classification

### Q95. What is Tokenization?
Breaking text into tokens that a model can process.

A token may be:
- A word
- A subword
- A character
- Another vocabulary-defined unit

### Q96. What is an Embedding?
An embedding is a dense numerical vector representation of an object such as a word, sentence, document, image, or user.

Similar meanings often have vectors that are close under an appropriate similarity measure.

### Q97. What is Cosine Similarity?

```text
cos(θ) = (A · B) / (||A|| ||B||)
```

It measures the angle-based similarity between vectors and is widely used with embeddings.

---

# 27. LLM Fundamentals

### Q98. What is an LLM?
A Large Language Model is a neural language model trained on large amounts of text to learn patterns in language and perform tasks such as generation, summarization, question answering, and transformation.

### Q99. What is a Transformer in LLMs?
Transformers use attention to model relationships between tokens and process sequences efficiently in parallel during training.

### Q100. What is Attention?
Attention lets a model assign different importance to different tokens when computing a representation.

### Q101. What is Self-Attention?
Self-attention allows tokens in the same sequence to attend to one another.

### Q102. What are Query, Key, and Value?
In scaled dot-product attention:

```text
Attention(Q,K,V) = softmax(QKᵀ / √dₖ)V
```

- **Query:** What information am I looking for?
- **Key:** What information does each token offer for matching?
- **Value:** What content is retrieved/combined?

### Q103. What is a Context Window?
The maximum amount of token context a model can process in one input/output interaction, according to that model's architecture and product limits.

### Q104. What is Hallucination?
When a generative model produces information that is incorrect, unsupported, or fabricated while presenting it as if it were reliable.

Common mitigation strategies:
- Retrieval grounding
- Tool use
- Better prompts
- Structured outputs
- Verification
- Human review
- Fine-tuning where appropriate

---

# 28. RAG Fundamentals

### Q105. What is RAG?
RAG stands for **Retrieval-Augmented Generation**.

It combines retrieval of relevant external information with generation by an LLM.

```text
User Question
     ↓
Retriever
     ↓
Relevant Documents
     ↓
Context + Question
     ↓
LLM
     ↓
Answer
```

### Q106. Why use RAG?
RAG can:
- Ground answers in external knowledge
- Use private/company documents
- Improve factuality for knowledge-intensive tasks
- Avoid retraining the model every time documents change

### Q107. Basic RAG pipeline

```text
Documents
   ↓
Chunking
   ↓
Embeddings
   ↓
Vector Database
   ↓
User Query
   ↓
Query Embedding
   ↓
Similarity Search
   ↓
Retrieved Chunks
   ↓
Prompt + Context
   ↓
LLM
   ↓
Answer
```

### Q108. RAG vs Fine-Tuning

**RAG**
- Supplies external information at inference time.
- Good when knowledge changes frequently.
- Can provide source documents.

**Fine-Tuning**
- Changes model behavior/parameters through additional training.
- Useful for style, task behavior, or domain adaptation.
- Does not automatically make a model a reliable database of current facts.

---

# 29. Vector Databases

### Q109. What is a Vector Database?
A system designed to store and search vector representations efficiently.

Examples of use:
- Semantic search
- RAG
- Recommendation
- Similarity search

### Q110. What is a vector embedding?
A numerical representation of data in a continuous vector space.

### Q111. What is semantic search?
Search based on meaning/similarity rather than requiring exact keyword matches.

---

# 30. AI Agents

### Q112. What is an AI Agent?
An AI agent is a system that can use a model plus tools, memory/state, and control logic to perform tasks toward a goal.

Typical components:

```text
User Goal
   ↓
Agent / LLM
   ├── Reasoning / Planning
   ├── Tools
   ├── Memory / State
   └── Observations
   ↓
Action
```

### Q113. AI Agent vs Chatbot
A basic chatbot mainly responds to messages.

An agent may:
- Decide what actions to take
- Call tools/APIs
- Retrieve information
- Execute multi-step workflows
- Observe results and continue

### Q114. RAG vs AI Agent
**RAG** is primarily a retrieval-and-generation pattern.

**Agent** is a broader system pattern involving decision-making and actions, potentially including RAG as one of its tools/components.

---

# 31. Model Evaluation

### Q115. Why is model evaluation important?
A model can perform well on training data while failing in production. Evaluation estimates generalization and checks whether the model meets the actual business objective.

### Q116. What is a baseline model?
A simple reference approach used to compare whether a more complex model actually provides meaningful improvement.

### Q117. What is a benchmark?
A standardized dataset, task, or evaluation setup used to compare model performance.

### Q118. What is data drift?
A change in the distribution of input data over time.

Example:
A fraud model was trained on customer behavior from 2024, but user behavior changes significantly in 2026.

### Q119. What is concept drift?
A change in the relationship between inputs and the target over time.

Example:
The meaning of patterns associated with fraud changes.

---

# 32. Imbalanced Datasets

### Q120. What is class imbalance?
When some classes have substantially more examples than others.

Example:

```text
99% Normal
1% Fraud
```

A model predicting "Normal" every time would have 99% accuracy but be useless for fraud detection.

### Q121. How can you handle class imbalance?

Options:
- Class weights
- Oversampling
- Undersampling
- SMOTE
- Threshold tuning
- Appropriate evaluation metrics

---

# 33. Data Science vs ML Engineering vs AI Engineering

### Q122. What does a Data Scientist do?
Typically focuses on:
- Data analysis
- Experimentation
- Statistical modeling
- Predictive modeling
- Business insights

### Q123. What does an ML Engineer do?
Typically focuses on:
- Building ML pipelines
- Training models
- Model serving
- Deployment
- Monitoring
- Scaling
- Reliability

### Q124. What does an AI Engineer do?
The role varies by organization, but commonly involves integrating AI/ML models into real applications.

Possible areas:
- LLM applications
- RAG
- AI agents
- Model APIs
- Prompting
- Evaluation
- Vector search
- AI application backend
- Deployment and monitoring

---

# 34. MLOps Fundamentals

### Q125. What is MLOps?
MLOps applies software engineering and operational practices to the lifecycle of ML systems.

Typical areas:
- Data pipelines
- Training
- Experiment tracking
- Model versioning
- Deployment
- Monitoring
- Retraining

### Q126. What is Model Deployment?
Making a trained model available for real-world inference.

Common approaches:
- REST API
- gRPC
- Batch inference
- Embedded/on-device inference

### Q127. What is Model Serving?
Running a model in a system that accepts inputs and returns predictions.

### Q128. What is Model Monitoring?
Monitoring production behavior such as:
- Latency
- Error rate
- Input drift
- Output quality
- Resource usage
- Business metrics

---

# 35. Python Fundamentals for AI/ML Interviews

### Q129. Why is Python popular in AI/ML?
Because it has:
- Simple syntax
- Large ecosystem
- Strong data-science libraries
- Excellent ML/DL frameworks
- Large community

Important libraries:
- NumPy
- pandas
- Matplotlib
- scikit-learn
- PyTorch
- TensorFlow
- Hugging Face Transformers

### Q130. NumPy vs pandas

**NumPy**
- Numerical arrays
- Vectorized numerical computation

**pandas**
- Tabular data
- Data cleaning
- Data manipulation
- Data analysis

### Q131. What is vectorization?
Performing operations on arrays/tensors using optimized numerical operations instead of explicit Python loops where appropriate.

---

# 36. Common ML Algorithms — Quick Revision

| Algorithm | Main Use | Learning Type |
|---|---|---|
| Linear Regression | Continuous prediction | Supervised |
| Logistic Regression | Classification | Supervised |
| KNN | Classification/Regression | Supervised |
| Decision Tree | Classification/Regression | Supervised |
| Random Forest | Classification/Regression | Supervised |
| SVM | Classification/Regression | Supervised |
| K-Means | Clustering | Unsupervised |
| DBSCAN | Clustering | Unsupervised |
| PCA | Dimensionality reduction | Unsupervised |
| Neural Network | Complex prediction/generation | Supervised/Self-supervised/etc. |
| CNN | Images/spatial data | Deep Learning |
| RNN/LSTM/GRU | Sequential data | Deep Learning |
| Transformer | Language/multimodal/sequential tasks | Deep Learning |

---

# 37. Interview Scenario Questions

### Q132. Your model has 99% accuracy. Is it a good model?
**Answer:** Not necessarily. If the dataset is highly imbalanced, accuracy can hide poor minority-class performance. I would inspect the confusion matrix, precision, recall, F1, PR-AUC, and the business cost of errors.

### Q133. Training accuracy is 99% but test accuracy is 70%. What could be happening?
**Answer:** The model may be overfitting. I would investigate data leakage, train/test distribution differences, model complexity, regularization, feature quality, and validation methodology.

### Q134. Your model performs well offline but poorly in production. Why?
Possible causes:
- Data drift
- Training-serving skew
- Data leakage in offline evaluation
- Different preprocessing
- Distribution shift
- Poor production data quality
- Latency/resource constraints
- Metric mismatch with the real objective

### Q135. Your dataset contains missing values. What would you do?
**Answer:** First understand why values are missing and how much is missing. Then choose an appropriate strategy such as removal, imputation, missing indicators, or a model that can handle missingness. The preprocessing must be fitted only on training data when applicable.

### Q136. How would you choose between two ML models?
Consider:
1. Problem requirements
2. Baseline performance
3. Validation metrics
4. Generalization
5. Interpretability
6. Latency
7. Memory/compute cost
8. Data size
9. Maintenance complexity
10. Business impact

### Q137. How would you improve a poorly performing ML model?
A strong interview answer:

```text
1. Verify the problem and target definition
2. Check data quality
3. Establish a baseline
4. Analyze errors
5. Check leakage and train/test split
6. Improve features/data
7. Tune hyperparameters
8. Try suitable models
9. Evaluate using the right metrics
10. Test on realistic unseen data
11. Deploy carefully
12. Monitor in production
```

---

# 38. Important "Explain in One Sentence" Questions

Be able to answer these quickly:

- **AI:** Machines performing tasks associated with intelligence.
- **ML:** Learning patterns from data to make predictions/decisions.
- **Deep Learning:** ML using multi-layer neural networks.
- **Generative AI:** AI systems that generate new content.
- **Feature:** Input variable.
- **Label:** Target/output to predict.
- **Overfitting:** Good training performance but poor generalization.
- **Underfitting:** Model is too simple to capture important patterns.
- **Regularization:** Penalizing complexity to improve generalization.
- **Epoch:** One pass through the training dataset.
- **Batch:** Number of examples processed per update.
- **Learning Rate:** Step size of parameter updates.
- **Gradient Descent:** Optimization method that moves parameters to reduce loss.
- **Embedding:** Dense vector representation.
- **Token:** Unit processed by a language model.
- **Transformer:** Attention-based neural architecture.
- **RAG:** Retrieval + generation.
- **Vector DB:** Database optimized for vector similarity search.
- **Agent:** AI system that can use tools/state to take actions toward a goal.
- **MLOps:** Engineering practices for reliable ML lifecycle management.

---

# 39. Most Important Formulas to Remember

### Linear Regression

```text
y = b0 + b1x1 + ... + bnxn
```

### MSE

```text
MSE = (1/n) Σ(y - ŷ)²
```

### MAE

```text
MAE = (1/n) Σ|y - ŷ|
```

### Sigmoid

```text
σ(x) = 1 / (1 + e^-x)
```

### Accuracy

```text
(TP + TN) / (TP + TN + FP + FN)
```

### Precision

```text
TP / (TP + FP)
```

### Recall

```text
TP / (TP + FN)
```

### F1

```text
2 × Precision × Recall / (Precision + Recall)
```

### Standardization

```text
z = (x - μ) / σ
```

### Min-Max Normalization

```text
x' = (x - min(x)) / (max(x) - min(x))
```

### Attention

```text
Attention(Q,K,V) = softmax(QKᵀ / √dₖ)V
```

---

# 40. Interview Preparation Priority

If you have limited time, learn in this order:

## Level 1 — Must Know

- AI vs ML vs Deep Learning
- Supervised vs Unsupervised Learning
- Classification vs Regression
- Features and labels
- Train/validation/test split
- Overfitting vs Underfitting
- Bias vs Variance
- Data leakage
- Linear Regression
- Logistic Regression
- Decision Trees
- Random Forest
- Accuracy, Precision, Recall, F1
- Confusion Matrix
- Cross-validation
- Feature engineering
- Missing values
- Scaling
- Basic Python
- NumPy
- pandas
- scikit-learn

## Level 2 — Strong ML Foundation

- Gradient Descent
- Loss functions
- Regularization
- Hyperparameter tuning
- ROC-AUC / PR-AUC
- Class imbalance
- PCA
- Clustering
- SVM
- KNN
- Ensemble learning
- Model evaluation
- Data drift
- MLOps basics

## Level 3 — AI Engineer Foundation

- Neural Networks
- Backpropagation
- CNN
- RNN/LSTM/GRU
- Transformers
- Tokenization
- Embeddings
- Attention
- LLMs
- Prompting
- RAG
- Vector databases
- AI Agents
- Tool calling
- Evaluation
- Model serving
- Monitoring

---

# 41. Final Interview Rule

For almost every AI/ML interview question, try to answer using this structure:

```text
1. Definition
2. How it works
3. Simple example
4. When to use it
5. Limitation / tradeoff
```

Example:

**Question:** What is Random Forest?

**Strong answer:**

> Random Forest is an ensemble machine-learning algorithm that combines multiple decision trees. Each tree is trained with randomness in the training samples and/or feature selection, and their predictions are aggregated. It is useful for classification and regression and often generalizes better than a single decision tree. Its tradeoffs include reduced interpretability compared with a single tree and potentially higher computational cost.

---

# 42. Quick Self-Test

Before an AI/ML interview, make sure you can explain these without memorizing definitions:

- [ ] AI vs ML vs DL vs GenAI
- [ ] Supervised vs unsupervised learning
- [ ] Regression vs classification
- [ ] Train vs validation vs test
- [ ] Data leakage
- [ ] Overfitting and underfitting
- [ ] Bias and variance
- [ ] Linear regression
- [ ] Logistic regression
- [ ] Decision tree
- [ ] Random forest
- [ ] K-Means
- [ ] PCA
- [ ] Confusion matrix
- [ ] Precision vs recall
- [ ] F1 score
- [ ] ROC-AUC vs PR-AUC
- [ ] Cross-validation
- [ ] Feature engineering
- [ ] Normalization vs standardization
- [ ] Missing-value handling
- [ ] Gradient descent
- [ ] Learning rate
- [ ] Loss function
- [ ] Regularization
- [ ] Neural networks
- [ ] Backpropagation
- [ ] CNN
- [ ] Transformers
- [ ] Tokenization
- [ ] Embeddings
- [ ] Attention
- [ ] LLM
- [ ] RAG
- [ ] Vector database
- [ ] AI agents
- [ ] MLOps
- [ ] Model deployment
- [ ] Model monitoring

---

## Bottom Line

For an **AI/ML Engineer interview**, do not focus only on memorizing algorithm definitions. Be prepared to explain:

> **What the technique is → why it works → when to use it → what can go wrong → how you would evaluate it.**

That style of explanation demonstrates actual engineering understanding rather than memorization.
