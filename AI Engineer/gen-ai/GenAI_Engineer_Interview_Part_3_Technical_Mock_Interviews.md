# GenAI Engineer Interview Preparation — Part 3
## Practical Coding, APIs, Debugging, System Design, and Mock Interviews

**Target:** GenAI Engineer / Generative AI Intern interview  
**Focus:** Technical understanding, coding, debugging, design trade-offs, and interview-ready explanations.

> Try answering each question aloud before reading the suggested answer. In coding questions, explain assumptions, edge cases, complexity, and design choices.

## Contents
1. Python coding exercises
2. SQL and databases
3. REST APIs and LLM integration
4. Debugging and troubleshooting
5. GenAI system design
6. Project deep-dive questions
7. Difficult follow-ups
8. Mock interview: fundamentals and coding
9. Mock interview: RAG and production
10. Mock interview: system design
11. Take-home assignment
12. Final revision checklist

---

# 1. Python Coding Exercises

## Q1. Remove duplicates while preserving order

```python
def unique_in_order(items):
    seen = set()
    result = []
    for item in items:
        if item not in seen:
            seen.add(item)
            result.append(item)
    return result

print(unique_in_order([3, 1, 3, 2, 1, 4]))
# [3, 1, 2, 4]
```

A set tracks previously seen values and a list preserves order. Average complexity is O(n) time and O(n) extra space. This works for hashable items; lists and dictionaries are unhashable.

## Q2. Count word frequency

```python
from collections import Counter
import re

def word_frequency(text):
    words = re.findall(r"\b[\w']+\b", text.lower())
    return Counter(words)

print(word_frequency("RAG uses retrieval. RAG uses context."))
```

Discuss normalization, punctuation, Unicode, languages, and whether stop words should be removed. Splitting only on spaces is often too simplistic.

## Q3. Find the k most frequent items

```python
from collections import Counter

def top_k(items, k):
    if k <= 0:
        return []
    return Counter(items).most_common(k)
```

Counting takes O(n) time. For streaming data or very large collections, discuss bounded heaps or approximate heavy-hitter algorithms.

## Q4. Implement cosine similarity

\[
\operatorname{cos}(a,b)=\frac{a\cdot b}{\|a\|\|b\|}
\]

```python
import math

def cosine_similarity(a, b):
    if len(a) != len(b):
        raise ValueError("Vectors must have equal dimensions")
    dot = sum(x * y for x, y in zip(a, b))
    norm_a = math.sqrt(sum(x * x for x in a))
    norm_b = math.sqrt(sum(y * y for y in b))
    if norm_a == 0 or norm_b == 0:
        raise ValueError("Cosine similarity is undefined for zero vectors")
    return dot / (norm_a * norm_b)
```

Cosine similarity compares vector direction. It does not prove that a document answers a question. For large-scale retrieval, use optimized vector-search systems rather than Python loops.

## Q5. Split text into overlapping chunks

```python
def chunk_text(text, chunk_size=500, overlap=80):
    if chunk_size <= 0:
        raise ValueError("chunk_size must be positive")
    if overlap < 0 or overlap >= chunk_size:
        raise ValueError("overlap must be smaller than chunk_size")

    chunks = []
    start = 0
    while start < len(text):
        end = min(start + chunk_size, len(text))
        chunks.append(text[start:end])
        if end == len(text):
            break
        start = end - overlap
    return chunks
```

This is a character-based teaching example. Production systems may chunk by tokens, sentences, headings, pages, or semantic boundaries. Preserve document ID, page, section, version, tenant, and access metadata. Overlap can preserve boundary context but increases storage and repeated retrieval.

## Q6. Parse and validate JSON safely

```python
import json

def parse_json_object(raw):
    try:
        value = json.loads(raw)
    except json.JSONDecodeError as exc:
        raise ValueError("Output is not valid JSON") from exc

    if not isinstance(value, dict):
        raise ValueError("Expected a JSON object")
    required = {"answer", "confidence"}
    missing = required - value.keys()
    if missing:
        raise ValueError(f"Missing fields: {sorted(missing)}")
    if not isinstance(value["answer"], str):
        raise ValueError("answer must be a string")

    confidence = value["confidence"]
    if not isinstance(confidence, (int, float)) or isinstance(confidence, bool):
        raise ValueError("confidence must be numeric")
    if not 0 <= confidence <= 1:
        raise ValueError("confidence must be between 0 and 1")
    return value
```

Model output can be invalid or misleading. Parse it, validate its schema, and enforce business rules. Prefer schema-constrained output when available. Valid JSON does not mean the content is true.

## Q7. Retry transient failures with exponential backoff

```python
import random
import time

def retry(operation, attempts=4, base_delay=0.5, max_delay=8.0):
    last_error = None
    for attempt in range(attempts):
        try:
            return operation()
        except (TimeoutError, ConnectionError) as exc:
            last_error = exc
            if attempt == attempts - 1:
                break
            delay = min(max_delay, base_delay * (2 ** attempt))
            delay += random.uniform(0, delay * 0.2)
            time.sleep(delay)
    raise RuntimeError("Operation failed after retries") from last_error
```

Retry only plausible transient errors, use bounded retries and deadlines, respect `Retry-After`, and be careful with non-idempotent operations. Do not retry every HTTP error.

## Q8. Create a simple TTL cache

```python
from time import monotonic

class TTLCache:
    def __init__(self, ttl_seconds=60):
        self.ttl = ttl_seconds
        self.data = {}

    def get(self, key):
        item = self.data.get(key)
        if item is None:
            return None
        value, expires_at = item
        if monotonic() >= expires_at:
            del self.data[key]
            return None
        return value

    def set(self, key, value):
        self.data[key] = (value, monotonic() + self.ttl)
```

This is process-local, non-durable, and unbounded unless eviction is added. Production apps may use Redis. Personalized results must not be shared across users without permission-aware cache keys.

## Q9. Fit chunks into a token budget

```python
def select_chunks(chunks, token_budget, token_counter):
    selected, used = [], 0
    for chunk in chunks:
        cost = token_counter(chunk)
        if used + cost <= token_budget:
            selected.append(chunk)
            used += cost
    return selected, used
```

This greedy example does not rank chunks. A real pipeline should rank, deduplicate, preserve source metadata, and reserve tokens for instructions, question, conversation, and output. Character count is not a reliable token count.

## Q10. Write a basic unit test

```python
def test_unique_in_order():
    assert unique_in_order([1, 2, 1, 3, 2]) == [1, 2, 3]

def test_cosine_similarity():
    assert abs(cosine_similarity([1, 0], [1, 0]) - 1.0) < 1e-9
```

Unit tests validate small units; integration tests validate cooperating components; end-to-end tests validate user workflows. GenAI systems also need quality evaluation because a pipeline may run without errors and still return incorrect answers.

---

# 2. SQL and Databases

Assume the following tables:

```sql
CREATE TABLE users (
    id BIGINT PRIMARY KEY,
    email VARCHAR(255) NOT NULL UNIQUE,
    created_at TIMESTAMP NOT NULL
);

CREATE TABLE documents (
    id BIGINT PRIMARY KEY,
    owner_id BIGINT NOT NULL,
    title VARCHAR(255) NOT NULL,
    status VARCHAR(30) NOT NULL,
    created_at TIMESTAMP NOT NULL,
    FOREIGN KEY (owner_id) REFERENCES users(id)
);

CREATE TABLE queries (
    id BIGINT PRIMARY KEY,
    user_id BIGINT NOT NULL,
    question TEXT NOT NULL,
    latency_ms INT,
    created_at TIMESTAMP NOT NULL,
    FOREIGN KEY (user_id) REFERENCES users(id)
);
```

## Q1. Count documents by status

```sql
SELECT status, COUNT(*) AS document_count
FROM documents
GROUP BY status
ORDER BY document_count DESC;
```

## Q2. Find users who have never submitted a query

```sql
SELECT u.id, u.email
FROM users AS u
LEFT JOIN queries AS q ON q.user_id = u.id
WHERE q.id IS NULL;
```

A `LEFT JOIN` preserves rows from the left table. The null filter finds users with no matching query.

## Q3. Average query latency per user

```sql
SELECT user_id,
       COUNT(*) AS total_queries,
       AVG(latency_ms) AS average_latency_ms
FROM queries
WHERE latency_ms IS NOT NULL
GROUP BY user_id
ORDER BY average_latency_ms DESC;
```

Average latency can hide outliers. Track p50, p95, and p99 in telemetry.

## Q4. Get the latest five queries

```sql
SELECT id, user_id, question, latency_ms, created_at
FROM queries
ORDER BY created_at DESC, id DESC
LIMIT 5;
```

Indexes can improve queries, but cost storage and write time. Validate with the database query plan.

## Q5. Find users with more than ten queries

```sql
SELECT user_id, COUNT(*) AS query_count
FROM queries
GROUP BY user_id
HAVING COUNT(*) > 10;
```

`WHERE` filters rows before grouping; `HAVING` filters groups after aggregation.

## Q6. Explain key database concepts

- **Primary key:** Uniquely identifies a row.
- **Foreign key:** Enforces a relationship to a referenced key.
- **Index:** Can speed up lookup and sorting, at a storage/write cost.
- **Unique constraint:** Prevents duplicate values for a column or column combination.
- **Transaction:** Groups operations under ACID properties, depending on engine and configuration.

## Q7. How would you store RAG documents?

A relational design could include:
- `documents`: owner, title, source, status, version, tenant ID.
- `chunks`: document ID, text, page/section, sequence.
- `embeddings`: chunk ID, model/version, vector reference or vector.
- `permissions`: user/group/document access rules.
- `ingestion_jobs`: status, errors, retries, timestamps.
- `query_logs`: request ID, retrieved IDs, latency, evaluation metadata.

A vector database may store vectors and metadata directly. Apply access and tenant filters during retrieval; do not fetch unauthorized chunks and rely on the LLM to ignore them.

## Q8. Why use transactions in ingestion?

A document should not appear fully indexed if only some chunks or metadata were written. Use transactions where available, staged states, idempotent job IDs, cleanup/retry logic, and reconciliation if relational and vector storage cannot share a transaction.

---

# 3. REST APIs and LLM Integration

## Q1. What is a REST API?

A REST-style API exposes resources through HTTP methods and status codes:
- `GET`: read.
- `POST`: create or trigger an operation.
- `PUT`: replace.
- `PATCH`: partially update.
- `DELETE`: delete.

Good APIs validate input, authenticate users, authorize actions, return consistent errors, and document schemas.

## Q2. Authentication vs authorization

Authentication asks “Who are you?” Authorization asks “What may you do?” A valid JWT does not automatically permit access to every document or action.

## Q3. Example chat endpoint

Request:

```json
{
  "question": "What is the leave policy?",
  "conversation_id": "conv_123",
  "top_k": 5
}
```

Response:

```json
{
  "answer": "The policy states ...",
  "sources": [
    {
      "document_id": "doc_42",
      "title": "Employee Handbook",
      "page": 12
    }
  ],
  "request_id": "req_abc",
  "latency_ms": 840
}
```

Values are illustrative. Do not expose internal paths, secret metadata, or unauthorized source details.

## Q4. Common HTTP status codes

- `200 OK`: successful request.
- `201 Created`: resource created.
- `202 Accepted`: work accepted for asynchronous processing.
- `400 Bad Request`: malformed or invalid input.
- `401 Unauthorized`: missing or invalid authentication.
- `403 Forbidden`: authenticated caller lacks permission.
- `404 Not Found`: resource absent or intentionally hidden.
- `413 Payload Too Large`: request exceeds size limits.
- `422 Unprocessable Content`: structurally valid request fails semantic validation.
- `429 Too Many Requests`: rate limit exceeded.
- `500 Internal Server Error`: unexpected failure.
- `502/503/504`: upstream error, unavailability, or timeout depending on context.

Never return raw stack traces or provider secrets to the client.

## Q5. What is streaming?

Streaming sends output incrementally, often using Server-Sent Events or a streaming response. It can reduce perceived latency by showing the first tokens early. Handle disconnects, cancellation, completion vs failure, and source/citation formatting. Measure time-to-first-token and total latency.

## Q6. How do you call an LLM API safely?

1. Store the API key in secret management or environment configuration.
2. Validate requests and enforce size limits.
3. Authenticate, authorize, and rate-limit users.
4. Set connection/read timeouts.
5. Send only necessary data.
6. Handle rate limits, timeouts, and provider errors.
7. Validate returned output.
8. Record request IDs, latency, token usage, and safe diagnostics.

Never hard-code API keys in source control or expose them in frontend JavaScript.

## Q7. What is idempotency?

Repeating an operation produces the same intended result as doing it once. Idempotency keys can prevent duplicate expensive jobs when clients retry after a timeout.

## Q8. Design asynchronous ingestion

- `POST /documents` validates input and creates a document record.
- Return `202 Accepted` with a job ID if processing is asynchronous.
- A worker extracts, cleans, chunks, embeds, and indexes the document.
- `GET /ingestion-jobs/{id}` reports status.
- Jobs should be idempotent, observable, and safely retryable.

---

# 4. Debugging and Troubleshooting

## Scenario 1: API returns 401

Possible causes: missing/malformed authorization header, expired token, invalid signature, wrong signing key, or issuer/audience mismatch.

Debug in order:
1. Inspect response and server-side error category.
2. Verify the expected header format.
3. Check expiry and signing configuration without printing the token.
4. Confirm algorithm, issuer, audience, and key settings.
5. Add tests for expired and invalid tokens.

Do not fix this by disabling token validation.

## Scenario 2: RAG answers unrelated questions

Check each stage:
1. Was the document parsed correctly?
2. Are chunks coherent?
3. Are query and document embeddings compatible?
4. Do top results contain the answer?
5. Are permission filters too restrictive?
6. Is reranking helping?
7. Is context too long or contradictory?
8. Is the model ignoring evidence?
9. Is the evaluation set representative?

Do not change the LLM before locating the failing stage.

## Scenario 3: Vector search returns no results

Check whether embeddings exist, dimensions match, the correct index is selected, the embedding model changed, filters are too strict, preprocessing differs, similarity threshold is too high, or the index has not updated. Test with a known document and inspect counts, dimensions, filters, and scores.

## Scenario 4: Invalid JSON from the model

Use schema-constrained output where available, specify exact fields and types, validate responses, retry selectively within a bounded budget, and reject unexpected content. Never execute model-generated code or SQL merely because it parses.

## Scenario 5: Latency suddenly doubles

Measure queueing, auth, retrieval, reranking, prompt construction, time-to-first-token, generation, tool calls, and response serialization. Compare p50/p95/p99, token counts, provider latency, retries, and traffic. Look for larger prompts or repeated calls.

## Scenario 6: Works locally, fails in deployment

Check environment variables, dependency/runtime versions, network rules, database migrations, CORS, frontend API URL, TLS/proxy configuration, case-sensitive file paths, resource limits, health checks, DNS, and deployment logs.

## Scenario 7: Users can see each other's documents

Treat it as a security incident. Restrict the affected endpoint if needed, preserve logs, assess scope, fix server-side permission and tenant filtering, invalidate unsafe caches, add cross-tenant regression tests, and follow the incident process. A frontend filter is not a security boundary.

## Scenario 8: Uploaded PDF instructions manipulate the model

This may be prompt injection. Treat retrieved content as untrusted data, separate it from system policy, constrain tool permissions, enforce authorization in application code, and test malicious documents. Prompt wording alone is not a complete defense.

## Scenario 9: Provider returns 429

Respect `Retry-After` and provider quota guidance, use bounded backoff with jitter, reduce concurrency, queue bursty workloads, track request and token quotas, and avoid retry storms.

## Scenario 10: Model upgrade worsens answers

Compare old and new versions on a fixed dataset: correctness, grounding, citation validity, retrieval quality, refusal behavior, latency, cost, structured-output validity, and security tests. Use staged rollout and a rollback path.

---

# 5. GenAI System Design

## Q1. Design a company-policy assistant

### Requirements
- Employees ask questions about company documents.
- Answers include sources.
- Users cannot access unauthorized documents.
- Documents can be updated and re-indexed.
- Quality, latency, and cost are measured.

### Architecture

```text
Client
  |
API Gateway / Authentication / Rate Limits
  |
Chat Orchestrator -------- Observability
  |
Permission Checks
  |
Query Processing
  |
Hybrid Retrieval --> Optional Reranker
  |
Context Builder
  |
LLM Provider
  |
Output + Citation Validation
  |
Answer and Sources
```

Ingestion is a separate asynchronous flow:

```text
Upload -> Validation -> Queue/Worker -> Text Extraction/OCR
       -> Cleaning -> Chunking + Metadata -> Embeddings
       -> Vector Index + Keyword Index + Document Metadata
```

### Design decisions

- **Hybrid retrieval:** Combines semantic similarity with lexical search, useful for natural-language questions and exact identifiers.
- **Reranking:** May improve ordering but adds latency and cost. Measure the benefit.
- **Citations:** Preserve document/page/chunk metadata; only cite sources actually retrieved and accessible.
- **Permissions:** Enforce access at retrieval time and validate source access before returning metadata. Include permission scope in cache keys.
- **Updates/deletion:** Track versions and remove deleted documents from indexes and caches.
- **Failures:** If retrieval is unavailable, do not silently invent an answer.
- **Evaluation:** Use representative questions, expected sources, and acceptable answer criteria.

## Q2. Build a RAG pipeline from scratch

1. Gather representative questions and documents.
2. Parse file formats and use OCR when necessary.
3. Normalize text while preserving headings, tables, and page references.
4. Chunk using structure-aware boundaries and a token budget.
5. Attach stable IDs, version, and permission metadata.
6. Generate embeddings and record model version.
7. Store vectors and searchable text.
8. Normalize the query and apply authorization filters.
9. Retrieve candidates using vector, keyword, or hybrid search.
10. Optionally rerank and deduplicate.
11. Build context within the token budget.
12. Ask the model to answer from evidence and acknowledge missing evidence.
13. Validate output and citations.
14. Return answer, sources, and request ID.
15. Record safe telemetry and evaluate failures.

## Q3. Evaluate RAG quality

### Retrieval metrics
- **Recall@k:** Fraction of relevant documents found in top k.
- **Precision@k:** Fraction of top-k results that are relevant.
- **MRR:** Rewards ranking the first relevant result highly.
- **nDCG:** Evaluates ranking with graded relevance.

### Answer metrics
Correctness, groundedness, completeness, citation accuracy, appropriate abstention, and safety.

### Operational metrics
p50/p95/p99 latency, time-to-first-token, errors, token usage, cost per request, cache hit rate, ingestion failure rate, and document freshness.

LLM-as-judge can scale reviews but may be biased. Calibrate it against human labels and use human review for important cases.

## Q4. How do you reduce hallucinations?

Retrieve trustworthy evidence, make the evidence boundary clear, link citations to retrieved sources, validate citations, evaluate with reference and adversarial questions, allow abstention, and use deterministic code for facts that should not be generated. No single prompt guarantees zero hallucinations.

## Q5. RAG or fine-tuning?

RAG is useful for changing/private facts and source citations. Fine-tuning is useful for teaching behavior, format, style, or repeated task patterns. They can be combined; fine-tuning does not automatically provide up-to-date facts.

## Q6. Reduce cost

Choose the smallest model that meets measured quality, limit input/output tokens, retrieve fewer but better chunks, cache only where safe, avoid redundant model calls, batch offline tasks, apply quotas, and measure cost per successful task.

## Q7. What should be monitored?

Request volume, failures, latency percentiles, provider timeouts/rate limits, token use, cost, retrieval relevance, citation failures, abstention rate, ingestion freshness, permission denials, and model/prompt/index versions. Avoid logging secrets or unnecessary sensitive content.

---

# 6. Project Deep-Dive Questions

## Q1. Explain your project in 60 seconds

Use this template and replace the brackets with true details:

> “I built **[project name]**, a **[type of application]** that helps **[target users]** solve **[specific problem]**. It uses **[model/API]** for generation and **[retrieval/database method]** to provide relevant context. The backend uses **[framework]** and the frontend uses **[framework]**. I personally worked on **[specific contributions]**. I evaluated it using **[test set/metrics/manual checks]** and observed **[measured result or honest limitation]**. The main challenge was **[challenge]**, which I addressed by **[approach]**.”

Never claim a metric, deployment, or feature you did not implement and verify.

## Q2. Why this technology stack?

Discuss requirements, development speed, team familiarity, ecosystem, scale, data model, deployment, cost, security, and maintainability. “Because it is popular” is not enough.

## Q3. Trace a user request end to end

Explain what your actual application does:
1. Frontend validates and sends the request.
2. Backend authenticates and authorizes.
3. Schema and request limits are checked.
4. Query processing and retrieval occur.
5. Relevant context is selected.
6. Model generates an answer.
7. Output and citations are validated.
8. Backend returns the result.
9. Safe telemetry records the request.

Clearly distinguish implemented steps from planned work.

## Q4. Explain your hardest bug

Use this structure:
- **Symptom:** What failed?
- **Diagnosis:** What evidence identified the cause?
- **Fix:** What changed?
- **Validation:** What test proved it was fixed?
- **Trade-off:** What limitation remains?

Example: “The chatbot retrieved relevant information inconsistently. I inspected the chunks before changing the prompt and found key ideas split across boundaries. I tested structure-aware chunk sizes and controlled overlap on a fixed set of questions. The results improved on those cases, but a larger evaluation set would be needed before claiming production quality.”

Use this example only if it reflects your real work.

## Q5. How do you know answers are correct?

Build a representative test set, label relevant chunks, evaluate retrieval and generation separately, verify citations, include unanswerable questions, categorize failures, and report sample size and limitations.

## Q6. What would you improve in one week?

Prioritize measurable work: regression tests, evaluation dataset, retrieval/citation validation, timeouts and request IDs, authorization checks, latency/cost measurements, deployment reliability, and documentation.

## Q7. How do you discuss an unfinished project?

Separate **implemented**, **tested**, **prototype**, and **planned** features. Clear honesty is stronger than exaggerated claims.

---

# 7. Difficult Follow-Up Questions

## Q1. If the context window is huge, why use RAG?

Large prompts cost more, increase latency, and can include irrelevant or conflicting information. The model may still miss the right evidence. RAG selects relevant context, supports permission-aware retrieval, and tracks sources.

## Q2. Why keyword search if vector search is semantic?

Embeddings can miss exact IDs, rare names, product codes, and error strings. Keyword search is often strong for exact matches; hybrid retrieval combines complementary signals.

## Q3. Why not increase top-k?

More chunks can add noise, duplication, and token cost. Improve relevance, filtering, deduplication, and reranking instead of blindly increasing k.

## Q4. Does high cosine similarity prove a chunk answers the question?

No. It measures vector similarity, not factual support. Similar text may not contain the answer. Evaluate relevance and evidence support.

## Q5. Is temperature zero deterministic?

Not guaranteed. Provider infrastructure, model versions, sampling implementations, and parallel execution may still cause variation. It often reduces sampling variation but does not guarantee identical outputs.

## Q6. Can an LLM safely execute SQL?

Not by default. Use parameterized queries, read-only accounts, allowlists, validation, row/statement limits, tenant checks, and human approval for sensitive actions. Never concatenate untrusted strings into SQL.

## Q7. Are agents always better than workflows?

No. Fixed workflows are often cheaper, simpler, and easier to test. Use agents when dynamic tool selection or planning gives measurable value and can be constrained.

## Q8. Embedding model vs generative model?

An embedding model maps input into vectors useful for similarity and retrieval. A generative model produces content. They serve different roles and can work together.

## Q9. What causes context-window overflow?

Instructions, conversation history, retrieved content, and output allowance exceed the limit. Summarize history, retrieve better/fewer chunks, remove redundancy, and reserve output tokens.

## Q10. Why can good retrieval still produce a bad answer?

Context may be too long, contradictory, poorly ordered, or incomplete. The model may misinterpret or ignore it. Evaluate retrieval and generation separately.

## Q11. Prevent data leakage through logs?

Minimize collected content, redact sensitive fields, restrict access, define retention, avoid secrets, separate identifiers from payloads, and document provider behavior.

## Q12. What is the most important GenAI metric?

There is no universal single metric. Use task success or answer quality as the primary outcome, with safety, latency, cost, and reliability as constraints.

---

# 8. Mock Interview — Fundamentals and Coding

Answer aloud before reading the suggested responses.

### 1. Explain a transformer simply.
A transformer processes tokens using attention, allowing each token to incorporate information from other tokens. It combines token embeddings and positional information and processes them through attention and feed-forward layers. Decoder-only transformers commonly generate text by predicting the next token repeatedly.

**Follow-up: What does self-attention do?** It computes how strongly each token should use information from other tokens, using learned query, key, and value representations.

### 2. Explain embeddings.
Embeddings are dense vectors intended to represent useful relationships between inputs. Semantically related inputs may be close under a similarity measure. They support search, clustering, and retrieval. Individual dimensions are usually not directly interpretable.

### 3. Explain RAG.
RAG retrieves external information and adds it to the model's context. A typical pipeline parses and chunks documents, embeds/indexes chunks, retrieves candidates, optionally reranks, and generates an answer using selected evidence.

### 4. Find the most frequent word in a document.
Normalize and tokenize the text, then use `collections.Counter`. Discuss punctuation, case, languages, and tie handling.

### 5. What is a Python generator?
A generator yields values lazily rather than materializing all results at once. It can reduce memory use for large sequences and is created with `yield` or a generator expression.

### 6. List vs tuple?
Lists are mutable; tuples are immutable at the container level. Tuples can be useful for fixed records and are hashable if all elements are hashable.

### 7. What is a database index?
An auxiliary structure that can speed up lookups and sorting. It consumes storage and can slow writes. Choose indexes based on query patterns and query-plan evidence.

### 8. Handle a slow model API.
Measure individual stages, set timeouts, inspect provider latency and token counts, reduce unnecessary prompt/retrieval work, stream if useful, and apply bounded retries to transient failures.

### 9. Precision vs recall?
Precision asks how many retrieved items are relevant. Recall asks how many of all relevant items were retrieved. The right balance depends on the use case.

### 10. What if you do not know an answer?
Be transparent, state what you know, identify uncertainty, and explain how you would verify it. Do not bluff.

---

# 9. Mock Interview — RAG and Production

### 1. The chatbot answers without sources. What do you check?
Verify retrieval ran, candidates were returned, metadata survived context construction, the model was instructed to cite sources, and parsing did not remove citations. Add tests for source propagation and validation. If no evidence exists, follow a defined fallback or abstention policy.

### 2. Why does chunk size matter?
Small chunks are precise but can lose context; large chunks retain context but add irrelevant material and token cost. Test alternatives on a fixed dataset.

### 3. What is reranking?
A second-stage model scores query-document pairs in a shortlist to improve ordering. It adds cost and latency, so measure its benefit.

### 4. How do you handle PDF tables?
Use parsing that preserves table structure, retain headers with rows, preserve page/table IDs, and test table-specific questions. Plain-text extraction may scramble columns; scanned files may need OCR.

### 5. What is prompt injection?
An attempt to manipulate the model through malicious instructions in user input or retrieved content. Treat external content as untrusted, constrain tools, enforce permissions in code, and test adversarial inputs.

### 6. Why shouldn't the model decide authorization?
The model can be mistaken or manipulated. Trusted application code and the data layer must enforce authorization independently.

### 7. Timeout vs rate limit?
A timeout means the operation exceeded its allowed duration. A rate limit means throughput is restricted. Timeouts require deadline-aware handling; rate limits require quota-aware throttling and retries.

### 8. How do you evaluate a model change?
Run a fixed evaluation set against both versions and compare quality, groundedness, safety, latency, cost, and output validity. Inspect regressions and use staged rollout/rollback.

### 9. Reduce irrelevant retrieved chunks?
Improve cleaning/chunking, apply metadata and permission filters, use hybrid search, tune candidate count, rerank, and deduplicate. Evaluate rather than relying on a few examples.

### 10. What is observability?
Understanding system behavior through logs, metrics, and traces. Trace requests through authentication, retrieval, reranking, generation, validation, and response delivery while protecting sensitive content.

---

# 10. Mock Interview — System Design

### 1. Design a support chatbot for 50,000 documents.
Clarify user types, permissions, formats, freshness, request volume, languages, and quality targets. Separate asynchronous ingestion from online answering. Store permission metadata; use vector and keyword retrieval if evaluation supports it; add reranking only when worthwhile; enforce access filters; version models/indexes; evaluate quality; monitor latency, cost, freshness, and citations; define deletion and backup procedures.

### 2. RAG answers are correct for public documents but leak restricted content.
Treat this as a critical authorization defect. Restrict the endpoint, investigate scope, fix server-side filters, review caches and source metadata, add cross-tenant tests, and follow incident response. Do not rely on prompt instructions to prevent disclosure.

### 3. The team wants multi-agent architecture immediately.
First define the user problem and success criteria. A simple retrieval-and-generation workflow may meet the need with less latency, cost, and complexity. Add agents only when dynamic tool use provides measured value and can be constrained and tested.

### 4. The model is accurate but too expensive.
Measure cost per successful task and token distribution. Reduce redundant context, improve retrieval, cache safely, cap output, test smaller models, batch offline work, and remove unnecessary calls. Re-run evaluations after changes.

### 5. A manager asks for “99% accuracy.” What do you clarify?
Define accuracy, dataset, task distribution, acceptable errors, confidence intervals, safety requirements, and applicable conditions. Open-ended generation rarely has one adequate accuracy number; use task-specific quality and groundedness metrics.

### 6. You have 30 minutes to debug production.
Assess impact, check recent deployments and alerts, reproduce using a request ID or sanitized example, inspect traces, identify the failing component, mitigate safely, verify with a regression test, and document root cause/follow-ups.

---

# 11. Practical Take-Home Assignment

## Build a document question-answering API

**Goal:** Build a backend that answers questions from a collection of documents and returns sources.

### Suggested endpoints
- `POST /documents`: accept a supported file or text payload.
- `GET /documents`: list only documents the caller may access.
- `POST /chat`: retrieve relevant chunks and generate an answer.
- `GET /health`: report health without exposing secrets.
- `GET /ingestion-jobs/{id}`: report asynchronous ingestion status.

### Minimum engineering requirements
- Environment-based secrets.
- Input validation and size limits.
- Consistent errors.
- External-call timeouts.
- Request IDs and structured logs.
- Permission checks.
- Unit tests for chunking, validation, and authorization.
- Integration test for the main question-answer flow.
- README with setup instructions and limitations.

### GenAI requirements
- Document parsing and chunking.
- Embedding/index creation.
- Retrieval and optional reranking.
- Grounded answer generation.
- Source metadata in responses.
- Defined behavior when evidence is missing.
- Small evaluation dataset with answerable and unanswerable questions.

### Evaluation rubric

| Area | What is evaluated |
|---|---|
| Correctness | Works on representative cases |
| Code quality | Clear modules, errors, and tests |
| Retrieval | Relevant chunks are returned |
| Grounding | Answers follow evidence |
| Security | Secrets and permissions are protected |
| Reliability | Timeouts and failures are handled |
| Observability | Failures can be diagnosed |
| Communication | Trade-offs and limitations are explained |

In a code review, explain architecture, assumptions, tests, scaling, cross-user isolation, what you measured, what you did not measure, and the next improvement.

---

# 12. Final Revision Checklist

## Fundamentals
- [ ] AI vs ML vs deep learning vs GenAI.
- [ ] Tokenization, embeddings, attention, transformers, next-token prediction.
- [ ] Temperature, top-k, top-p, context windows, token budgets.
- [ ] Prompting vs RAG vs fine-tuning.

## RAG
- [ ] Ingestion, chunking, embeddings, retrieval, reranking, generation.
- [ ] Vector vs keyword vs hybrid search.
- [ ] Recall@k, Precision@k, MRR, nDCG.
- [ ] Grounding, citations, abstention.
- [ ] Diagnose retrieval separately from generation.

## Engineering
- [ ] Python functions, tests, lists, dictionaries, sets, generators, exceptions.
- [ ] SQL joins, aggregation, `HAVING`.
- [ ] REST methods, status codes, authentication vs authorization.
- [ ] Timeouts, retries, backoff, idempotency, rate limits.
- [ ] Logs, metrics, traces, latency percentiles.

## Production and security
- [ ] Prompt injection and untrusted retrieved content.
- [ ] Server-side authorization and tenant filtering.
- [ ] Secrets and sensitive logs.
- [ ] Tenant isolation, safe caching, deletion.
- [ ] Evaluation, staged rollout, rollback.

## Project explanation
- [ ] Explain one project in 60 seconds.
- [ ] Draw architecture from memory.
- [ ] Trace one request end to end.
- [ ] Explain a real bug and how you diagnosed it.
- [ ] Separate implemented features from planned features.
- [ ] Discuss measurable limitations honestly.

---

# Final Interview Strategy

For technical questions:
1. **Definition:** Explain the concept briefly.
2. **Mechanism:** Describe how it works.
3. **Example:** Connect it to a GenAI application.
4. **Trade-off:** Explain when it helps and what it costs.
5. **Failure mode:** Mention a limitation or common mistake.

For coding questions:
1. Clarify input/output.
2. State assumptions.
3. Write a correct basic solution.
4. Test normal, empty, invalid, and boundary cases.
5. Discuss complexity.
6. Explain how to productionize it.

For questions you cannot answer, do not bluff. State what you know, explain the uncertainty, and describe how you would verify the behavior.

**The goal is not to memorize every answer word-for-word. Understand the concepts well enough to explain them clearly, write code, debug failures systematically, and defend your design decisions.**
