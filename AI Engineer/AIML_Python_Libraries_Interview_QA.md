# Python Libraries for AI/ML Engineer — Interview Q&A

A focused interview guide for the core Python libraries an AI/ML Engineer should know:

**NumPy → Pandas → Matplotlib → Scikit-learn → PyTorch → Hugging Face Transformers → Requests**

---

# 1. NumPy

## Q1. What is NumPy?

NumPy is a Python library for numerical computing. Its core data structure is the fast, multidimensional `ndarray`.

```text
Python
  ↓
NumPy
  ├── Arrays
  ├── Matrix operations
  ├── Mathematical operations
  └── Linear algebra
```

## Q2. NumPy array vs Python list?

| Python List | NumPy Array |
|---|---|
| General-purpose | Numerical computing |
| Can contain mixed types | Usually homogeneous |
| Slower for large numerical operations | Fast/vectorized |
| More general | Memory-efficient for numerical data |

```python
import numpy as np

a = [1, 2, 3]
b = np.array([1, 2, 3])

print(b * 2)
# [2 4 6]
```

## Q3. What is vectorization?

Vectorization means performing operations on entire arrays instead of explicitly looping through individual elements.

```python
import numpy as np

x = np.array([1, 2, 3, 4])
y = x * 10

print(y)
# [10 20 30 40]
```

## Q4. What is broadcasting?

Broadcasting allows NumPy to perform operations between arrays of compatible shapes.

```python
import numpy as np

x = np.array([1, 2, 3])
print(x + 10)

# [11 12 13]
```

Conceptually:

```text
[1, 2, 3]
   +
[10,10,10]
   ↓
[11,12,13]
```

## Q5. Important NumPy concepts

Know:

- `np.array()`
- `shape`
- `ndim`
- `dtype`
- `reshape()`
- `flatten()`
- Indexing/slicing
- `mean()`
- `median()`
- `std()`
- `sum()`
- `min()`
- `max()`
- Broadcasting
- Vectorization
- Random number generation

---

# 2. Pandas

## Q6. What is Pandas?

Pandas is a Python library used for data manipulation, cleaning, analysis, and working with tabular data.

Main structures:

```text
Pandas
├── Series       → 1D
└── DataFrame    → 2D table
```

## Q7. What is a DataFrame?

A DataFrame is a two-dimensional labeled data structure similar to a spreadsheet or database table.

```python
import pandas as pd

data = {
    "name": ["A", "B", "C"],
    "age": [20, 25, 30]
}

df = pd.DataFrame(data)

print(df)
```

## Q8. How do you inspect a dataset?

```python
df.head()
df.tail()
df.shape
df.columns
df.info()
df.describe()
df.dtypes
```

## Q9. How do you handle missing values?

```python
df.isnull().sum()

df.dropna()

df.fillna(0)

df["age"] = df["age"].fillna(df["age"].median())
```

**Interview point:** Do not blindly fill every missing value with zero. Choose the strategy based on the meaning and pattern of missingness.

## Q10. How do you filter data?

```python
df[df["age"] > 25]
```

Multiple conditions:

```python
df[(df["age"] > 25) & (df["salary"] > 50000)]
```

## Q11. What is `groupby()`?

`groupby()` is used to split data into groups and calculate aggregate statistics.

```python
df.groupby("department")["salary"].mean()
```

## Q12. How do you remove duplicate rows?

```python
df.drop_duplicates()
```

## Q13. How do you merge DataFrames?

```python
result = pd.merge(
    customers,
    orders,
    on="customer_id",
    how="inner"
)
```

Common join types:

- `inner`
- `left`
- `right`
- `outer`

## Q14. Important Pandas concepts

Know:

- `Series`
- `DataFrame`
- `read_csv()`
- `read_excel()`
- `head()`
- `info()`
- `describe()`
- `loc`
- `iloc`
- Filtering
- Sorting
- Missing values
- Duplicates
- `groupby()`
- `merge()`
- `concat()`
- `apply()`
- Datetime operations

---

# 3. Matplotlib

## Q15. What is Matplotlib?

Matplotlib is a Python visualization library used to create charts and graphs.

```text
Data
 ↓
Matplotlib
 ↓
Visualization
 ├── Line
 ├── Bar
 ├── Scatter
 ├── Histogram
 └── Pie
```

## Q16. Create a basic line chart.

```python
import matplotlib.pyplot as plt

x = [1, 2, 3, 4]
y = [10, 20, 15, 30]

plt.plot(x, y)
plt.xlabel("X")
plt.ylabel("Y")
plt.title("Example")
plt.show()
```

## Q17. What is a histogram?

A histogram shows the distribution of numerical values.

```python
plt.hist(df["age"])
plt.xlabel("Age")
plt.ylabel("Frequency")
plt.show()
```

Useful for understanding:
- Distribution
- Skewness
- Spread
- Potential outliers

## Q18. Scatter plot vs line plot?

**Scatter plot:** Useful for examining relationships between two numerical variables.

**Line plot:** Useful for trends, especially ordered/time-series data.

```python
plt.scatter(df["age"], df["salary"])
plt.show()
```

## Q19. Why is visualization important in ML?

It can help identify:

- Outliers
- Class imbalance
- Distributions
- Correlations
- Trends
- Data-quality problems

---

# 4. Scikit-learn

## Q20. What is Scikit-learn?

Scikit-learn is one of the most important Python libraries for classical machine learning.

It provides:

- ML algorithms
- Preprocessing
- Model selection
- Metrics
- Pipelines
- Cross-validation

```text
Raw Data
   ↓
Preprocessing
   ↓
Feature Engineering
   ↓
Model
   ↓
Evaluation
   ↓
Prediction
```

## Q21. How do you train a simple ML model?

```python
from sklearn.model_selection import train_test_split
from sklearn.linear_model import LinearRegression

X = df[["age", "experience"]]
y = df["salary"]

X_train, X_test, y_train, y_test = train_test_split(
    X, y, test_size=0.2, random_state=42
)

model = LinearRegression()
model.fit(X_train, y_train)

predictions = model.predict(X_test)
```

## Q22. What is `fit()`?

`fit()` trains the model on the provided training data.

```python
model.fit(X_train, y_train)
```

## Q23. What is `predict()`?

`predict()` generates predictions using a trained model.

```python
model.predict(X_test)
```

## Q24. What is `transform()`?

`transform()` applies a learned or predefined transformation to data.

Example:

```python
scaler.fit(X_train)
X_train_scaled = scaler.transform(X_train)
```

Often you will see:

```python
X_train_scaled = scaler.fit_transform(X_train)
X_test_scaled = scaler.transform(X_test)
```

**Important:** Fit preprocessing on training data, then transform validation/test data. This helps prevent data leakage.

## Q25. What is StandardScaler?

It standardizes features approximately to zero mean and unit variance.

```python
from sklearn.preprocessing import StandardScaler

scaler = StandardScaler()

X_train_scaled = scaler.fit_transform(X_train)
X_test_scaled = scaler.transform(X_test)
```

## Q26. What is OneHotEncoder?

It converts categorical values into binary indicator features.

```python
from sklearn.preprocessing import OneHotEncoder

encoder = OneHotEncoder(handle_unknown="ignore")
```

## Q27. What is a Pipeline?

A Pipeline chains preprocessing and a model into one workflow.

```python
from sklearn.pipeline import Pipeline
from sklearn.preprocessing import StandardScaler
from sklearn.linear_model import LogisticRegression

pipeline = Pipeline([
    ("scaler", StandardScaler()),
    ("model", LogisticRegression())
])

pipeline.fit(X_train, y_train)
predictions = pipeline.predict(X_test)
```

Concept:

```text
Input
  ↓
Scaler
  ↓
Model
  ↓
Prediction
```

Pipelines help keep preprocessing consistent and reduce leakage mistakes.

## Q28. What ML algorithms should you know in Scikit-learn?

### Regression
- Linear Regression
- Ridge
- Lasso
- Random Forest Regressor
- Gradient Boosting Regressor

### Classification
- Logistic Regression
- Decision Tree
- Random Forest
- SVM
- KNN
- Gradient Boosting

### Unsupervised Learning
- K-Means
- DBSCAN
- PCA

## Q29. How do you evaluate classification?

```python
from sklearn.metrics import (
    accuracy_score,
    precision_score,
    recall_score,
    f1_score
)

print(accuracy_score(y_test, predictions))
print(precision_score(y_test, predictions))
print(recall_score(y_test, predictions))
print(f1_score(y_test, predictions))
```

## Q30. What is train_test_split?

It separates data into training and testing subsets.

```python
X_train, X_test, y_train, y_test = train_test_split(
    X, y, test_size=0.2, random_state=42
)
```

## Q31. What is cross-validation?

It evaluates a model across multiple training/validation splits.

```python
from sklearn.model_selection import cross_val_score

scores = cross_val_score(
    model,
    X,
    y,
    cv=5
)

print(scores.mean())
```

---

# 5. PyTorch

## Q32. What is PyTorch?

PyTorch is a deep-learning framework used to build, train, and deploy neural networks.

```text
Data
 ↓
Tensor
 ↓
Neural Network
 ↓
Forward Pass
 ↓
Loss
 ↓
Backpropagation
 ↓
Optimizer
 ↓
Updated Weights
```

## Q33. What is a Tensor?

A Tensor is a multidimensional numerical data structure used heavily in deep learning.

```python
import torch

x = torch.tensor([
    [1, 2],
    [3, 4]
])

print(x.shape)
# torch.Size([2, 2])
```

Conceptually:

```text
Scalar → Vector → Matrix → Tensor
  1       [1,2]    [[1,2],
                     [3,4]]
```

## Q34. NumPy array vs PyTorch Tensor?

Both support multidimensional numerical data, but PyTorch tensors are designed for deep learning and can participate in automatic differentiation and accelerated computation on supported devices.

## Q35. What is `requires_grad=True`?

It tells PyTorch to track operations involving a tensor so gradients can be computed for it.

```python
x = torch.tensor(2.0, requires_grad=True)
```

## Q36. What is Autograd?

PyTorch's automatic differentiation system.

It automatically computes gradients needed for optimization.

```python
x = torch.tensor(2.0, requires_grad=True)

y = x ** 2
y.backward()

print(x.grad)
# tensor(4.)
```

Because:

```text
y = x²
dy/dx = 2x
at x=2 → 4
```

## Q37. What is `nn.Module`?

`torch.nn.Module` is the base class commonly used to define neural-network models.

```python
import torch.nn as nn

class SimpleModel(nn.Module):
    def __init__(self):
        super().__init__()
        self.layer = nn.Linear(10, 1)

    def forward(self, x):
        return self.layer(x)
```

## Q38. What is a forward pass?

The process of sending input through a neural network to produce an output.

```text
Input
 ↓
Layer 1
 ↓
Activation
 ↓
Layer 2
 ↓
Output
```

## Q39. What is backpropagation?

Backpropagation computes gradients of the loss with respect to model parameters using the chain rule.

```text
Prediction
    ↓
  Loss
    ↓
Backward()
    ↓
Gradients
    ↓
Optimizer
    ↓
New Weights
```

## Q40. What is an optimizer?

An optimizer updates model parameters using gradients.

Common optimizers:
- SGD
- Adam
- AdamW

Example:

```python
optimizer = torch.optim.Adam(
    model.parameters(),
    lr=0.001
)
```

## Q41. What is a loss function?

A function that measures how wrong the model prediction is.

Examples:

```python
nn.MSELoss()
nn.CrossEntropyLoss()
nn.BCELoss()
```

## Q42. Basic PyTorch training loop

```python
for epoch in range(epochs):

    optimizer.zero_grad()

    output = model(X_train)

    loss = criterion(output, y_train)

    loss.backward()

    optimizer.step()
```

Meaning:

```text
Clear old gradients
       ↓
Forward pass
       ↓
Calculate loss
       ↓
Backpropagation
       ↓
Update parameters
```

## Q43. What is `model.train()` vs `model.eval()`?

```python
model.train()
```

Sets training behavior.

```python
model.eval()
```

Sets evaluation/inference behavior.

This matters for layers such as Dropout and BatchNorm.

## Q44. What is `torch.no_grad()`?

It disables gradient tracking when gradients are unnecessary, such as normal inference.

```python
model.eval()

with torch.no_grad():
    predictions = model(X_test)
```

---

# 6. Hugging Face Transformers

## Q45. What is Hugging Face Transformers?

Transformers is a popular library providing pretrained transformer models and tools for NLP, LLM, vision, audio, and multimodal tasks.

Common ecosystem components include:

- `transformers`
- Tokenizers
- Model architectures
- Pretrained checkpoints
- Training/inference utilities

## Q46. What is a tokenizer?

A tokenizer converts raw text into tokens/IDs that a model can process.

```text
"AI is powerful"
       ↓
Tokenizer
       ↓
["AI", "is", "powerful"]
       ↓
Token IDs
       ↓
Model
```

Actual tokenization may split words into subword tokens.

## Q47. What is a pretrained model?

A model that has already been trained on a large dataset and can be reused for inference, fine-tuning, or further adaptation.

## Q48. Basic Hugging Face example

```python
from transformers import pipeline

classifier = pipeline("sentiment-analysis")

result = classifier("I love machine learning!")

print(result)
```

The pipeline handles several steps for you.

## Q49. What is the `pipeline()` API?

It provides a simple high-level interface for common ML/NLP tasks.

Examples:

```python
pipeline("sentiment-analysis")
pipeline("text-generation")
pipeline("summarization")
pipeline("translation")
pipeline("question-answering")
```

## Q50. How do you load a tokenizer and model?

```python
from transformers import AutoTokenizer, AutoModel

tokenizer = AutoTokenizer.from_pretrained(
    "model-name"
)

model = AutoModel.from_pretrained(
    "model-name"
)
```

For a specific task, a task-specific model class may be more appropriate.

## Q51. What is `AutoModel`?

`AutoModel` and related auto classes select an appropriate architecture/configuration based on a model checkpoint.

Examples:

```python
AutoTokenizer
AutoModel
AutoModelForSequenceClassification
AutoModelForCausalLM
```

## Q52. What is a causal language model?

A language model trained to predict the next token based on previous tokens.

```text
The cat is
     ↓
  "sleeping"
```

This is a common objective for generative LLMs.

## Q53. What is fine-tuning?

Fine-tuning continues training a pretrained model on a task/domain-specific dataset.

```text
Pretrained Model
      ↓
Task-specific Data
      ↓
Fine-tuning
      ↓
Specialized Model
```

---

# 7. Requests

## Q54. What is the Requests library?

Requests is a Python HTTP library used to communicate with web APIs and HTTP services.

```text
Python Application
       ↓
   HTTP Request
       ↓
      API
       ↓
 HTTP Response
       ↓
Python Application
```

## Q55. How do you make a GET request?

```python
import requests

response = requests.get(
    "https://api.example.com/users"
)

print(response.status_code)
print(response.json())
```

## Q56. GET vs POST?

**GET**
- Usually retrieves data.

**POST**
- Usually sends data to a server to create/process something.

```python
response = requests.post(
    "https://api.example.com/users",
    json={"name": "John"}
)
```

## Q57. Why use `timeout`?

Without a timeout, a request can potentially wait too long for a response.

```python
response = requests.get(
    url,
    timeout=10
)
```

## Q58. How do you handle HTTP errors?

```python
response = requests.get(url, timeout=10)

response.raise_for_status()

data = response.json()
```

`raise_for_status()` raises an exception for unsuccessful HTTP status codes.

## Q59. What are headers?

Headers carry additional HTTP metadata.

Example:

```python
headers = {
    "Authorization": "Bearer TOKEN",
    "Content-Type": "application/json"
}

response = requests.get(
    url,
    headers=headers,
    timeout=10
)
```

Never hard-code real API secrets in source code.

---

# 8. How These Libraries Work Together

A very common AI/ML workflow can look like:

```text
                 DATA SOURCE
                     │
                     ▼
                Requests
                     │
                     ▼
                  Pandas
              Data Cleaning
                     │
                     ▼
                  NumPy
            Numerical Operations
                     │
                     ▼
                Matplotlib
             Data Visualization
                     │
                     ▼
              Scikit-learn
          Classical ML / Preprocessing
                     │
                     ▼
                  PyTorch
              Deep Learning
                     │
                     ▼
          Hugging Face Transformers
                LLM / NLP
                     │
                     ▼
                 FastAPI/API
             Production Serving
```

---

# 9. Interview Scenario Questions

## Q60. You receive CSV data. What libraries would you use?

**Answer:**

```text
Pandas → Load and clean data
NumPy → Numerical operations
Matplotlib → Visualization
Scikit-learn → ML/preprocessing
```

Example:

```python
import pandas as pd

df = pd.read_csv("data.csv")

print(df.info())
print(df.describe())
```

## Q61. You need to build a house-price prediction model. Which library?

**Answer:** Scikit-learn is a good starting point for classical ML.

```text
Pandas
  ↓
Clean Data
  ↓
Scikit-learn
  ↓
Linear Regression / Random Forest
  ↓
Evaluation
```

## Q62. You need to build an image classifier. Which library?

**Answer:** PyTorch is a strong choice for deep learning, often combined with image/data libraries and pretrained models.

## Q63. You need to build a sentiment-analysis application using a pretrained LLM/NLP model.

**Answer:** Hugging Face Transformers is a strong choice.

```python
from transformers import pipeline

model = pipeline("sentiment-analysis")

print(model("This product is excellent!"))
```

## Q64. Your AI application needs to call an external REST API. Which library?

**Answer:** Requests is a simple choice for synchronous HTTP requests.

```python
import requests

response = requests.get(
    url,
    timeout=10
)

response.raise_for_status()
data = response.json()
```

---

# 10. Most Important Interview Questions by Library

## NumPy
- What is NumPy?
- Array vs list?
- What is vectorization?
- What is broadcasting?
- What is `reshape()`?
- What is `axis`?
- What are `shape`, `ndim`, and `dtype`?

## Pandas
- Series vs DataFrame?
- How do you handle missing values?
- `loc` vs `iloc`?
- How do you filter rows?
- What is `groupby()`?
- How do you merge DataFrames?
- How do you remove duplicates?
- How do you inspect a dataset?

## Matplotlib
- Why visualize data?
- Line vs scatter plot?
- What is a histogram?
- How do you add labels/title?
- How can visualization help detect outliers?

## Scikit-learn
- What is `fit()`?
- What is `predict()`?
- What is `transform()`?
- What is preprocessing?
- What is StandardScaler?
- What is OneHotEncoder?
- What is a Pipeline?
- What is train/test split?
- What is cross-validation?
- Which ML algorithms do you know?

## PyTorch
- What is a Tensor?
- Tensor vs NumPy array?
- What is Autograd?
- What is `requires_grad`?
- What is `nn.Module`?
- What is forward propagation?
- What is backpropagation?
- What is an optimizer?
- What is a loss function?
- `train()` vs `eval()`?
- What is `no_grad()`?

## Transformers
- What is a Transformer?
- What is tokenization?
- What is an embedding?
- What is a pretrained model?
- What is `pipeline()`?
- What are Auto classes?
- What is fine-tuning?
- What is a causal language model?
- What is attention?

## Requests
- What is HTTP?
- GET vs POST?
- How do you send JSON?
- What are headers?
- Why use timeout?
- How do you handle errors?
- How do you authenticate API requests?

---

# 11. Priority for an AI/ML Engineer

### 🔴 Must Know Very Well

```text
NumPy
Pandas
Scikit-learn
PyTorch
Transformers
```

### 🟡 Must Know Basics

```text
Matplotlib
Requests
```

### Recommended Learning Order

```text
NumPy
  ↓
Pandas
  ↓
Matplotlib
  ↓
Scikit-learn
  ↓
PyTorch
  ↓
Transformers
  ↓
Requests + APIs
```

---

# 12. Final Interview Tip

Do not just memorize syntax.

For each library, be able to answer:

```text
What is it?
   ↓
Why is it used?
   ↓
What are its important objects/functions?
   ↓
Show a small code example
   ↓
Where would you use it in an AI/ML project?
   ↓
What are its limitations/tradeoffs?
```

If you can explain these seven libraries **and write small working examples without copying**, you have a strong Python-library foundation for an entry-level AI/ML Engineer interview.
