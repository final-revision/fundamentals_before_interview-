# Bruviti AI — Technical Assessment Preparation
## AI/ML, Edge Computing, Cloud, IoT, Computer Science & Bruviti-Focused Q&A

> Purpose: Technical written-assessment preparation for Bruviti AI campus placement.
> Scope: Conceptual technical questions and answers only. No coding questions and no HR questions.

---

# 1. Bruviti — Technology You Should Understand

## Q1. What does Bruviti do?

**Answer:**
Bruviti is a technology company focused on **edge computing, IoT, data processing, AI/ML, and cloud-connected business solutions**. Its technology is designed to bring computation and intelligence closer to where data is generated, while also connecting devices, applications, and cloud systems.

The important concepts to understand for a technical assessment are:

- Edge computing
- IoT and connected devices
- AI/ML at or near the edge
- Cloud computing
- Real-time data processing
- Data security
- Distributed systems
- APIs and system integration
- Automation and intelligent decision-making

---

## Q2. What is edge computing?

**Answer:**
Edge computing is a computing architecture in which data is processed **near the location where it is generated**, instead of sending every piece of data to a distant cloud server.

### Example:
A factory camera detects a defective product.

- Traditional cloud approach: Camera → Internet → Cloud → Analysis → Response
- Edge approach: Camera → Edge device → Analysis → Immediate response

### Main advantages:
- Lower latency
- Faster decisions
- Reduced bandwidth usage
- Better operation when internet connectivity is poor
- Improved privacy for some workloads

---

## Q3. What is the difference between edge computing and cloud computing?

| Edge Computing | Cloud Computing |
|---|---|
| Processing happens near the data source | Processing happens in centralized data centers |
| Very low latency | Usually higher latency |
| Useful for real-time decisions | Useful for large-scale processing/storage |
| Can reduce network traffic | Requires data transmission to cloud |
| Useful for IoT and industrial systems | Useful for centralized applications |

A modern system often uses **both edge and cloud**, rather than choosing only one.

---

# 2. Artificial Intelligence

## Q4. What is Artificial Intelligence?

**Answer:**
Artificial Intelligence is the field of computer science concerned with building systems that can perform tasks that normally require human-like intelligence, such as:

- Reasoning
- Learning
- Pattern recognition
- Prediction
- Decision-making
- Natural language understanding
- Computer vision

---

## Q5. What is Machine Learning?

**Answer:**
Machine Learning is a subset of AI in which a system learns patterns from data and uses those patterns to make predictions or decisions.

### Example:
A system receives historical machine sensor data:

`temperature + vibration + pressure → machine failure`

After training, it can predict whether a new machine state is likely to result in failure.

---

## Q6. What are the major types of Machine Learning?

**Answer:**

### 1. Supervised Learning
The training data contains input and known output/labels.

Examples:
- Classification
- Regression

### 2. Unsupervised Learning
The data does not contain target labels.

Examples:
- Clustering
- Dimensionality reduction

### 3. Reinforcement Learning
An agent learns by interacting with an environment and receiving rewards or penalties.

---

# 3. Supervised Learning

## Q7. What is classification?

**Answer:**
Classification predicts a **discrete category/class**.

Examples:
- Spam / Not Spam
- Defective / Non-defective
- Fraud / Not Fraud
- Normal / Abnormal

---

## Q8. What is regression?

**Answer:**
Regression predicts a **continuous numerical value**.

Examples:
- Temperature prediction
- Sales prediction
- House price prediction
- Energy consumption prediction

---

## Q9. Classification vs Regression

| Classification | Regression |
|---|---|
| Predicts categories | Predicts numerical values |
| Output is discrete | Output is continuous |
| Example: spam/not spam | Example: price prediction |

---

# 4. Common ML Algorithms

## Q10. What is Linear Regression?

**Answer:**
Linear Regression models the relationship between input variables and a continuous output using a linear equation.

A simple form is:

`y = mx + c`

It is commonly used for regression problems.

---

## Q11. What is Logistic Regression?

**Answer:**
Logistic Regression is mainly used for classification. It estimates the probability of an observation belonging to a class.

The **sigmoid function** maps values to a range between 0 and 1.

---

## Q12. What is a Decision Tree?

**Answer:**
A Decision Tree makes predictions by repeatedly splitting data according to feature-based conditions.

Example:

`Temperature > threshold?`
→ Yes → High risk  
→ No → Low risk

Decision trees can be used for both classification and regression.

---

## Q13. What is Random Forest?

**Answer:**
Random Forest is an ensemble learning algorithm that combines multiple decision trees.

For classification, the trees generally vote for a class.

### Advantages:
- Good performance
- Handles nonlinear relationships
- Less prone to overfitting than a single decision tree
- Works with many types of features

---

## Q14. What is K-Nearest Neighbors (KNN)?

**Answer:**
KNN predicts a sample based on the classes or values of its nearest neighboring training examples.

The value of **K** represents the number of neighbors considered.

---

## Q15. What is SVM?

**Answer:**
Support Vector Machine finds a decision boundary that separates classes while attempting to maximize the margin between them.

SVM can also use kernels to handle nonlinear relationships.

---

## Q16. What is clustering?

**Answer:**
Clustering is an unsupervised learning technique that groups similar data points together.

Example:
A company can group customers based on purchasing behavior without predefined customer categories.

---

## Q17. What is K-Means clustering?

**Answer:**
K-Means divides data into K clusters.

General process:

1. Choose K
2. Initialize cluster centroids
3. Assign points to the nearest centroid
4. Recalculate centroids
5. Repeat until the clusters stabilize

---

# 5. Neural Networks

## Q18. What is an Artificial Neural Network?

**Answer:**
An Artificial Neural Network (ANN) is a machine learning model inspired by the structure of biological neural networks.

It generally contains:

- Input layer
- Hidden layer(s)
- Output layer

Each neuron applies weights, bias, and an activation function to its inputs.

---

## Q19. What is an activation function?

**Answer:**
An activation function introduces non-linearity into a neural network.

Common activation functions:

- ReLU
- Sigmoid
- Tanh
- Softmax

Without suitable nonlinear activation functions, deep neural networks would have limited ability to learn complex nonlinear relationships.

---

## Q20. What is ReLU?

**Answer:**
ReLU stands for Rectified Linear Unit.

`ReLU(x) = max(0, x)`

It outputs zero for negative inputs and the input itself for positive values.

It is widely used in hidden layers of neural networks.

---

## Q21. What is Softmax?

**Answer:**
Softmax converts a vector of scores into probabilities whose values sum to 1.

It is commonly used in the output layer of a multiclass classification neural network.

---

## Q22. What is backpropagation?

**Answer:**
Backpropagation is a method used to calculate how much each network parameter contributed to the prediction error.

The calculated gradients are then used by an optimization algorithm such as gradient descent to update the weights.

---

## Q23. What is an epoch?

**Answer:**
One epoch means that the model has processed the entire training dataset once.

---

## Q24. What is batch size?

**Answer:**
Batch size is the number of training samples processed before the model updates its parameters.

---

# 6. Deep Learning

## Q25. What is Deep Learning?

**Answer:**
Deep Learning is a subset of Machine Learning that uses neural networks with multiple layers to learn complex representations from data.

It is widely used in:

- Computer vision
- Speech recognition
- NLP
- Recommendation systems
- Generative AI

---

## Q26. What is CNN?

**Answer:**
CNN stands for Convolutional Neural Network.

It is especially useful for image and spatial data because convolution operations can learn local patterns such as:

- Edges
- Textures
- Shapes
- Objects

---

## Q27. What is RNN?

**Answer:**
Recurrent Neural Network is a neural network architecture designed for sequential data.

Applications include:

- Time-series data
- Text
- Speech
- Sequence prediction

---

## Q28. What is LSTM?

**Answer:**
LSTM stands for Long Short-Term Memory.

It is a type of recurrent neural network designed to better preserve useful information over longer sequences and reduce the limitations associated with traditional RNNs.

---

# 7. Generative AI & LLM Basics

## Q29. What is Generative AI?

**Answer:**
Generative AI refers to AI systems that can generate new content based on learned patterns.

Examples:
- Text
- Images
- Audio
- Code
- Video

---

## Q30. What is an LLM?

**Answer:**
LLM stands for Large Language Model.

It is a neural network trained on large amounts of text to learn patterns in language and generate or transform text.

Examples of tasks:
- Question answering
- Summarization
- Translation
- Text generation

---

## Q31. What is a Transformer?

**Answer:**
A Transformer is a neural network architecture based heavily on attention mechanisms.

It is widely used in modern NLP and large language models.

---

## Q32. What is attention?

**Answer:**
Attention allows a model to assign different importance to different parts of an input when processing information.

This helps the model understand relationships between tokens, including relationships between tokens that are far apart in a sequence.

---

## Q33. What is an AI model at the edge?

**Answer:**
An AI model at the edge is deployed on or near the device generating data instead of relying entirely on a remote cloud service.

Examples:
- Camera detecting objects locally
- Industrial device detecting abnormal vibration
- Smart sensor predicting equipment failure

---

# 8. Edge AI

## Q34. What is Edge AI?

**Answer:**
Edge AI combines **AI/ML with edge computing**.

Instead of sending all raw data to the cloud, an AI model can run near the data source.

### Example:

`Sensor → Edge Device → ML Model → Decision`

The cloud may then receive only important results or summaries.

---

## Q35. Why is Edge AI useful?

**Answer:**

1. Low latency
2. Faster response
3. Reduced bandwidth
4. Better privacy for certain applications
5. Less dependence on continuous cloud connectivity
6. Suitable for real-time systems

---

## Q36. What are the challenges of Edge AI?

**Answer:**

- Limited CPU/GPU resources
- Limited memory
- Energy constraints
- Model size
- Model optimization
- Device management
- Security
- Updating models across many devices

---

## Q37. How can an ML model be optimized for edge deployment?

**Answer:**

Common techniques include:

- Quantization
- Pruning
- Knowledge distillation
- Smaller architectures
- Hardware acceleration
- Efficient inference runtimes

---

## Q38. What is model quantization?

**Answer:**
Quantization reduces the numerical precision used by a model.

For example, a model may use lower-precision representations instead of full 32-bit floating-point values.

Potential benefits:

- Smaller model size
- Lower memory usage
- Faster inference
- Lower power consumption

There can be a trade-off involving model accuracy.

---

## Q39. What is model pruning?

**Answer:**
Pruning removes less important parameters or connections from a neural network to reduce model complexity.

---

# 9. IoT

## Q40. What is IoT?

**Answer:**
IoT stands for Internet of Things.

It refers to physical devices equipped with sensors, software, processing capability, and connectivity that can collect and exchange data.

Examples:

- Smart meters
- Industrial sensors
- Smart cameras
- Wearable devices
- Connected machines

---

## Q41. What is the basic architecture of an IoT system?

**Answer:**

`Sensors → Edge/Gateway → Network → Cloud/Server → Application`

Depending on the system, processing can happen at multiple stages.

---

## Q42. What is a sensor?

**Answer:**
A sensor detects a physical quantity and converts it into a measurable signal.

Examples:

- Temperature sensor
- Pressure sensor
- Motion sensor
- Humidity sensor
- Vibration sensor

---

## Q43. What is an actuator?

**Answer:**
An actuator converts a control signal into physical action.

Examples:

- Motor
- Relay
- Valve
- Servo motor

---

## Q44. Sensor vs Actuator

**Answer:**

- **Sensor:** observes the physical environment.
- **Actuator:** performs an action in the physical environment.

---

# 10. IoT Communication Protocols

## Q45. What is MQTT?

**Answer:**
MQTT is a lightweight messaging protocol commonly used in IoT.

It follows a **publish-subscribe** communication model.

Components:

- Publisher
- Broker
- Subscriber

Example:

`Temperature Sensor → MQTT Broker → Monitoring Application`

---

## Q46. Why is MQTT suitable for IoT?

**Answer:**

- Lightweight
- Low bandwidth requirements
- Supports unreliable networks
- Publish-subscribe architecture
- Suitable for resource-constrained devices

---

## Q47. What is HTTP?

**Answer:**
HTTP is a request-response application-layer protocol widely used for communication between web clients and servers.

Example:

`Client → HTTP Request → Server → HTTP Response`

---

## Q48. MQTT vs HTTP

| MQTT | HTTP |
|---|---|
| Publish/Subscribe | Request/Response |
| Lightweight | Relatively heavier |
| Common in IoT | Common in web applications |
| Broker-based | Client-server |
| Good for continuous messaging | Good for web APIs |

---

# 11. Cloud Computing

## Q49. What is Cloud Computing?

**Answer:**
Cloud computing provides computing resources such as:

- Servers
- Storage
- Databases
- Networking
- AI/ML infrastructure

over a network, typically with scalable resource allocation.

---

## Q50. What are IaaS, PaaS and SaaS?

**Answer:**

### IaaS — Infrastructure as a Service
Provides infrastructure such as virtual machines, storage, and networking.

### PaaS — Platform as a Service
Provides a platform for developing and deploying applications.

### SaaS — Software as a Service
Provides complete software applications to users.

---

## Q51. Why combine edge and cloud?

**Answer:**
Edge and cloud complement each other.

### Edge:
- Real-time processing
- Local decisions
- Reduced bandwidth

### Cloud:
- Large-scale storage
- Centralized analytics
- Model training
- Device management
- Long-term data analysis

A common architecture is:

`Device → Edge Processing → Cloud → Analytics/Dashboard`

---

# 12. Distributed Systems

## Q52. What is a distributed system?

**Answer:**
A distributed system consists of multiple computing components that communicate over a network and work together to provide a service.

Edge-cloud architectures are examples of distributed computing environments.

---

## Q53. What is latency?

**Answer:**
Latency is the time taken between sending a request/data and receiving a response/result.

For real-time systems, lower latency is generally important.

---

## Q54. What is bandwidth?

**Answer:**
Bandwidth refers to the amount of data that a communication channel can transmit over a given period.

---

## Q55. Latency vs Bandwidth

**Answer:**

- **Latency:** How long data takes to travel/respond.
- **Bandwidth:** How much data can be transferred per unit time.

A network can have high bandwidth but still have high latency.

---

# 13. Databases & Data

## Q56. What is a database?

**Answer:**
A database is an organized collection of data that can be stored, managed, retrieved, and updated efficiently.

---

## Q57. SQL vs NoSQL

| SQL | NoSQL |
|---|---|
| Relational | Non-relational |
| Tables and relationships | Documents/key-value/graphs/etc. |
| Usually structured schema | Often flexible schema |
| Strong relational querying | Useful for flexible/scalable data models |

---

## Q58. Why can NoSQL be useful for IoT?

**Answer:**
IoT systems can generate large volumes of rapidly changing and heterogeneous data. Some NoSQL databases can provide flexible schemas and horizontal scalability that fit particular IoT workloads.

The correct database depends on the application's requirements.

---

## Q59. What is real-time data processing?

**Answer:**
Real-time data processing means analyzing or acting on data with very small delay after the data is generated.

Example:

`Sensor → Edge Processing → Detect abnormal condition → Alert`

---

# 14. Data Preprocessing

## Q60. Why is data preprocessing important?

**Answer:**
Raw data may contain:

- Missing values
- Noise
- Outliers
- Duplicate records
- Different scales
- Incorrect values

Preprocessing improves the quality and usefulness of data for machine learning.

---

## Q61. What is feature scaling?

**Answer:**
Feature scaling transforms numerical features to comparable scales.

Common methods:

- Standardization
- Min-Max normalization

---

## Q62. What is normalization?

**Answer:**
Normalization commonly refers to transforming values to a fixed range, often 0 to 1.

---

## Q63. What is standardization?

**Answer:**
Standardization transforms a feature so that it has approximately:

- Mean = 0
- Standard deviation = 1

---

## Q64. What is an outlier?

**Answer:**
An outlier is an observation that differs significantly from the general pattern of the data.

Outliers may represent:

- Measurement errors
- Rare events
- Genuine unusual behavior

They should not automatically be deleted.

---

# 15. Model Evaluation

## Q65. What is training data?

**Answer:**
Training data is used by a machine learning algorithm to learn model parameters/patterns.

---

## Q66. What is test data?

**Answer:**
Test data is used to evaluate how well the trained model performs on previously unseen data.

---

## Q67. What is validation data?

**Answer:**
Validation data is used during model development for tasks such as hyperparameter selection and model comparison.

---

## Q68. What is overfitting?

**Answer:**
Overfitting occurs when a model learns the training data too closely, including noise or accidental patterns, and performs poorly on unseen data.

---

## Q69. What is underfitting?

**Answer:**
Underfitting occurs when a model is too simple to capture important patterns in the data.

---

## Q70. Overfitting vs Underfitting

| Overfitting | Underfitting |
|---|---|
| Model too complex for available data | Model too simple |
| Very good training performance | Poor training performance |
| Poor generalization | Poor training and generalization |

---

# 16. Classification Metrics

## Q71. What is a confusion matrix?

**Answer:**
A confusion matrix summarizes classification predictions using:

- True Positive (TP)
- True Negative (TN)
- False Positive (FP)
- False Negative (FN)

---

## Q72. What is accuracy?

**Answer:**

`Accuracy = (TP + TN) / (TP + TN + FP + FN)`

It represents the proportion of total predictions that are correct.

---

## Q73. What is precision?

**Answer:**

`Precision = TP / (TP + FP)`

Precision answers:

**Of the instances predicted as positive, how many were actually positive?**

---

## Q74. What is recall?

**Answer:**

`Recall = TP / (TP + FN)`

Recall answers:

**Of all actual positive instances, how many did the model identify?**

---

## Q75. What is F1-score?

**Answer:**
F1-score is the harmonic mean of precision and recall.

`F1 = 2 × Precision × Recall / (Precision + Recall)`

It is useful when both precision and recall matter.

---

# 17. AI/ML Concepts Frequently Tested

## Q76. What is a feature?

**Answer:**
A feature is an input variable used by a machine learning model.

Example:

For predicting machine failure:

- Temperature
- Vibration
- Pressure
- Operating time

can be features.

---

## Q77. What is a label?

**Answer:**
A label is the target output associated with a training example in supervised learning.

Example:

`Temperature + Vibration → Failure`

Here, **Failure** is the label.

---

## Q78. What is a parameter?

**Answer:**
A parameter is a value learned by the model during training.

For a neural network, weights and biases are examples of parameters.

---

## Q79. What is a hyperparameter?

**Answer:**
A hyperparameter is a configuration value selected before or during model training rather than directly learned from the training data.

Examples:

- Learning rate
- Number of trees
- K in KNN
- Batch size
- Number of epochs

---

## Q80. What is gradient descent?

**Answer:**
Gradient descent is an optimization algorithm used to minimize a loss function by iteratively updating model parameters in the direction that reduces the loss.

---

## Q81. What is a loss function?

**Answer:**
A loss function measures the difference between the model's prediction and the expected target.

Training attempts to minimize this loss.

---

# 18. Computer Vision

## Q82. What is Computer Vision?

**Answer:**
Computer Vision enables computers to extract meaningful information from images and videos.

Applications:

- Object detection
- Image classification
- Face detection
- Quality inspection
- OCR
- Surveillance
- Industrial automation

---

## Q83. Image classification vs object detection

**Answer:**

### Image Classification
Determines what category an image belongs to.

### Object Detection
Identifies objects and their locations, usually using bounding boxes.

Example:

An image may contain three objects. Object detection can identify all three and locate them.

---

# 19. Cybersecurity & Edge Security

## Q84. Why is security important in IoT?

**Answer:**
IoT devices interact with physical environments and may collect sensitive or operational data.

Security risks include:

- Unauthorized access
- Device compromise
- Data interception
- Malware
- Fake devices
- Unauthorized commands

---

## Q85. What is encryption?

**Answer:**
Encryption converts readable information into a protected form so that unauthorized parties cannot easily understand it.

---

## Q86. What is authentication?

**Answer:**
Authentication verifies **who** a user or device is.

---

## Q87. What is authorization?

**Answer:**
Authorization determines **what an authenticated user or device is allowed to do**.

---

## Q88. Authentication vs Authorization

**Answer:**

- Authentication → **Who are you?**
- Authorization → **What are you allowed to access/do?**

---

# 20. APIs and System Integration

## Q89. What is an API?

**Answer:**
API stands for Application Programming Interface.

It provides a defined way for different software components to communicate.

Example:

`Edge Device → API → Cloud Service`

---

## Q90. What is REST API?

**Answer:**
A REST API is an API style commonly used for communication over HTTP.

Common HTTP methods:

- GET — retrieve
- POST — create/send
- PUT/PATCH — update
- DELETE — remove

---

# 21. Edge Architecture — Important Scenario Questions

## Q91. A sensor generates thousands of readings every second. Should all data be sent to the cloud?

**Answer:**
Not necessarily.

An edge device can preprocess the data and send only:

- Important events
- Aggregated data
- Alerts
- Relevant measurements

This can reduce bandwidth usage and cloud processing requirements.

---

## Q92. Why would a company process AI locally instead of in the cloud?

**Answer:**
Possible reasons include:

- Lower latency
- Privacy requirements
- Reduced bandwidth
- Faster local decisions
- Intermittent connectivity
- Operational reliability

---

## Q93. What happens if an edge device loses internet connectivity?

**Answer:**
A well-designed edge system can continue performing local processing and decision-making for supported functions.

It can later synchronize data with the cloud when connectivity is restored.

This is one of the important advantages of edge architectures.

---

## Q94. An industrial machine suddenly starts vibrating abnormally. How could Edge AI help?

**Answer:**

`Vibration Sensor`
→ `Edge Device`
→ `Data Preprocessing`
→ `ML Model`
→ `Anomaly Detection`
→ `Immediate Alert`

The edge device can make the initial decision without waiting for a round trip to the cloud.

---

## Q95. How can Edge AI and cloud AI work together?

**Answer:**

### Edge:
- Data filtering
- Real-time inference
- Immediate alerts
- Local decisions

### Cloud:
- Store historical data
- Train/retrain models
- Perform large-scale analytics
- Manage devices
- Monitor system performance

Architecture:

`IoT Device → Edge AI → Cloud → Analytics/Model Training`

---

# 22. Scenario-Based Questions Likely to Test Understanding

## Q96. A company has cameras in a factory and wants to detect defective products immediately. What technology would you suggest?

**Answer:**
A possible solution is **Edge AI with Computer Vision**.

The camera can send frames to an edge device where a trained vision model performs inference locally.

This provides low-latency detection and reduces the need to continuously transmit raw video to the cloud.

---

## Q97. A smart device has limited RAM and CPU. What should you consider before deploying an ML model?

**Answer:**

- Model size
- RAM usage
- CPU requirements
- Inference latency
- Power consumption
- Quantization
- Pruning
- Hardware acceleration
- Required accuracy

---

## Q98. An ML model performs 99% accuracy on training data but only 72% on test data. What could be the problem?

**Answer:**
A likely issue is **overfitting**.

The model may have learned training-specific patterns that do not generalize well to unseen data.

---

## Q99. A fraud detection model misses many fraudulent transactions. Which metric should you examine?

**Answer:**
**Recall** is particularly important because it measures how many actual positive cases are detected.

However, precision and the business cost of false positives should also be considered.

---

## Q100. A medical/industrial warning system must avoid missing dangerous events. Which type of error is especially important?

**Answer:**
A **false negative** can be particularly important when missing a positive/dangerous event has high consequences.

This is why recall/sensitivity may be emphasized in such systems.

---

# 23. Important Technical Comparisons

## Q101. AI vs ML vs Deep Learning

**Answer:**

`Artificial Intelligence`
→ Broad field of intelligent systems

`Machine Learning`
→ Subfield of AI that learns patterns from data

`Deep Learning`
→ Subfield of ML using multilayer neural networks

---

## Q102. Edge Computing vs Edge AI

**Answer:**

- Edge Computing = processing data near the source.
- Edge AI = running AI/ML inference near the source.

Edge computing does not necessarily require AI.

---

## Q103. IoT vs Edge Computing

**Answer:**

- IoT focuses on connected physical devices and data exchange.
- Edge computing focuses on processing data near where it is generated.

They are often used together.

---

## Q104. Cloud AI vs Edge AI

**Answer:**

| Cloud AI | Edge AI |
|---|---|
| Model runs in cloud infrastructure | Model runs near data source |
| Requires network communication for cloud inference | Can operate locally |
| Large compute resources available | Resource constrained |
| Useful for large-scale processing | Useful for real-time/local decisions |

---

# 24. High-Priority Topics to Revise

Before the Bruviti technical assessment, revise these in this order:

### Priority 1 — Very Important
1. Edge Computing
2. Edge AI
3. IoT
4. Cloud vs Edge
5. AI vs ML vs Deep Learning
6. Supervised/Unsupervised/Reinforcement Learning
7. Classification vs Regression
8. Neural Networks
9. Computer Vision
10. ML model deployment

### Priority 2 — Important
11. MQTT
12. HTTP
13. Sensors and Actuators
14. Latency and Bandwidth
15. Real-time processing
16. Model optimization
17. Quantization
18. Overfitting/Underfitting
19. Precision/Recall/F1
20. Training/Validation/Test datasets

### Priority 3 — Revise if Time Allows
21. CNN
22. RNN/LSTM
23. Transformers
24. LLM basics
25. REST APIs
26. SQL vs NoSQL
27. Authentication/Authorization
28. Distributed systems
29. Cybersecurity
30. Data preprocessing

---

# 25. Rapid-Fire One-Line Questions

### Q: What is AI?
**A:** Technology for building systems capable of tasks associated with intelligent behavior.

### Q: What is ML?
**A:** A method where systems learn patterns from data.

### Q: What is Deep Learning?
**A:** ML based on multilayer neural networks.

### Q: What is Edge Computing?
**A:** Processing data near its source.

### Q: What is Edge AI?
**A:** Running AI/ML inference near the data source.

### Q: What is IoT?
**A:** Networked physical devices that collect, exchange, and/or act on data.

### Q: What is MQTT?
**A:** Lightweight publish-subscribe messaging protocol commonly used in IoT.

### Q: What is latency?
**A:** Time delay between an action/request and its response.

### Q: What is bandwidth?
**A:** Data-carrying capacity of a communication channel.

### Q: What is overfitting?
**A:** Learning training-specific patterns too closely and generalizing poorly.

### Q: What is underfitting?
**A:** Failing to learn important patterns because the model is too simple.

### Q: What is inference?
**A:** Using a trained model to generate predictions on new data.

### Q: What is quantization?
**A:** Reducing numerical precision to make models more efficient.

### Q: What is a sensor?
**A:** Device that measures a physical quantity.

### Q: What is an actuator?
**A:** Device that performs a physical action based on a control signal.

### Q: What is CNN?
**A:** Neural network architecture widely used for image/spatial data.

### Q: What is an API?
**A:** Interface that allows software components to communicate.

### Q: What is cloud computing?
**A:** On-demand computing resources delivered over a network.

### Q: What is a model?
**A:** A learned mathematical/computational representation used for prediction or decision-making.

### Q: What is a feature?
**A:** Input variable used by an ML model.

### Q: What is a label?
**A:** Target output in supervised learning.

---

# 26. Final Bruviti-Focused Revision Checklist

Before entering the written assessment, you should be able to explain these without memorizing long definitions:

- [ ] What Bruviti's technology domain is
- [ ] What edge computing means
- [ ] Why edge computing is useful
- [ ] Edge vs cloud
- [ ] What Edge AI means
- [ ] Why AI can be deployed at the edge
- [ ] IoT architecture
- [ ] Sensors and actuators
- [ ] MQTT
- [ ] HTTP
- [ ] Latency
- [ ] Bandwidth
- [ ] Real-time processing
- [ ] AI vs ML vs Deep Learning
- [ ] Supervised vs unsupervised learning
- [ ] Classification vs regression
- [ ] ANN
- [ ] CNN
- [ ] RNN/LSTM
- [ ] Transformer basics
- [ ] Training/validation/test data
- [ ] Overfitting and underfitting
- [ ] Accuracy, precision, recall, F1
- [ ] Loss function
- [ ] Gradient descent
- [ ] Features and labels
- [ ] Parameters and hyperparameters
- [ ] Model inference
- [ ] Quantization
- [ ] Pruning
- [ ] Cloud + Edge architecture
- [ ] AI model deployment constraints
- [ ] IoT security
- [ ] Authentication vs authorization
- [ ] REST API basics
- [ ] SQL vs NoSQL
- [ ] Computer vision basics
- [ ] Scenario-based Edge AI questions

---

# 27. Most Important Conceptual Questions to Practice

If the assessment contains conceptual/scenario-based questions, practice answering these first:

1. Why is edge computing required when cloud computing already exists?
2. How does Edge AI reduce latency?
3. What happens when an edge device loses internet connectivity?
4. Why should all IoT data not necessarily be sent to the cloud?
5. How would you deploy an ML model on a resource-constrained device?
6. What is the difference between training and inference?
7. What is the difference between Edge AI and Cloud AI?
8. Why is quantization useful for edge devices?
9. How can computer vision be used in industrial environments?
10. How can IoT sensors and ML be combined for predictive maintenance?
11. Why is MQTT commonly used in IoT?
12. What is the difference between latency and bandwidth?
13. How would you handle an ML model that overfits?
14. When is recall more important than accuracy?
15. How do edge and cloud systems work together?
16. What are the security challenges of connected edge devices?
17. What is the difference between a sensor and an actuator?
18. What is the role of an edge gateway?
19. What factors should be considered before selecting an ML model for edge deployment?
20. What is the difference between AI, ML, Deep Learning, and Generative AI?

---

## Final Strategy

For Bruviti, do not prepare only generic AIML definitions.

Your preparation should connect:

**AI/ML + IoT + Edge Computing + Cloud + Real-Time Processing + Computer Vision + Model Deployment + Security**

The most useful mental model is:

`Physical Device/Sensor`
↓
`Edge Device / Gateway`
↓
`Local Processing / Edge AI`
↓
`Immediate Decision`
↓
`Cloud`
↓
`Storage + Analytics + Model Training + Monitoring`

Understand **why each component exists**, not just its definition. This is especially important for scenario-based technical questions.
