# Bruviti AI Placement Technical Preparation (AI/ML Focus)

## 1. Understanding Bruviti AI Technology

Bruviti builds AI systems for enterprise service operations. Their
platform focuses on agentic AI, AI workflows, knowledge systems, and
automation of complex service processes.

Important technical areas based on Bruviti's technology direction:

-   Agentic AI
-   Large Language Models (LLMs)
-   Retrieval Augmented Generation (RAG)
-   Knowledge graphs and ontology
-   AI workflow orchestration
-   Enterprise AI security
-   ML models for prediction and classification

Bruviti's platform architecture uses concepts like: - AI agents -
Workflows - Tasks - Tools - Event-driven communication - AI-driven
routing

------------------------------------------------------------------------

# Artificial Intelligence Questions

## Q1. What is Artificial Intelligence?

### Answer:

Artificial Intelligence is a field of computer science that enables
machines to perform tasks that normally require human intelligence, such
as understanding language, recognizing patterns, making decisions, and
learning from data.

Examples: - Chatbots - Recommendation systems - Image recognition -
Autonomous systems

------------------------------------------------------------------------

## Q2. Difference between AI, ML, and Deep Learning?

### Answer:

AI: The complete field of making machines intelligent.

ML: A subset of AI where machines learn patterns from data.

Deep Learning: A subset of ML using neural networks with multiple
layers.

Example:

AI: "Computer understands customer complaint"

ML: "Model predicts complaint category"

Deep Learning: "Neural network understands image or speech"

------------------------------------------------------------------------

# Machine Learning Questions

## Q3. What are the types of Machine Learning?

### Answer:

### 1. Supervised Learning

Training data contains input and correct output.

Examples: - Spam detection - Disease prediction - Image classification

Algorithms: - Linear Regression - Logistic Regression - Decision Tree -
Random Forest - SVM

### 2. Unsupervised Learning

Data has no labels. Model finds hidden patterns.

Examples: - Customer segmentation - Clustering

Algorithms: - K-Means - PCA

### 3. Reinforcement Learning

Agent learns by interacting with environment using rewards and
penalties.

Examples: - Robotics - Game AI

------------------------------------------------------------------------

## Q4. What is overfitting?

### Answer:

Overfitting happens when a model learns training data too well,
including noise, and performs poorly on new data.

Solutions: - More training data - Regularization - Dropout -
Cross-validation

------------------------------------------------------------------------

## Q5. Difference between training data and testing data?

### Answer:

Training data: Used to teach the model.

Testing data: Used to evaluate performance on unseen data.

------------------------------------------------------------------------

# Generative AI and LLM Questions

## Q6. What is an LLM?

### Answer:

Large Language Model is a deep learning model trained on huge amounts of
text data to understand and generate human-like language.

Examples: - GPT models - Llama - Mistral

Applications: - Chatbots - Document analysis - AI assistants

------------------------------------------------------------------------

## Q7. How does an LLM work?

### Answer:

High-level process:

1.  Text is converted into tokens.
2.  Tokens are converted into numerical representations.
3.  Transformer architecture processes relationships between tokens.
4.  Model predicts the next possible token.
5.  Output text is generated.

------------------------------------------------------------------------

## Q8. What is a Transformer model?

### Answer:

Transformer is a neural network architecture that uses attention
mechanisms to understand relationships between words.

Main components: - Encoder - Decoder - Self-attention - Positional
encoding

------------------------------------------------------------------------

## Q9. What is attention mechanism?

### Answer:

Attention allows a model to focus on important parts of input while
generating output.

Example:

In a sentence, the model can understand which words are important for
the current prediction.

------------------------------------------------------------------------

# RAG (Retrieval Augmented Generation)

## Q10. What is RAG?

### Answer:

RAG combines a language model with external knowledge retrieval.

Process:

User Question \| Retrieve relevant documents \| Send context to LLM \|
Generate answer

Benefits: - Reduces hallucination - Uses updated information - Works
with private company data

------------------------------------------------------------------------

## Q11. Difference between RAG and fine tuning?

### Answer:

RAG: - Adds external knowledge - No model retraining required - Good for
changing information

Fine tuning: - Changes model behavior - Requires training data -
Expensive

------------------------------------------------------------------------

# Embeddings and Vector Database

## Q12. What are embeddings?

### Answer:

Embeddings convert text, images, or data into numerical vectors that
represent meaning.

Similar meanings have similar vector positions.

Example:

"car repair"

and

"vehicle maintenance"

will have similar embeddings.

------------------------------------------------------------------------

## Q13. What is a vector database?

### Answer:

A vector database stores embeddings and performs similarity search.

Examples: - Pinecone - FAISS - Weaviate - Chroma

Used in: - RAG systems - Semantic search - Recommendation systems

------------------------------------------------------------------------

# AI Agents

## Q14. What is an AI Agent?

### Answer:

An AI agent is a system that can understand goals, reason, use tools,
make decisions, and perform actions automatically.

Architecture:

Goal \| Agent \| Reasoning \| Tools/API \| Action \| Feedback

------------------------------------------------------------------------

## Q15. Difference between chatbot and AI agent?

### Answer:

Chatbot: Only responds to user queries.

AI Agent: Can plan, make decisions, call tools, and complete tasks.

Example:

Chatbot: "Your machine problem may be a sensor issue."

Agent: - Checks machine history - Searches manuals - Finds possible
cause - Creates service request

------------------------------------------------------------------------

## Q16. What is Agentic AI?

### Answer:

Agentic AI refers to AI systems that can autonomously execute multi-step
workflows.

Important concepts: - Planning - Reasoning - Tool usage - Memory -
Feedback loop

------------------------------------------------------------------------

# Bruviti-Specific Architecture Questions

## Q17. Explain event-driven architecture.

### Answer:

Event-driven architecture allows systems to communicate through events.

Example:

New service request created.

Event is published.

Different agents react: - Diagnosis agent - Parts agent - Notification
agent

Benefits: - Scalability - Loose coupling - Faster processing

------------------------------------------------------------------------

## Q18. What is AI-driven routing?

### Answer:

AI-driven routing selects the best workflow or agent based on context.

Example:

Customer complaint:

"My machine produces abnormal noise"

AI identifies: - Equipment type - Possible failure - Correct diagnostic
workflow

------------------------------------------------------------------------

## Q19. What is knowledge graph?

### Answer:

A knowledge graph stores entities and relationships between them.

Example:

Machine \| contains \| Motor \| has problem \| Overheating

Used for: - Better reasoning - Context understanding - Semantic search

------------------------------------------------------------------------

## Q20. What is ontology in AI?

### Answer:

Ontology defines concepts, entities, and relationships in a specific
domain.

Example:

Service domain ontology:

Equipment Component Part Failure Repair Procedure

It helps AI understand domain knowledge.

------------------------------------------------------------------------

# Computer Vision Questions

## Q21. How can AI analyze uploaded images?

### Answer:

Computer vision pipeline:

Image \| Preprocessing \| Feature extraction \| Deep learning model \|
Classification/Object detection \| Result

Applications: - Defect detection - Damage identification - Quality
inspection

------------------------------------------------------------------------

# NLP Questions

## Q22. What is NLP?

### Answer:

Natural Language Processing enables computers to understand and generate
human language.

Applications: - Translation - Sentiment analysis - Chatbots - Text
classification

------------------------------------------------------------------------

## Q23. What is tokenization?

### Answer:

Tokenization converts text into smaller units called tokens.

Example:

"AI is powerful"

Tokens: AI is powerful

------------------------------------------------------------------------

# Model Evaluation Questions

## Q24. What are accuracy, precision, and recall?

### Answer:

Accuracy: Overall correct predictions.

Precision: Out of predicted positives, how many are correct.

Recall: Out of actual positives, how many were found.

------------------------------------------------------------------------

## Q25. What is hallucination in AI?

### Answer:

Hallucination occurs when an AI model generates incorrect information
confidently.

Solutions: - RAG - Better prompts - Evaluation systems - Grounding with
trusted data

------------------------------------------------------------------------

# Important Topics To Revise Before Bruviti

Priority:

1.  AI Agents
2.  LLM basics
3.  RAG
4.  Embeddings
5.  Vector databases
6.  Machine Learning fundamentals
7.  NLP
8.  Computer Vision
9.  Knowledge graphs
10. Enterprise AI architecture
