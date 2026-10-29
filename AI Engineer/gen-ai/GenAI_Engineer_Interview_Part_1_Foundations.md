# GenAI Engineer Interview Preparation — Part 1: Foundations

**Level:** Beginner to intermediate, aimed at a GenAI internship interview  
**Target:** Technical interview preparation for a Generative AI Engineer role  
**How to use:** First understand the concept, then practise answering aloud in your own words. Answers are interview-ready starting points, not scripts to memorise.

---

## Table of Contents

1. What a GenAI Engineer does
2. AI, ML, deep learning, NLP and generative AI
3. Core machine-learning foundations
4. Neural networks and deep learning
5. NLP foundations and text processing
6. Transformers and attention
7. Large language models (LLMs)
8. Tokens, embeddings and vector similarity
9. Prompt engineering
10. Inference, decoding and model parameters
11. Hallucinations, limitations and responsible AI
12. Python and essential technical coding questions
13. API and software engineering foundations for GenAI
14. Common interview scenarios
15. Rapid-fire revision questions
16. Practice interview checklist
17. Glossary

---

# 1. What Does a GenAI Engineer Do?

A **Generative AI (GenAI) Engineer** builds software that uses generative models to create or transform content such as text, code, images, audio or structured data. The role involves more than writing prompts: it can include selecting models, preparing data, integrating APIs, designing retrieval systems, evaluating output quality, controlling latency and cost, and deploying reliable applications.

Typical responsibilities include:

- Understanding a business problem and deciding whether an LLM is appropriate.
- Integrating hosted models or running open-weight models.
- Writing and testing prompts and structured output schemas.
- Building retrieval-augmented generation (RAG) systems over documents.
- Working with embeddings and vector databases.
- Evaluating factuality, relevance, safety, latency and cost.
- Building backend APIs, logging, monitoring and access controls.
- Reducing hallucinations and protecting sensitive data.
- Collaborating with product, data and software engineering teams.

### Q1. What is Generative AI?

**Answer:** Generative AI is a class of AI that learns patterns and structure from training data and uses those learned patterns to generate new content, such as text, images, audio, video or code. A text LLM, for example, generates a response by predicting tokens based on the context it receives. It does not simply retrieve a memorised answer for every prompt.

**Follow-up:** Is every AI system generative?

No. A spam classifier, fraud detector or model that predicts house prices is usually discriminative or predictive. It estimates a class, score or value rather than generating open-ended content.

### Q2. What is the difference between a GenAI Engineer and a traditional ML Engineer?

**Answer:** Both need data, evaluation, deployment and software engineering skills. A traditional ML Engineer may focus on feature engineering, training and serving models for classification, regression or ranking. A GenAI Engineer commonly works with pretrained foundation models, prompts, tokenisation, embeddings, retrieval, tool calling, generated output evaluation and LLM-specific risks. The roles overlap substantially.

### Q3. Do I need to train an LLM from scratch to be a GenAI Engineer?

**Answer:** No. Most practical applications use a pretrained model through an API or deploy an existing open-weight model. The engineer adapts the system using prompting, retrieval, tools, structured outputs, fine-tuning when justified, and evaluation. Training a foundation model from scratch requires extensive data, compute, expertise and funding.

### Q4. What are the main parts of a production GenAI application?

**Answer:**
1. User interface or client.
2. Backend/API layer.
3. Input validation, authentication and authorisation.
4. Prompt/context construction.
5. Model provider or inference server.
6. Optional retrieval, tools or business logic.
7. Output parsing and validation.
8. Safety checks, logging, evaluation and monitoring.

A production system must handle errors, timeouts, rate limits, sensitive data and cost—not just return a response in a demo.

---

# 2. AI, ML, Deep Learning, NLP and GenAI

## 2.1 The relationship

- **Artificial Intelligence (AI):** The broad field of building systems that perform tasks associated with intelligent behaviour.
- **Machine Learning (ML):** A subset of AI in which systems learn patterns from data rather than relying only on manually written rules.
- **Deep Learning (DL):** A subset of ML using neural networks with multiple layers.
- **Natural Language Processing (NLP):** The field concerned with processing, understanding and generating human language.
- **Generative AI:** Methods that generate new content. Modern GenAI often uses deep learning, including transformers and diffusion models.
- **Large Language Model (LLM):** A language model trained at large scale, usually on substantial text/code data, that predicts or generates token sequences.

These categories overlap; they are not all mutually exclusive.

### Q5. Explain AI vs ML vs DL vs GenAI.

**Answer:** AI is the broad umbrella. ML learns from examples. Deep learning uses multilayer neural networks to learn complex representations. Generative AI creates content, often using deep-learning models. For example, an LLM chatbot is an AI application that uses deep learning and NLP techniques to generate text.

### Q6. What is the difference between discriminative and generative models?

**Answer:** A discriminative model learns to distinguish labels or estimate a target, often modelling \(P(y\mid x)\). A generative model learns a data distribution or a process for producing examples, such as \(P(x)\) or \(P(x,y)\), depending on the formulation.

**Examples:**
- Discriminative: classify an email as spam or not spam.
- Generative: draft a new email from instructions.
- Important nuance: a generative model can also be used for classification, and not every generative model works in the same way.

### Q7. What is supervised learning?

**Answer:** Supervised learning uses labelled examples. Each training example contains input features and a target label/value. The model learns a mapping from inputs to targets.

Examples: predicting house prices (regression) and classifying product reviews as positive or negative (classification).

### Q8. What is unsupervised learning?

**Answer:** Unsupervised learning looks for structure in data without explicit target labels. Clustering, dimensionality reduction and some representation-learning approaches are examples. Self-supervised learning, widely used to train LLMs, creates learning targets from the data itself and is related but not identical to traditional unsupervised learning.

### Q9. What is self-supervised learning, and why is it important for LLMs?

**Answer:** Self-supervised learning creates training targets from the input data. In next-token prediction, for example, the model sees a token sequence and learns to predict the next token. Large collections of text can therefore provide many training examples without a human manually labelling each next token.

### Q10. Explain classification vs regression.

**Answer:** Classification predicts a category, such as spam/not spam. Regression predicts a continuous value, such as expected delivery time. The task determines the output layer, loss function and evaluation metrics.

### Q11. What are training, validation and test datasets?

**Answer:**
- **Training set:** Used to update model parameters.
- **Validation set:** Used for model selection and tuning.
- **Test set:** Used for final, relatively unbiased evaluation after choices are made.

The same examples should not leak across splits in ways that inflate performance. In LLM evaluation, near-duplicate documents and benchmark contamination can also make scores misleading.

### Q12. What is overfitting? How can it be reduced?

**Answer:** Overfitting happens when a model fits training data too closely and performs poorly on unseen data. Ways to reduce it include more representative data, regularisation, dropout, early stopping, data augmentation, simpler models and sound validation. For LLM applications, leakage, memorisation and overfitting during fine-tuning are related concerns.

### Q13. Explain bias and variance.

**Answer:** Bias is error from assumptions that are too restrictive; variance is sensitivity to fluctuations in the training data. High bias can lead to underfitting, while high variance can lead to overfitting. The goal is to generalise well rather than minimise training error alone.

### Q14. What is data leakage?

**Answer:** Data leakage occurs when training or model selection uses information that would not legitimately be available at prediction time. For example, including a post-outcome field in a fraud model can produce unrealistically high test performance. In RAG evaluation, placing test answers in the indexed corpus can also invalidate an evaluation if the test is supposed to measure retrieval from unseen sources.

---

# 3. Core Machine-Learning Foundations

## 3.1 Loss, optimisation and gradients

A **loss function** measures how far predictions are from desired targets. An **optimiser** updates model parameters to reduce the loss. A **gradient** indicates how the loss changes with respect to parameters.

### Q15. What is a loss function?

**Answer:** A loss function gives a numerical measure of prediction error for a training example or batch. The model is trained to minimise an objective built from this loss, possibly with regularisation terms. Cross-entropy is common for classification and language-model token prediction; mean squared error is common for regression.

### Q16. What is gradient descent?

**Answer:** Gradient descent updates parameters in the direction that reduces the loss, using the negative gradient. In simplified form:

\[
\theta_{t+1}=\theta_t-\eta\nabla_\theta L(\theta_t)
\]

Here, \(\theta\) represents parameters, \(L\) is the loss, and \(\eta\) is the learning rate.

### Q17. What is the learning rate?

**Answer:** The learning rate controls the size of parameter updates. If it is too large, training can oscillate or diverge; if too small, learning can be very slow or stall. Learning-rate schedules and warm-up are commonly used in deep learning.

### Q18. What is an epoch, batch and iteration?

**Answer:**
- **Epoch:** One complete pass through the training dataset.
- **Batch:** The examples processed together for a training step.
- **Iteration/step:** Usually one parameter update, often after processing one batch.

If there are 1,000 training examples and a batch size of 100, one epoch contains approximately 10 steps, assuming all examples are used and the final batch is handled normally.

### Q19. What is cross-entropy loss?

**Answer:** Cross-entropy measures how well a predicted probability distribution matches the target distribution. For a one-hot target, it penalises the model when it assigns low probability to the correct class. In next-token training, the target is the actual next token and the model learns to assign it high probability.

### Q20. What is regularisation?

**Answer:** Regularisation discourages overly complex or unstable solutions and can improve generalisation. Examples include L1/L2 penalties, dropout and early stopping. Weight decay is often used with optimisers such as AdamW.

### Q21. What is precision, recall and F1-score?

**Answer:**
- Precision = TP / (TP + FP): among predicted positives, how many are correct?
- Recall = TP / (TP + FN): among actual positives, how many were found?
- F1 = harmonic mean of precision and recall.

For a retrieval system, precision at \(k\) can describe how many of the top-\(k\) retrieved chunks are relevant; recall at \(k\) can describe how much of the relevant material was retrieved. These definitions depend on the evaluation setup.

### Q22. Why is accuracy not always a good metric?

**Answer:** Accuracy can hide poor performance on rare classes. If 99% of examples are negative, a model that always predicts negative achieves 99% accuracy but detects no positives. Precision, recall, F1, PR-AUC, ROC-AUC and task-specific costs may be more informative.

### Q23. What is a confusion matrix?

**Answer:** It counts true positives, true negatives, false positives and false negatives. It helps show the types of mistakes a classifier makes, not just its overall score.

### Q24. What is the difference between a parameter and a hyperparameter?

**Answer:** Parameters are learned from training data, such as neural-network weights. Hyperparameters are choices made by the practitioner or training procedure, such as learning rate, batch size, number of layers, regularisation strength and decoding temperature.

---

# 4. Neural Networks and Deep Learning

## 4.1 How a neural network works

A basic neuron computes a weighted sum plus bias and passes it through an activation function:

\[
z=w^\top x+b,\qquad a=f(z)
\]

A network combines many such units. During training, forward propagation produces predictions, a loss measures error, backpropagation computes gradients, and an optimiser updates the weights.

### Q25. What is an artificial neural network?

**Answer:** It is a parameterised function made of connected computational units organised into layers. The network transforms input representations through learned weights and nonlinear activation functions to produce outputs. Deep networks have multiple layers and can learn hierarchical features.

### Q26. What is an activation function? Why is it needed?

**Answer:** An activation function introduces nonlinearity. Without nonlinear activations, stacking linear layers would still produce an overall linear transformation and would not model many complex relationships. Common functions include ReLU, sigmoid, tanh and GELU.

### Q27. Explain ReLU, sigmoid and softmax.

**Answer:**
- **ReLU:** \(f(x)=\max(0,x)\). Simple and common in hidden layers.
- **Sigmoid:** Maps a scalar to \((0,1)\), often used for a binary probability output.
- **Softmax:** Converts a vector of logits into probabilities that sum to one, commonly for mutually exclusive classes or next-token distributions.

In an LLM, softmax over the vocabulary gives a probability distribution for the next token.

### Q28. What is backpropagation?

**Answer:** Backpropagation applies the chain rule to compute gradients of the loss with respect to network parameters, moving backward through the computation graph. The optimiser then uses those gradients to update parameters. Backpropagation computes gradients; it is not itself the parameter-update rule.

### Q29. What are vanishing and exploding gradients?

**Answer:** During backpropagation, gradients can become extremely small or large as they pass through many layers or time steps. Vanishing gradients slow learning in earlier layers; exploding gradients can destabilise training. Techniques include suitable initialisation, normalisation, residual connections, gated recurrent units, gradient clipping and appropriate architectures.

### Q30. What are embeddings in neural networks?

**Answer:** An embedding is a dense vector representation of an item, such as a token, user, product or document. The vector is learned or computed so it is useful for a task. In language systems, token embeddings represent vocabulary items, while sentence/document embeddings aim to represent larger pieces of text.

### Q31. What is transfer learning?

**Answer:** Transfer learning starts with a model or representation learned on one task or dataset and adapts it to another task. Pretrained LLMs are a major example: their learned language representations are reused for tasks such as summarisation, extraction or question answering.

### Q32. What is fine-tuning?

**Answer:** Fine-tuning continues training a pretrained model on a task- or domain-specific dataset. It can adapt behaviour, style, output formats or specialised patterns. It does not automatically give the model current facts, and poor data or evaluation can make the model worse.

### Q33. What is the difference between full fine-tuning and PEFT?

**Answer:** Full fine-tuning updates most or all model parameters. Parameter-efficient fine-tuning (PEFT) updates a small subset of parameters or adds trainable components. Methods such as LoRA can reduce trainable parameter count, memory use and storage needs, though hardware requirements still depend on the base model and setup.

---

# 5. NLP Foundations and Text Processing

### Q34. What is tokenisation?

**Answer:** Tokenisation converts text into model-specific units called tokens. A token may be a word, part of a word, punctuation or another subword unit. The tokenizer maps text to token IDs; the model operates on those IDs and their learned representations.

**Example:** The word “unbelievable” might be split into multiple subword tokens. The exact split depends on the tokenizer.

### Q35. Why do LLMs use subword tokenisation instead of one token per word?

**Answer:** Word-level vocabularies become huge and struggle with unseen words, names, spelling variations and multilingual text. Character-level tokenisation creates long sequences. Subword methods balance vocabulary size and sequence length while allowing unfamiliar words to be represented as smaller units.

### Q36. What is a vocabulary?

**Answer:** A tokenizer's vocabulary is the set of token units it can map to token IDs. Different models may use different tokenizers and vocabulary sizes, so the same text can have different token counts across models.

### Q37. What are stop words? Are they always removed?

**Answer:** Stop words are frequent words such as “the” or “is” that some traditional NLP pipelines remove for certain tasks. They should not be removed automatically in every GenAI workflow. In LLM prompts, retrieval and semantic search, such words may contribute to meaning, syntax or exact wording.

### Q38. What is stemming vs lemmatisation?

**Answer:** Stemming crudely reduces words to a root-like form, sometimes producing a non-word. Lemmatisation maps a word to its dictionary base form using linguistic information. They are traditional NLP preprocessing techniques and are not automatically necessary for modern embedding-based retrieval.

### Q39. What is named entity recognition (NER)?

**Answer:** NER identifies spans of text that refer to entities such as people, organisations, locations, dates or products. For example, in “OpenAI opened an office in London,” a model may identify “OpenAI” as an organisation and “London” as a location. NER can support information extraction, search and document processing.

### Q40. What is sentiment analysis?

**Answer:** Sentiment analysis estimates the attitude or emotion expressed in text, often as positive, negative or neutral. It can be implemented with a classifier or prompted LLM. Results should be evaluated on representative examples because sarcasm, mixed opinions and domain-specific language are challenging.

---

# 6. Transformers and Attention

Transformers are central to many modern LLMs. They process token representations using attention and feed-forward layers, often with residual connections and normalisation.

## 6.1 Self-attention

Self-attention allows each token representation to incorporate information from other permitted tokens in the sequence.

For an input representation matrix \(X\), learned projections produce queries, keys and values:

\[
Q=XW_Q,\qquad K=XW_K,\qquad V=XW_V
\]

Scaled dot-product attention is:

\[
\operatorname{Attention}(Q,K,V)=
\operatorname{softmax}\left(\frac{QK^\top}{\sqrt{d_k}}\right)V
\]

A causal mask is applied in decoder-only language models so a position cannot attend to future tokens during next-token training.

### Q41. What is a transformer?

**Answer:** A transformer is a neural-network architecture based primarily on attention mechanisms rather than recurrence. It processes token representations through attention and feed-forward blocks. Transformers support parallel processing of training positions and model long-range relationships more effectively than many older sequence architectures, although attention can be computationally expensive for long sequences.

### Q42. What is attention in a transformer?

**Answer:** Attention computes how much information a position should take from other positions. Queries represent what a position is looking for, keys represent what other positions offer for matching, and values contain the information to combine. The analogy is useful, but these are learned vector projections, not literal human intentions.

### Q43. Explain query, key and value.

**Answer:**
- **Query (Q):** Representation used to compare the current position with other positions.
- **Key (K):** Representation used to calculate match scores.
- **Value (V):** Representation that is weighted and combined based on attention scores.

The attention weights are derived from query-key similarity, then applied to the values.

### Q44. Why divide \(QK^\top\) by \(\sqrt{d_k}\)?

**Answer:** As the key dimension grows, dot products can grow in magnitude. Large logits can make softmax very peaked, producing small gradients. Scaling by \(\sqrt{d_k}\) helps keep values in a more suitable range for optimisation.

### Q45. What is multi-head attention?

**Answer:** Multi-head attention uses multiple attention heads with different learned projections. Each head can learn different relationships or representation subspaces. Their outputs are combined through a learned projection. It is not guaranteed that each head has a clean, human-interpretable role.

### Q46. What is positional encoding or positional information?

**Answer:** Attention alone does not inherently identify token order. Transformers therefore need positional information, provided through methods such as sinusoidal positional encodings, learned position embeddings or rotary position embeddings (RoPE), depending on the architecture. These methods help the model represent order and relative position.

### Q47. What is the difference between encoder-only, encoder-decoder and decoder-only transformers?

**Answer:**
- **Encoder-only:** Builds contextual representations of input tokens; often used for understanding tasks, such as BERT-style models.
- **Encoder-decoder:** An encoder processes input and a decoder generates output; often used for sequence-to-sequence tasks, such as translation.
- **Decoder-only:** Predicts the next token using previous context; widely used for generative LLMs.

These are common patterns, not strict limits on what each architecture can do.

### Q48. What is causal attention?

**Answer:** Causal attention masks future positions so each token can use only previous tokens and itself. This matches the autoregressive next-token training objective and prevents the model from seeing the answer token through future context during training.

### Q49. What are residual connections and layer normalisation?

**Answer:** A residual connection adds a block's input to its transformed output, helping information and gradients flow through deep networks. Layer normalisation stabilises activations by normalising features within a sample. Modern transformer blocks typically combine attention, feed-forward layers, residual paths and normalisation.

### Q50. Why are transformers effective for language?

**Answer:** They can represent contextual relationships across tokens, process training sequences in parallel, scale to large datasets and model capacity, and learn useful representations from self-supervised objectives. Their success also depends on data quality, optimisation, architecture, compute and post-training—not just attention alone.

---

# 7. Large Language Models (LLMs)

### Q51. What is an LLM?

**Answer:** A large language model is a language model trained at large scale, typically with many parameters and extensive text/code data. A common training objective is to predict the next token. Through training and later alignment or instruction tuning, the model can perform tasks such as answering questions, summarising, extracting information and generating code.

### Q52. How does a decoder-only LLM generate text?

**Answer:**
1. The input prompt is tokenised into token IDs.
2. The model processes the prompt and computes a probability distribution for the next token.
3. A decoding strategy selects a token from that distribution.
4. The selected token is appended to the context.
5. The process repeats until a stop condition or output limit is reached.

Generation is autoregressive: each generated token can affect the next one.

### Q53. What is next-token prediction?

**Answer:** The model is trained to assign high probability to the actual next token given previous tokens. For a sequence \(x_1,\ldots,x_T\), the objective is commonly expressed as maximising:

\[
\sum_{t=1}^{T}\log P(x_t\mid x_{<t})
\]

Equivalently, training minimises the negative log-likelihood or cross-entropy of the target tokens.

### Q54. What is a foundation model?

**Answer:** A foundation model is trained on broad data at scale and can be adapted to many downstream tasks. It may be a language, vision, audio or multimodal model. An LLM is one type of foundation model, but not all foundation models are LLMs.

### Q55. What is instruction tuning?

**Answer:** Instruction tuning trains a pretrained model on examples of instructions and appropriate responses so it better follows user requests. It is one form of supervised fine-tuning and is distinct from the initial broad pretraining stage.

### Q56. What is alignment?

**Answer:** Alignment refers broadly to shaping model behaviour to better follow intended instructions, human preferences and safety requirements. Methods can include supervised fine-tuning, preference optimisation and reinforcement-learning-based approaches. Alignment is imperfect and does not guarantee truthfulness or safety.

### Q57. What is RLHF?

**Answer:** Reinforcement Learning from Human Feedback is a family of approaches that uses human preference feedback to improve model behaviour. A common pipeline collects preference comparisons, trains a reward model, and optimises a policy against that reward, with safeguards such as a reference-policy constraint. Some modern systems use other preference-optimisation methods, so RLHF is not the only alignment technique.

### Q58. What is the difference between pretraining, fine-tuning and inference?

**Answer:**
- **Pretraining:** Learns broad patterns from large-scale data.
- **Fine-tuning/post-training:** Adapts a pretrained model to desired behaviours or tasks.
- **Inference:** Uses the trained model to produce outputs for new inputs.

Inference does not normally update the model's weights.

### Q59. Does an LLM store a database of facts?

**Answer:** Not in the same way as a conventional database. Its parameters encode statistical patterns learned during training, which can include information about the world. It may recall some facts, but recall can be incomplete or wrong, and its knowledge may be outdated. A database or retrieval system is preferable when answers must be grounded in authoritative, current records.

### Q60. What is a context window?

**Answer:** The context window is the maximum amount of tokenised input and output context a model can handle in a single request, according to that model's limits. The exact counting rules vary by provider and model. System instructions, conversation history, retrieved passages, tool outputs and generated tokens may all consume context.

### Q61. What happens if a prompt exceeds the context window?

**Answer:** The request may be rejected, truncated or handled by a framework that removes or summarises context. The exact behaviour depends on the model and application. A robust application should count tokens, reserve space for output and use an intentional strategy such as retrieval, chunking or summarisation.

### Q62. What is an open-weight model vs a hosted model API?

**Answer:** A hosted API lets an application call a provider's model without managing its inference infrastructure, but introduces provider costs, quotas, network dependency and data-handling considerations. An open-weight model can be deployed or adapted on infrastructure the organisation controls, but requires hardware, operations, security and licence review. “Open-weight” does not necessarily mean fully open-source in every respect.

---

# 8. Tokens, Embeddings and Vector Similarity

## 8.1 Token embeddings vs semantic embeddings

A token embedding maps an individual token ID to a vector that enters the model. A text embedding model maps a larger text span—such as a sentence, paragraph or document—to a vector intended to capture useful semantic or task-specific information.

### Q63. What is an embedding?

**Answer:** An embedding is a numerical vector representing an item in a learned feature space. In semantic search, an embedding model maps queries and documents into a vector space where related items are expected to be close under a suitable similarity measure.

### Q64. What is the difference between token embeddings and sentence embeddings?

**Answer:** Token embeddings represent individual vocabulary tokens and are used inside a language model. Sentence embeddings represent an entire sentence or text passage as one vector for tasks such as semantic search, clustering or similarity comparison. The latter usually comes from a model specifically trained or configured to produce text-level representations.

### Q65. What is cosine similarity?

**Answer:** Cosine similarity measures the cosine of the angle between two vectors:

\[
\cos(\theta)=\frac{A\cdot B}{\|A\|\|B\|}
\]

It measures directional similarity, not absolute magnitude. It is commonly used for text-embedding comparisons. The score's interpretation depends on the embedding model and task; a high score is not automatically a calibrated probability that two texts are equivalent.

### Q66. What is the difference between cosine similarity and Euclidean distance?

**Answer:** Cosine similarity compares vector direction; Euclidean distance measures straight-line distance between vector points. For normalised vectors, the two rankings are closely related because squared Euclidean distance equals \(2-2\cos(\theta)\). Without normalisation, vector magnitude can affect Euclidean distance differently.

### Q67. What is a vector database?

**Answer:** A vector database stores embeddings and supports similarity search, often alongside metadata and filtering. In a RAG system, it can retrieve text chunks likely to be relevant to a user's query. Examples of vector-search technologies include specialised vector databases and vector capabilities added to general-purpose databases. The right choice depends on scale, filtering, deployment and operational needs.

### Q68. Does semantic similarity guarantee factual relevance?

**Answer:** No. Two texts can be semantically similar but differ in dates, quantities, negation or key details. Retrieval should be evaluated on the actual task, and systems may combine dense retrieval, keyword search, metadata filters, reranking and answer-grounding checks.

### Q69. What are dense and sparse retrieval?

**Answer:** Dense retrieval represents queries and documents as dense vectors and finds nearby vectors. Sparse retrieval represents text with sparse features, such as word terms and weights, as in BM25. Dense retrieval can help with paraphrases; sparse retrieval can be strong for exact names, identifiers and rare terms. Hybrid retrieval combines their strengths.

### Q70. What is a reranker?

**Answer:** A reranker takes an initial set of retrieved candidates and scores them more carefully for relevance to the query. A common architecture is a cross-encoder that reads the query and candidate together. Reranking can improve the ordering of relevant passages but adds latency and compute.

---

# 9. Prompt Engineering

Prompt engineering is the design and testing of instructions and context provided to a model. It improves task clarity, but it cannot guarantee correctness or replace reliable data and evaluation.

### Q71. What makes a good prompt?

**Answer:** A good prompt states the task, relevant context, constraints, desired output format and how to handle missing information. It avoids contradictory instructions and includes examples when they clarify the expected behaviour.

**Example prompt:**

> You are an information-extraction assistant. Extract the invoice number, invoice date and total from the supplied text. Return valid JSON matching the specified schema. If a field is absent, use `null`. Do not infer values that are not present.

### Q72. What is zero-shot prompting?

**Answer:** Zero-shot prompting asks the model to perform a task using instructions without providing worked examples in the prompt.

### Q73. What is few-shot prompting?

**Answer:** Few-shot prompting includes a small number of input-output examples to demonstrate the desired task or format. It can improve consistency for a task, but examples must be representative and should not conflict with the instruction.

### Q74. What is chain-of-thought prompting?

**Answer:** Chain-of-thought prompting encourages a model to reason through intermediate steps for tasks that benefit from decomposition. In a production application, it is often better to request a concise explanation, a structured result, or verifiable intermediate outputs rather than depend on a long free-form reasoning trace. Generated reasoning text is not guaranteed to faithfully reveal the model's internal computation.

### Q75. What is system, developer and user instruction hierarchy?

**Answer:** Many chat systems distinguish higher-priority system or developer instructions from user messages. Higher-priority instructions define application behaviour and constraints, while user instructions describe the immediate task. Exact roles and conflict rules depend on the API. Treating untrusted document text as instructions can create prompt-injection vulnerabilities.

### Q76. What is prompt injection?

**Answer:** Prompt injection is an attack in which malicious or irrelevant text attempts to override instructions, reveal data or cause an LLM application to misuse tools. It can appear directly in a user prompt or indirectly in retrieved documents, websites or tool results.

**Mitigations:** Keep secrets out of model context, treat retrieved content as untrusted data, enforce tool permissions in code, validate arguments, restrict data access, require confirmation for consequential actions, and test adversarial cases. A prompt saying “ignore prompt injection” is not a sufficient security boundary.

### Q77. What is structured output?

**Answer:** Structured output means returning data in a predefined format, often JSON that follows a schema. When supported, schema-constrained generation can reduce formatting errors. The application should still validate the result, handle missing or invalid fields and check business rules.

### Q78. How do you make an LLM return valid JSON?

**Answer:** Prefer a provider's structured-output or JSON-schema mode when available. Define required fields, types, allowed values and null behaviour. Otherwise, give an explicit schema example, parse the response, validate it and handle failures with bounded retries. Do not assume that asking for JSON in plain text guarantees valid JSON.

### Q79. What is prompt versioning and why is it useful?

**Answer:** Prompt versioning stores changes to prompts with identifiers and tests. It makes regressions traceable, supports controlled experiments and allows the team to compare quality, latency and cost across versions. Prompts should be treated as part of the application's code and evaluation process.

---

# 10. Inference, Decoding and Model Parameters

### Q80. What is temperature?

**Answer:** Temperature adjusts the sharpness of the next-token probability distribution during sampling. Lower temperature generally makes outputs more predictable; higher temperature generally increases variety. It does not add knowledge or guarantee factuality. Exact effects depend on the model and decoding implementation.

### Q81. What is top-k sampling?

**Answer:** Top-k sampling restricts token selection to the \(k\) most probable next-token candidates, then samples among them after renormalising their probabilities.

### Q82. What is top-p (nucleus) sampling?

**Answer:** Top-p sampling chooses from the smallest set of high-probability tokens whose cumulative probability reaches a threshold \(p\), then samples from that set. Unlike fixed top-k, the candidate-set size can vary by context.

### Q83. What is greedy decoding?

**Answer:** Greedy decoding chooses the highest-probability next token at every step. It is simple and deterministic for a fixed model and context, but a locally most likely token at each step does not necessarily produce the best overall response.

### Q84. What is beam search?

**Answer:** Beam search maintains several candidate sequences and expands the most promising ones at each step, using a scoring rule. It is common in some sequence-to-sequence tasks. For open-ended chat, beam search is not automatically better; it can produce repetitive or less natural responses depending on the model and objective.

### Q85. What are max output tokens and stop sequences?

**Answer:** A maximum output-token setting limits generation length. A stop sequence tells the serving system to stop when a specified token sequence or pattern is reached, where supported. The application should account for token limits and avoid truncating required structured output.

### Q86. Does lowering temperature eliminate hallucinations?

**Answer:** No. It may make outputs more consistent, but a model can confidently produce incorrect information at low temperature. Grounding, retrieval, tool use, verification, calibrated refusal behaviour and evaluation are more direct ways to address factuality.

---

# 11. Hallucinations, Limitations and Responsible AI

### Q87. What is an LLM hallucination?

**Answer:** A hallucination is output that is false, unsupported or inconsistent with the available evidence but is presented as if it were valid. Examples include fabricated citations, incorrect dates or invented API parameters.

### Q88. Why do LLMs hallucinate?

**Answer:** Next-token training optimises plausible sequence prediction, not a universal truth-verification objective. A model may lack relevant information, misinterpret a prompt, overgeneralise patterns, receive misleading context or be pushed to answer when it should abstain. Retrieval and tools can help, but they introduce their own errors.

### Q89. How can you reduce hallucinations in a business application?

**Answer:**
1. Retrieve relevant, authoritative evidence for knowledge-specific questions.
2. Tell the model to distinguish evidence from assumptions and to abstain when evidence is insufficient.
3. Provide citations tied to actual retrieved source IDs and validate them.
4. Use tools or deterministic code for calculations and current facts.
5. Validate structured outputs and business rules.
6. Evaluate with representative and adversarial test cases.
7. Monitor incorrect answers and user feedback.
8. Keep human review for high-impact decisions.

No single technique eliminates hallucinations.

### Q90. What is grounding?

**Answer:** Grounding ties an answer to evidence, such as supplied documents, database records, or verified tool results. A grounded system should make it possible to trace claims to evidence. Merely including documents in a prompt does not guarantee that every generated claim is supported.

### Q91. What is responsible AI in a GenAI application?

**Answer:** It means designing for safety, privacy, fairness, transparency, security and accountability. The appropriate controls depend on the use case and risk. They can include data minimisation, access controls, content checks, evaluation across user groups, audit logs, human oversight and clear limits on what the system can do.

### Q92. What is PII, and how should a GenAI system handle it?

**Answer:** Personally identifiable information (PII) is information that identifies or can help identify a person, depending on context and jurisdiction. Minimise what is collected and sent to model providers, apply access controls and retention policies, redact where appropriate, and follow applicable laws and organisational policies. Never place API keys or credentials in prompts.

### Q93. Can model output be trusted without checking?

**Answer:** Not for consequential or evidence-sensitive tasks. Use deterministic validation, source checking, tests or human review appropriate to the risk. A fluent answer is not proof of correctness.

---

# 12. Python and Essential Technical Coding Questions

GenAI internships frequently test Python, data structures, APIs and the ability to reason about model outputs. Practise writing code without relying entirely on libraries.

## Q94. What is the difference between a list, tuple, set and dictionary in Python?

**Answer:**
- `list`: ordered, mutable collection; permits duplicates.
- `tuple`: ordered, immutable sequence.
- `set`: collection of unique hashable values; useful for membership checks and set operations.
- `dict`: key-value mapping; keys must be hashable.

```python
names = ["Asha", "Ravi", "Asha"]
unique_names = set(names)
scores = {"Asha": 90, "Ravi": 85}
```

## Q95. What is a generator in Python?

**Answer:** A generator yields values lazily instead of building the entire result in memory at once. It is useful for processing large files or streams.

```python
def read_chunks(items, size):
    for start in range(0, len(items), size):
        yield items[start:start + size]

for chunk in read_chunks(list(range(10)), 3):
    print(chunk)
```

This example illustrates chunking; real document pipelines should also consider token limits and meaningful text boundaries.

## Q96. What is the difference between `==` and `is`?

**Answer:** `==` compares values for equality. `is` checks whether two references point to the same object. Use `is None` to test for `None`; do not use `is` for ordinary string or numeric equality.

## Q97. What is exception handling, and why does it matter in an LLM application?

**Answer:** Exception handling uses constructs such as `try` and `except` to handle failures without crashing the entire application. Model APIs can time out, reject requests, hit rate limits or return malformed output. Catch expected errors, log useful diagnostics without exposing secrets, use bounded retries where appropriate and return clear errors to clients.

```python
import json

raw = '{"answer": "hello"}'

try:
    result = json.loads(raw)
except json.JSONDecodeError:
    result = None

if result is None:
    print("Could not parse the model response")
```

## Q98. Write a function to count word frequencies.

```python
from collections import Counter
import re

def word_frequencies(text: str) -> dict[str, int]:
    words = re.findall(r"\b[\w']+\b", text.lower())
    return dict(Counter(words))

print(word_frequencies("GenAI is useful. GenAI is evolving!"))
```

**Expected idea:** Normalise text, extract tokens and count them. This simple example is not a production-grade multilingual tokenizer.

## Q99. Write a function to split a list into batches.

```python
def batches(items, batch_size):
    if batch_size <= 0:
        raise ValueError("batch_size must be positive")

    for i in range(0, len(items), batch_size):
        yield items[i:i + batch_size]

print(list(batches([1, 2, 3, 4, 5], 2)))
# [[1, 2], [3, 4], [5]]
```

**Why it matters:** Batch processing is common when embedding many documents or calling services with per-request limits. Production batching should also respect token counts, provider limits and error handling.

## Q100. What is time complexity, and why does it matter?

**Answer:** Time complexity describes how an algorithm's work grows as input size grows. For example, scanning a list is \(O(n)\), while checking membership in a hash set is typically \(O(1)\) on average. Retrieval, chunking, reranking and data processing choices can strongly affect application latency at scale.

## Q101. What is asynchronous programming, and why is it useful for API calls?

**Answer:** Asynchronous programming allows a program to wait for I/O—such as network requests—without blocking the entire execution flow. It can improve throughput when an application makes many concurrent API calls. It does not automatically make CPU-heavy model inference faster, and concurrency must respect provider rate limits.

## Q102. What is an API?

**Answer:** An API defines how software components communicate. A GenAI backend may expose endpoints such as `POST /chat`, `POST /documents` or `GET /health`. The API should validate inputs, authenticate users where needed, manage errors and return predictable response formats.

## Q103. What is the difference between authentication and authorisation?

**Answer:** Authentication verifies who a user or service is. Authorisation decides what that identity is allowed to do. A valid login must not automatically grant access to every document, vector index, tool or administrative operation.

## Q104. Why should API keys be stored in environment variables or a secret manager?

**Answer:** Secrets should not be committed to source control or exposed to browsers, logs or prompts. Environment variables or secret-management systems help separate credentials from code. Production systems should also rotate keys, scope permissions and restrict access.

---

# 13. API and Software Engineering Foundations for GenAI

### Q105. How would you integrate an LLM API into a backend?

**Answer:**
1. Keep the provider key on the server.
2. Validate and limit user input.
3. Build the request using controlled system instructions and required context.
4. Call the provider with timeouts and appropriate limits.
5. Handle rate limits, network errors and provider errors.
6. Validate the returned content or schema.
7. Return a safe, stable response to the frontend.
8. Record operational metrics while avoiding unnecessary sensitive-data logging.

### Q106. What is a timeout?

**Answer:** A timeout limits how long the application waits for an operation. Without timeouts, a stalled upstream call can occupy resources and degrade the service. Choose timeouts based on expected response time and user experience, and handle timeout failures explicitly.

### Q107. What is rate limiting?

**Answer:** Rate limiting caps how often a user, key or service can make requests within a time period. It helps control cost, prevent abuse and stay within provider quotas. A robust system may combine per-user limits, global limits, concurrency limits and retry policies.

### Q108. Why should you not blindly retry every failed model call?

**Answer:** Some failures are permanent, such as invalid input or authentication errors. Retrying them wastes time and money. Retry transient failures with bounded exponential backoff and jitter, respect `Retry-After` when provided, and avoid duplicating non-idempotent tool actions.

### Q109. What is streaming output?

**Answer:** Streaming sends pieces of a response to the client as they are generated instead of waiting for the full answer. It can reduce perceived latency. The application must handle interrupted streams, partial output, cancellation and incomplete structured data.

### Q110. What should be logged for a GenAI system?

**Answer:** Useful operational metadata includes request ID, model/version, latency, token usage, estimated cost, status, retry count, retrieval metrics and evaluation outcomes. Log prompts or outputs only when justified by policy and user expectations; redact secrets and sensitive data. Logs need access control and retention limits.

### Q111. How would you test an LLM application?

**Answer:** Use unit tests for deterministic code, integration tests for provider/retrieval connections, and evaluation datasets for response quality. Include normal, edge, adversarial and unanswerable questions. Measure task-specific quality, factual grounding, schema validity, safety, latency and cost. Re-run evaluations when prompts, models, data or retrieval settings change.

### Q112. What is the difference between unit, integration and end-to-end tests?

**Answer:**
- **Unit tests:** Test one function or component in isolation.
- **Integration tests:** Check that components work together, such as the backend and vector store.
- **End-to-end tests:** Exercise the complete user workflow from input to final output.

For non-deterministic LLM outputs, tests should usually check criteria or structured invariants rather than demand an identical sentence every time.

---

# 14. Common Interview Scenarios

## Scenario 1: “The chatbot gives wrong answers about our company policies. What would you do?”

**Strong answer:**

First, I would identify whether the problem comes from missing source documents, retrieval failure, poor chunking, prompt construction, model behaviour or unsupported questions. I would create a test set of representative policy questions with verified answers. Then I would retrieve authoritative policy passages, inspect retrieval precision and recall, improve chunking and metadata filters, and consider reranking. I would require the response to cite retrieved source IDs and abstain when evidence is insufficient. Finally, I would evaluate factual correctness, citation validity, latency and cost before deploying changes.

**Why this answer is strong:** It diagnoses the pipeline instead of assuming that changing the prompt will fix everything.

## Scenario 2: “The response is accurate but takes 12 seconds. How would you reduce latency?”

**Strong answer:**

I would measure where time is spent: queueing, retrieval, reranking, provider time-to-first-token and total generation. Depending on the bottleneck, I could reduce unnecessary context, use a faster model, stream output, cache safe repeatable results, parallelise independent I/O, reduce output length or optimise retrieval. I would compare quality, latency and cost on the same evaluation set before choosing a trade-off.

## Scenario 3: “The model sometimes returns invalid JSON.”

**Strong answer:**

I would use schema-constrained output if the provider supports it, define required fields and types, parse the result, validate business rules, and handle failures safely. A bounded repair/retry step may be appropriate, but I would not rely on unlimited retries or treat syntactically valid JSON as semantically correct.

## Scenario 4: “A user asks for information that is not in the company documents.”

**Strong answer:**

The system should not invent a policy answer. I would design it to distinguish supported from unsupported questions, provide relevant evidence when available, and say that the information could not be found when it cannot ground an answer. If useful, it can ask a clarifying question or route the request to an authorised human.

## Scenario 5: “A retrieved document tells the model to reveal its system prompt.”

**Strong answer:**

I would treat retrieved text as untrusted data rather than executable instructions. The application should not store secrets in prompts, tool permissions should be enforced in backend code, and document content should not be allowed to expand the user's access. I would test indirect prompt-injection cases and inspect whether the model or tools can expose restricted information.

## Scenario 6: “Should we fine-tune or use RAG?”

**Strong answer:**

I would start from the failure mode. If the model needs access to changing, private or source-specific facts, I would usually evaluate RAG first. If the main problem is consistent behaviour, domain-specific patterns, style or output format, fine-tuning may help. They can also be combined. I would compare both approaches using a representative evaluation set, considering data readiness, update frequency, latency, cost and maintenance.

## Scenario 7: “How do you know your RAG system is working?”

**Strong answer:**

I would evaluate retrieval and generation separately. Retrieval metrics can include Recall@k, Precision@k, MRR or nDCG against labelled relevant passages. Generation can be measured for correctness, faithfulness to retrieved evidence, completeness, citation correctness and appropriate abstention. I would also measure latency and cost, then inspect failures manually because a single aggregate score can hide important issues.

## Scenario 8: “A stakeholder wants the chatbot to answer every question.”

**Strong answer:**

I would explain that answering every question can increase unsupported claims and risk. I would define when the system should answer, ask for clarification, use a tool, or abstain and escalate. I would measure both answer quality and abstention quality, so the system is helpful when evidence exists without pretending to know what it does not know.

## Scenario 9: “How would you control GenAI costs?”

**Strong answer:**

I would track tokens and cost by feature, choose a model that meets the quality target rather than always using the largest model, reduce irrelevant context, set output limits, cache eligible repeated requests, batch embedding work, and avoid unnecessary multi-step calls. I would monitor cost per successful task, not just cost per request, because cheap incorrect responses can be more expensive operationally.

## Scenario 10: “What would you do if the LLM provider is unavailable?”

**Strong answer:**

I would handle provider errors and timeouts explicitly, use bounded retries for transient failures, expose a clear temporary-unavailability response, and consider a fallback model only if it has been tested and is authorised for the same data. Queuing or graceful degradation may be suitable. I would not silently route sensitive data to a different provider without approval.

---

# 15. Rapid-Fire Revision Questions

Try answering each in 20–40 seconds.

### Q113. What is perplexity?

**Answer:** Perplexity is an exponentiated average negative log-likelihood, commonly used to evaluate language-model prediction on a token sequence. Lower perplexity means the model assigned higher probability to the observed tokens under that evaluation setup. It does not directly measure usefulness, safety or factual correctness.

### Q114. What are logits?

**Answer:** Logits are unnormalised scores produced before applying a probability function such as softmax. In next-token prediction, the model produces a logit for each candidate vocabulary token.

### Q115. What is a GPU used for in deep learning?

**Answer:** GPUs perform many parallel numerical operations efficiently, especially matrix multiplications used in neural networks. Training and serving large models may require substantial GPU memory and compute, although smaller models can run on CPUs or other accelerators.

### Q116. What is quantisation?

**Answer:** Quantisation represents model weights or activations using lower-precision numeric formats, such as 8-bit or 4-bit values, instead of higher-precision formats. It can reduce memory use and sometimes improve inference speed, with a possible quality trade-off depending on the model and method.

### Q117. What is model distillation?

**Answer:** Distillation trains a smaller student model to imitate behaviour or outputs from a larger teacher model or another target. It can produce a cheaper, faster model for a specific use case, but performance depends on the training data, objective and evaluation.

### Q118. What is catastrophic forgetting?

**Answer:** Catastrophic forgetting is when learning new data or tasks damages performance on previously learned tasks. It can occur during fine-tuning. Representative data, careful learning rates, parameter-efficient methods and evaluation on both old and new tasks can help detect or reduce it.

### Q119. What is an agent in GenAI?

**Answer:** An LLM-based agent is a system that uses a model to choose or sequence actions—often tool calls—toward a goal, with application logic controlling permissions and execution. A reliable agent needs bounded steps, tool validation, error handling and safeguards. Not every chatbot is an agent.

### Q120. What is function calling or tool calling?

**Answer:** The model emits a structured request to call a named tool with arguments. The application validates the request, executes the tool if authorised, and returns the result to the model or user. The model's proposed tool call is not itself proof that the action is safe or valid.

### Q121. What is multimodal AI?

**Answer:** Multimodal AI processes or generates more than one modality, such as text, images, audio or video. A multimodal model may answer questions about an image or combine speech input with text output. Capabilities and limits vary by model.

### Q122. What is an evaluation benchmark?

**Answer:** A benchmark is a defined dataset and scoring procedure used to compare systems. A useful benchmark should reflect the target task and avoid leakage. High benchmark scores do not guarantee performance in a different real-world environment.

### Q123. What is an ablation study?

**Answer:** An ablation study removes or changes one component at a time to estimate its contribution. For example, compare a RAG pipeline with and without reranking while holding other conditions constant.

### Q124. What is an embedding dimension?

**Answer:** It is the number of numeric values in an embedding vector. Higher dimensionality does not automatically mean better retrieval. The model, training objective, corpus, index and similarity measure all matter.

### Q125. What is cosine similarity score of 0.9 telling you?

**Answer:** It indicates that two vectors point in similar directions under cosine similarity, but its practical meaning depends on the embedding model and task. It is not automatically a 90% probability of relevance.

### Q126. What is a knowledge cutoff?

**Answer:** It is a rough boundary for the period covered by a model's training data, although actual coverage varies. It does not prevent the model from using new information supplied in the prompt or through tools, and it does not guarantee that all earlier information is known correctly.

### Q127. What is the difference between a chatbot and RAG?

**Answer:** A chatbot is an interaction interface or application pattern. RAG is a technique that retrieves relevant external information and supplies it to a generative model. A chatbot may use RAG, but a chatbot does not inherently require it.

### Q128. What is an API hallucination?

**Answer:** It is when a model invents or misstates a function, parameter, endpoint or library behaviour. Use official documentation, tool execution, type checking, tests and version-aware retrieval instead of trusting generated code blindly.

### Q129. What is idempotency?

**Answer:** An operation is idempotent if repeating it has the same effect as performing it once. Idempotency keys or request IDs help prevent duplicate effects when a client retries a request, particularly for payments, bookings or other state-changing tools.

### Q130. Why are citations not enough to guarantee a grounded answer?

**Answer:** A model may attach a real citation to a claim that the source does not support, cite the wrong passage, or omit important context. A robust system checks that each citation maps to a retrieved source and evaluates whether the cited evidence actually supports the claim.

---

# 16. Practice Interview Checklist

Use this as a self-assessment. Mark a topic only when you can explain it without reading.

- [ ] Explain AI, ML, DL, NLP and GenAI with examples.
- [ ] Explain supervised, unsupervised and self-supervised learning.
- [ ] Describe loss, gradient descent, backpropagation and learning rate.
- [ ] Explain overfitting, data leakage and train/validation/test splits.
- [ ] Explain neural-network activations and embeddings.
- [ ] Draw a transformer block and explain attention.
- [ ] Explain Q, K, V, multi-head attention and causal masking.
- [ ] Explain next-token prediction and autoregressive generation.
- [ ] Distinguish pretraining, instruction tuning, fine-tuning and inference.
- [ ] Explain tokens, context windows and output limits.
- [ ] Compare token embeddings and text embeddings.
- [ ] Explain cosine similarity, dense retrieval and sparse retrieval.
- [ ] Explain prompt design, few-shot prompting and structured outputs.
- [ ] Explain temperature, top-k, top-p and greedy decoding.
- [ ] Explain hallucinations, grounding, prompt injection and privacy risks.
- [ ] Write Python functions for counting, batching, parsing and validation.
- [ ] Explain API keys, timeouts, retries, rate limits and logging.
- [ ] Answer the ten scenario questions with a clear diagnosis and evaluation plan.

## A suggested way to practise

1. Read one section.
2. Close the file and explain each answer aloud in your own words.
3. Write a short example or diagram for the harder concepts.
4. Mark questions you could not answer confidently and revisit them the next day.
5. Do a timed mock interview: 20–30 minutes of concepts, 20 minutes of coding and 10 minutes of scenarios.

---

# 17. Glossary

| Term | Meaning |
|---|---|
| AI | Broad field of intelligent computer systems |
| ML | Learning patterns from data |
| DL | Machine learning with multilayer neural networks |
| NLP | Processing and generating human language |
| GenAI | Models and systems that generate content |
| LLM | Large-scale language model |
| Token | A unit processed by a tokenizer and model |
| Tokenizer | Maps text to token IDs and often back to text |
| Embedding | Dense vector representation |
| Attention | Weighted information mixing between sequence positions |
| Transformer | Neural architecture built around attention and feed-forward blocks |
| Logit | Unnormalised output score |
| Softmax | Converts scores to a probability distribution |
| Loss | Numerical training objective or error measure |
| Gradient | Derivative of the loss with respect to parameters |
| Fine-tuning | Further training of a pretrained model |
| PEFT | Parameter-efficient fine-tuning |
| LoRA | Low-Rank Adaptation, a PEFT method |
| Inference | Using a trained model to generate predictions |
| RAG | Retrieval-Augmented Generation |
| Vector database | Store/search system for embeddings |
| Reranker | Model that reorders retrieved candidates by relevance |
| Hallucination | Unsupported or incorrect generated content presented as valid |
| Grounding | Tying output to evidence or verified data |
| Prompt injection | Malicious input attempting to override instructions or misuse tools |
| Temperature | Sampling parameter affecting distribution sharpness |
| Quantisation | Lower-precision representation to reduce model resource use |
| Latency | Time taken to complete or begin a response |
| Throughput | Amount of work completed per unit time |
| Rate limit | Maximum allowed request frequency or volume |
| Evaluation | Systematic measurement of task performance and risks |

---

## Final interview advice

For a technical internship interview, do not stop at definitions. For each concept, be ready to explain:

1. **What it is.**
2. **Why it is used.**
3. **How it works at a high level.**
4. **One practical example.**
5. **Its limitations or trade-offs.**

For example, if asked about embeddings, explain the vector representation, how cosine similarity can rank documents, how it supports semantic retrieval, and why a high similarity score still needs evaluation. That depth is more valuable than memorising dozens of buzzwords.

**End of Part 1 — Foundations.** The next parts can move into advanced GenAI engineering (RAG, chunking, vector search, reranking, fine-tuning, agents, evaluation and deployment) and then coding/system-design mock interviews.
