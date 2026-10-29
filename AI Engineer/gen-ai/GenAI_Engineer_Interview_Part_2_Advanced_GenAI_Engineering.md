# GenAI Engineer Interview Preparation — Part 2: Advanced GenAI Engineering

**Level:** Intermediate to advanced internship interview preparation  
**Focus:** Practical GenAI architecture, RAG, retrieval, fine-tuning, agents, evaluation, deployment and security  
**Goal:** Explain not only what each technique is, but when to use it, how it works, how to evaluate it and what can go wrong.

> Part 1 covered the foundations: machine learning, neural networks, transformers, LLMs, embeddings, prompts and inference. This file builds on those concepts and focuses on engineering real GenAI systems.

---

## Table of Contents

1. GenAI application architecture
2. Retrieval-Augmented Generation (RAG)
3. Document ingestion, chunking and metadata
4. Embeddings, vector search and hybrid retrieval
5. Reranking and query transformation
6. Grounded generation and citation design
7. RAG evaluation and debugging
8. Fine-tuning and parameter-efficient adaptation
9. Agents, tools and workflows
10. Multimodal GenAI
11. LLM evaluation and observability
12. Production performance, scaling and cost
13. Security, privacy and prompt-injection defence
14. GenAI coding and implementation questions
15. Advanced scenario-based interview questions
16. Rapid-fire questions
17. Final revision checklist

---

# 1. GenAI Application Architecture

### Q1. How would you design a production GenAI application?

**Answer:** I would start with the business requirements, users, data sensitivity, quality target, latency target and cost constraints. Then I would design the application around these components:

1. Client or frontend.
2. Backend API with authentication, authorisation and input validation.
3. Orchestration layer that constructs prompts and manages model calls.
4. Optional retrieval layer for private or current information.
5. Optional tools or deterministic business services.
6. Model provider or self-hosted inference server.
7. Output parsing, validation and safety checks.
8. Observability, evaluation, rate limiting and audit controls.

I would build a baseline, create a representative evaluation dataset, measure quality and latency, and add complexity only when evidence shows it is needed.

### Q2. What is the difference between an LLM, an LLM application and an AI agent?

**Answer:**
- **LLM:** The model that generates token sequences.
- **LLM application:** Software that uses a model to deliver a task, with prompts, data, APIs and validation.
- **AI agent:** An application in which a model can choose and sequence actions or tool calls toward a goal, under application-controlled permissions and limits.

A chatbot that only sends a prompt to a model is an LLM application, but it is not necessarily an agent.

### Q3. What is an orchestration layer?

**Answer:** It coordinates the steps around model use, such as prompt construction, retrieval, tool execution, output validation and error handling. It can be implemented with ordinary application code or a framework. The orchestration layer should make control flow and permissions explicit rather than blindly trusting model-generated instructions.

### Q4. Why should you avoid adding a framework too early?

**Answer:** A framework can accelerate development, but it can also hide network calls, prompt construction, retries and data flow. I would first understand the core workflow and create a small working baseline. Then I would adopt a framework if its abstractions improve maintainability, tracing, integrations or testing enough to justify the added complexity.

### Q5. What is the difference between deterministic code and LLM reasoning?

**Answer:** Deterministic code follows explicit rules and should produce predictable results for the same inputs and state. LLM output is probabilistic or otherwise model-dependent and can be incomplete or wrong. Use code for arithmetic, access control, validation and critical business rules; use the model for language-heavy tasks where its flexibility is useful.

---

# 2. Retrieval-Augmented Generation (RAG)

## 2.1 What is RAG?

Retrieval-Augmented Generation combines information retrieval with a generative model. Instead of relying only on what the model learned during training, the application searches an external corpus for relevant information and supplies selected evidence to the model.

A typical flow is:

**Documents → extraction → chunking → embeddings/indexing → query retrieval → optional reranking → prompt with evidence → generated answer with citations**

At query time, the model does not automatically search every document. The retrieval component selects candidate passages.

### Q6. Explain RAG in an interview.

**Answer:** RAG retrieves relevant external passages for a user query and supplies them as context to an LLM. The model then generates an answer using the query and retrieved evidence. RAG is useful for private, changing or source-specific knowledge because the corpus can be updated without retraining the model. Its quality depends on retrieval, document processing, context construction and generation.

### Q7. Why use RAG instead of fine-tuning?

**Answer:** RAG is usually a good first option when the main problem is access to changing facts, private documents or source citations. Updating a document index is often easier than retraining a model. Fine-tuning is more suitable when the model needs to learn a consistent task behaviour, style or specialised pattern. They solve different problems and can be combined.

### Q8. Does RAG eliminate hallucinations?

**Answer:** No. Retrieval may return irrelevant or incomplete passages, and the model may misread or overstate evidence. RAG can improve grounding, but it needs retrieval evaluation, source-aware prompting, citation validation, abstention behaviour and end-to-end testing.

### Q9. What is the difference between offline and online RAG processing?

**Answer:**
- **Offline/indexing stage:** Load documents, extract text, clean it, split it into chunks, attach metadata, generate embeddings and build an index.
- **Online/query stage:** Validate the question, optionally rewrite it, retrieve candidates, rerank them, assemble context, call the model, validate the output and return the answer.

Separating these stages allows document indexing to happen on a schedule or when source content changes, rather than for every user question.

### Q10. What are the main failure points in a RAG pipeline?

**Answer:**
1. The document was never indexed.
2. Text extraction lost important content.
3. Chunk boundaries split a key fact from its context.
4. Embeddings do not represent the domain or query well.
5. Retrieval misses the relevant chunk.
6. Ranking puts relevant chunks too low.
7. Context assembly truncates or mixes evidence.
8. The model ignores, misinterprets or contradicts the evidence.
9. Citations point to the wrong source.
10. Permissions allow retrieval of documents the user should not access.

Debug the pipeline stage by stage instead of treating every wrong answer as an LLM problem.

### Q11. What is the difference between parametric and non-parametric knowledge?

**Answer:** Parametric knowledge is encoded in a model's learned parameters. Non-parametric knowledge is available outside those parameters, for example in a document index or database that the application can query. RAG provides a way to combine the model's learned capabilities with external information.

### Q12. When might RAG be unnecessary?

**Answer:** RAG may be unnecessary for tasks that need no external knowledge, such as rewriting user-provided text or producing a generic explanation. It may also be unnecessary when a simple database query or deterministic rule is more reliable. I would add retrieval only when the task benefits from searchable external evidence.

---

# 3. Document Ingestion, Chunking and Metadata

## 3.1 Why chunk documents?

Embedding a whole large document into one vector can make precise retrieval difficult, and the document may exceed the model's context window. Chunking divides content into smaller pieces that can be retrieved independently. The ideal chunk size depends on document structure, query type, embedding model and context budget.

### Q13. What is chunking?

**Answer:** Chunking splits a document into smaller units for indexing and retrieval. Each chunk should contain enough context to be meaningful while being specific enough to retrieve precisely. A chunk may include text, source metadata, page number, section title and access-control labels.

### Q14. What is fixed-size chunking?

**Answer:** Fixed-size chunking splits text after a configured number of tokens or characters, optionally with overlap. It is simple and reproducible, but it can split sentences, tables, definitions or code blocks at awkward boundaries.

### Q15. What is semantic or structure-aware chunking?

**Answer:** It uses document structure or semantic boundaries—such as headings, paragraphs, sections, code blocks or topic changes—to create chunks. It can preserve meaning better than arbitrary splitting, but the implementation is more complex and may create chunks of uneven size.

### Q16. What is chunk overlap, and why use it?

**Answer:** Overlap repeats some content from the end of one chunk at the beginning of the next. It can preserve context when a fact crosses a boundary. Too much overlap increases index size, redundant retrieval and cost, so overlap should be measured rather than chosen automatically.

### Q17. How would you select chunk size?

**Answer:** I would begin with a reasonable baseline based on the document type and embedding model, then evaluate different sizes and overlaps using labelled questions. I would measure retrieval recall and precision, answer correctness, citation quality, token usage and latency. Policy documents, tables, code and long technical manuals may need different chunking rules.

### Q18. Why is metadata important in RAG?

**Answer:** Metadata enables filtering, traceability and access control. Useful fields may include document ID, title, section, page number, source URL, timestamp, document version, department, tenant ID and access permissions. Metadata should be retained through retrieval so the answer can cite the correct source.

### Q19. How should PDFs and tables be handled?

**Answer:** Do not assume every PDF has clean extractable text. Some are scanned images, have multi-column layouts or contain tables whose meaning depends on row and column headers. Use OCR when needed, preserve headings and table structure, validate extraction, and store page and source identifiers. For complex tables, structured extraction or a database representation may be better than plain text chunks.

### Q20. What is parent-child retrieval?

**Answer:** A system indexes small child chunks for precise matching but can return a larger parent section as context. This balances retrieval precision with the context needed to understand a fact. The parent-child relationship and source metadata must be maintained correctly.

### Q21. How do you keep a document index up to date?

**Answer:** Track document identifiers, versions and modification times. Re-index changed documents, remove or tombstone deleted documents, and avoid duplicate chunks. Make indexing idempotent so rerunning a job does not create duplicate records. For sensitive data, deletion must propagate to all relevant indexes and caches according to policy.

---

# 4. Embeddings, Vector Search and Hybrid Retrieval

### Q22. How does semantic search work?

**Answer:** An embedding model converts a query and document chunks into vectors. The system searches for vectors that are close under the selected similarity or distance measure, often with metadata filters. The retrieved text—not just the vectors—is passed to the generation stage.

### Q23. How do you choose an embedding model?

**Answer:** I would consider language coverage, domain performance, query-document compatibility, vector dimensions, maximum input length, latency, cost, licence and deployment constraints. I would evaluate candidate models on the actual corpus and labelled query set rather than relying only on public leaderboard scores.

### Q24. What is approximate nearest-neighbour (ANN) search?

**Answer:** ANN methods find vectors that are very close to a query vector without necessarily checking every vector exactly. They trade a small amount of recall or exactness for faster search at scale. Index structures such as HNSW or IVF-based methods are common examples, with different memory, build-time and search trade-offs.

### Q25. What is HNSW?

**Answer:** Hierarchical Navigable Small World is a graph-based approximate nearest-neighbour method. It builds layered proximity graphs to navigate efficiently toward similar vectors. It can provide fast high-recall search, but memory usage and index-building choices matter.

### Q26. What is BM25?

**Answer:** BM25 is a sparse lexical retrieval ranking function based on query-term matching, term frequency, inverse document frequency and document-length normalisation. It can be especially effective for exact keywords, product IDs, names and rare terms.

### Q27. What is hybrid search?

**Answer:** Hybrid search combines dense semantic retrieval with sparse lexical retrieval. For example, dense search may find a paraphrase, while BM25 finds an exact error code. Candidate lists can be combined with a method such as Reciprocal Rank Fusion (RRF), or a learned ranking model.

### Q28. What is Reciprocal Rank Fusion?

**Answer:** RRF combines rankings from multiple retrieval systems by giving credit to a document according to its rank in each list. A common form is:

\[
\operatorname{RRF}(d)=\sum_r\frac{1}{k+\operatorname{rank}_r(d)}
\]

Here, \(d\) is a document, \(r\) is a ranking list and \(k\) is a smoothing constant. RRF is useful when different retrieval systems produce scores that are not directly comparable.

### Q29. Why can a vector search return the wrong passage?

**Answer:** The query may be ambiguous, the embedding model may not fit the domain, the relevant text may be poorly chunked, or similar wording may conceal different facts. Metadata filters may also exclude the right source. I would inspect top results, measure recall at \(k\), and compare dense, sparse and hybrid methods.

### Q30. What is metadata filtering?

**Answer:** Metadata filtering restricts retrieval to documents meeting conditions such as tenant, department, date, document type or permissions. It can improve relevance and enforce data boundaries, but access-control filters must be applied server-side and must not rely on model instructions.

### Q31. How can you improve retrieval for exact technical terms?

**Answer:** Combine dense retrieval with lexical search, preserve identifiers and code symbols during ingestion, avoid destructive normalisation, apply metadata filters and rerank candidates. For code or error-message search, specialised tokenisation and code-aware chunking may also help.

---

# 5. Reranking and Query Transformation

### Q32. What is a cross-encoder reranker?

**Answer:** A cross-encoder processes the query and a candidate passage together and predicts a relevance score. Because it evaluates the pair jointly, it can capture interactions that a simple vector similarity score misses. It is usually more expensive than embedding search, so it is often applied only to a limited candidate set.

### Q33. What is a bi-encoder?

**Answer:** A bi-encoder embeds the query and document independently. The vectors can be computed in advance for documents and compared efficiently at query time. It is suitable for large-scale retrieval but may be less precise than a cross-encoder for final ranking.

### Q34. Explain a two-stage retrieval pipeline.

**Answer:** First, a fast retriever obtains a broad candidate set, perhaps using dense and sparse search. Second, a more accurate reranker orders those candidates. The application then sends only the top relevant evidence to the LLM. This improves precision while controlling reranking cost.

### Q35. What is query rewriting?

**Answer:** Query rewriting transforms a user's question into a search-friendly version, expands abbreviations, resolves context or generates alternate queries. It can help when the original query is conversational or underspecified. The rewritten query should not change the user's intent or inject unsupported assumptions.

### Q36. What is multi-query retrieval?

**Answer:** The system generates several alternative search queries from the original question, retrieves results for each and combines the candidates. It can improve recall for ambiguous questions, but adds latency and may retrieve more irrelevant material.

### Q37. What is HyDE?

**Answer:** Hypothetical Document Embeddings (HyDE) is a retrieval approach in which a language model generates a hypothetical passage that might answer the query. The passage is embedded and used to retrieve real documents. It can improve retrieval in some cases, but the hypothetical text can contain invented details; only retrieved source documents should be treated as evidence.

### Q38. What is contextual compression?

**Answer:** Contextual compression reduces retrieved material to the portions relevant to the query, using rules, extractive selection or a model. It can save context tokens and reduce distractions, but careless compression may remove qualifications or evidence. The compressed context should remain traceable to its original sources.

---

# 6. Grounded Generation and Citation Design

### Q39. How do you prompt an LLM to answer only from retrieved documents?

**Answer:** I would clearly separate the user question from retrieved evidence, instruct the model to use only relevant evidence for factual claims, require it to say when evidence is insufficient, and request source identifiers for supported claims. I would also validate citations in code and test whether the model follows these rules under adversarial inputs.

A prompt helps guide behaviour; it is not a security or correctness guarantee.

### Q40. What makes a citation valid?

**Answer:** A valid citation must point to a real source or chunk, and that source must support the associated claim. Checking that a source ID exists is necessary but not sufficient. For high-quality systems, evaluate claim-to-source support and preserve document version, page or section information where possible.

### Q41. What is answer faithfulness?

**Answer:** Faithfulness measures whether an answer's claims are supported by the supplied evidence. It differs from general correctness: an answer can be factually true based on outside knowledge yet unfaithful to the retrieved context. In grounded applications, both faithfulness and correctness can matter.

### Q42. What should the system do when retrieval returns no useful evidence?

**Answer:** It should avoid manufacturing a source-backed answer. Depending on the task, it can ask a clarifying question, state that the indexed sources do not contain enough information, or route the question to an authorised person. The threshold for abstention should be calibrated through evaluation.

### Q43. What is answer synthesis?

**Answer:** Answer synthesis combines information from multiple retrieved passages into one response. The system must reconcile duplicates, contradictions and different document versions. For conflicting sources, it should follow an explicit source-priority policy or report the conflict instead of silently choosing one.

---

# 7. RAG Evaluation and Debugging

RAG evaluation should separate retrieval quality from generation quality. A good final answer may occasionally result from the model's prior knowledge despite poor retrieval, so end-to-end evaluation alone can hide weaknesses.

### Q44. What is Recall@k?

**Answer:** Recall@k measures how much of the known relevant material is retrieved within the top \(k\) results. If a query has four labelled relevant chunks and the top five results contain three of them, Recall@5 is \(3/4=0.75\), under this definition.

### Q45. What is Precision@k?

**Answer:** Precision@k measures the proportion of the top \(k\) retrieved results that are relevant. If two of the top five results are relevant, Precision@5 is \(2/5=0.4\). Some evaluations treat multiple chunks from the same source specially, so the protocol should be defined in advance.

### Q46. What are MRR and nDCG?

**Answer:**
- **Mean Reciprocal Rank (MRR):** Averages the reciprocal of the rank of the first relevant result across queries.
- **Normalised Discounted Cumulative Gain (nDCG):** Evaluates ranking quality using graded relevance and discounts results lower in the list.

These metrics help evaluate whether useful evidence appears early enough to be included in a limited context budget.

### Q47. What should an end-to-end RAG evaluation measure?

**Answer:** It should measure answer correctness, relevance, faithfulness to retrieved evidence, completeness, citation accuracy, appropriate abstention, safety, latency and cost. Retrieval metrics such as Recall@k and nDCG should be measured separately. Automated LLM judges can assist, but their judgements should be calibrated against human-labelled examples.

### Q48. How do you create a RAG evaluation dataset?

**Answer:**
1. Sample representative real questions and important edge cases.
2. Have qualified reviewers identify the correct answer or acceptable answer criteria.
3. Label relevant source passages and expected citations where feasible.
4. Include unanswerable questions, ambiguous queries and conflicting documents.
5. Split development and test questions carefully to avoid leakage.
6. Version the corpus and evaluation set.
7. Review failures and update the dataset without tuning exclusively to the test set.

### Q49. How would you debug a RAG answer that is incorrect?

**Answer:** Trace the request through the pipeline. Verify the indexed content, inspect the extracted text and chunk boundaries, check filters and retrieved results, evaluate ranking, inspect the exact prompt and context, then examine the model output and citations. This identifies whether the problem is ingestion, retrieval, context construction, generation or validation.

### Q50. What is an LLM-as-a-judge?

**Answer:** It uses a model to score or compare generated answers against a rubric, reference answer or evidence. It can scale evaluation, but may be biased by response length, style, position or its own blind spots. Use explicit rubrics, blind pairwise comparisons where appropriate, human calibration and periodic audits.

### Q51. How do you evaluate abstention?

**Answer:** Measure whether the system answers when evidence is sufficient and abstains when it is insufficient. A system that refuses every question has low hallucination risk but little utility; a system that answers everything may be unreliable. Evaluate coverage, answer accuracy at that coverage, and the costs of false answers versus unnecessary abstentions.

---

# 8. Fine-Tuning and Parameter-Efficient Adaptation

### Q52. When should you fine-tune a model?

**Answer:** Consider fine-tuning when there is a stable, repeated behaviour that prompting and other simpler approaches cannot achieve reliably—for example, specialised extraction patterns, domain-specific language conventions or consistent output behaviour. Fine-tuning is less suitable as the only mechanism for frequently changing facts. Define a measurable baseline before investing in training.

### Q53. What data is needed for supervised fine-tuning?

**Answer:** Usually examples of inputs and desired outputs, formatted according to the model's training interface. Data should be high quality, representative, lawful to use and consistent with the intended behaviour. Remove duplicates, protect sensitive data, check labels and separate training, validation and test examples.

### Q54. What is supervised fine-tuning (SFT)?

**Answer:** SFT trains a pretrained model on examples of desired responses. The objective commonly maximises the likelihood of target output tokens conditioned on the input or conversation. It helps teach task behaviour and instruction following but does not guarantee factual accuracy.

### Q55. What is LoRA?

**Answer:** Low-Rank Adaptation adds trainable low-rank matrices to selected weight transformations while freezing most original weights. Instead of updating a full weight matrix \(W\), the learned update is represented approximately as \(\Delta W=BA\), where the intermediate rank is much smaller than the original dimensions. This reduces trainable parameter count and can reduce memory and storage costs.

### Q56. What is QLoRA?

**Answer:** QLoRA combines a quantised base model with trainable low-rank adapters. It can reduce memory requirements for fine-tuning larger models. Feasibility still depends on model size, quantisation support, sequence length, batch size, hardware and software compatibility.

### Q57. What is catastrophic forgetting in fine-tuning?

**Answer:** It is a decline in previously learned capabilities as the model adapts to new data. A narrow or low-quality fine-tuning dataset can make the model over-specialised. Evaluate both the target task and general capabilities that must be preserved.

### Q58. How do you know fine-tuning improved the model?

**Answer:** Compare the fine-tuned model against the original baseline on a held-out evaluation set, using the same conditions and task-specific metrics. Include quality, robustness, safety, latency and cost. Inspect regressions as well as improvements and avoid selecting the model only on training performance.

### Q59. What is the difference between RAG and fine-tuning in terms of knowledge updates?

**Answer:** In RAG, changing a source document can update what the system retrieves without changing model weights. In fine-tuning, changing learned behaviour or encoded patterns requires another training process. RAG also needs indexing and retrieval maintenance; it is not update-free.

### Q60. What is synthetic training data, and what are its risks?

**Answer:** Synthetic data is generated by a model or program instead of being collected entirely from human or real-world examples. It can increase coverage, but it may contain errors, biases, repetitive patterns or teacher-model quirks. Filter and validate it, preserve provenance, and test on independent real-world examples.

---

# 9. Agents, Tools and Workflows

## 9.1 The agent loop

A common tool-using loop is:

1. Receive the user's task.
2. Ask the model to choose an allowed next action.
3. Validate the proposed tool and arguments.
4. Execute the tool in application code.
5. Return the tool result to the model.
6. Continue until a stop condition, result or limit is reached.

The model proposes actions; the application enforces permissions and performs them.

### Q61. What is tool calling?

**Answer:** Tool calling lets a model request a structured action, such as searching documents, querying a database or calling a calculator. The backend validates the request, checks authorisation, executes the function and returns the result. Tool arguments must be validated just like any other untrusted input.

### Q62. What is the difference between an agent and a fixed workflow?

**Answer:** A fixed workflow follows predefined steps and branching rules. An agent allows the model to choose some steps or tools dynamically. Fixed workflows are often easier to test and control; agents are useful when the next action depends on uncertain intermediate results. Use the least autonomous design that meets the requirement.

### Q63. What are the risks of autonomous agents?

**Answer:** Agents may select incorrect tools, loop, misuse permissions, consume excessive resources, follow prompt injection, or take unintended actions. Controls include allowlisted tools, argument validation, least-privilege credentials, step and cost budgets, timeouts, audit logs and human confirmation for consequential actions.

### Q64. How should a tool be designed?

**Answer:** Give it a narrow purpose, a clear schema, typed arguments, explicit error responses and bounded outputs. Validate input and user permissions in code. Prefer read-only tools where possible, and separate high-impact write operations from routine lookups.

### Q65. Why should an LLM not directly execute arbitrary SQL?

**Answer:** Generated SQL may be incorrect, expensive, destructive or expose unauthorised data. Use parameterised queries, read-only database roles where possible, schema allowlists, query validation, timeouts and row limits. For write operations, require a controlled application service and appropriate authorisation.

### Q66. What is human-in-the-loop design?

**Answer:** It introduces human review or approval at steps where model confidence, risk or business impact warrants it. Examples include approving financial transactions, sending external messages or making high-impact decisions. Human review should be targeted to meaningful risk and supported by enough context to make a good decision.

### Q67. How do you prevent an agent from looping forever?

**Answer:** Set maximum steps, wall-clock deadlines, tool-call limits, token budgets and explicit stop conditions. Detect repeated actions where possible. Return a partial result or a clear failure state when the budget is exhausted.

### Q68. What is memory in an agent system?

**Answer:** “Memory” may refer to conversation history, a summarised user state, or external persistent records. It should be designed deliberately: define what is stored, why, for how long, who can access it and how users can correct or delete it. More stored context is not automatically better.

### Q69. What is the difference between short-term and long-term memory?

**Answer:** Short-term memory usually refers to current-session context or a temporary working state. Long-term memory persists across sessions in an external store. Long-term memory needs stronger lifecycle, privacy, relevance and access controls; it should not be treated as an unrestricted transcript archive.

### Q70. When should an agent use a tool instead of answering directly?

**Answer:** Use a tool when the answer depends on current or private data, deterministic calculation, an external state change or a capability the model does not possess. The application should decide which tools are available for the user's role and task, not expose every capability indiscriminately.

---

# 10. Multimodal GenAI

### Q71. What is multimodal RAG?

**Answer:** Multimodal RAG retrieves relevant information from sources containing different modalities, such as text, images, tables, audio or video. The pipeline may use OCR, image embeddings, transcription, frame extraction or modality-specific encoders. The retrieved evidence must preserve source references and modality context.

### Q72. How would you build question answering over scanned PDFs?

**Answer:** Detect whether pages contain text or images, apply OCR to scanned pages, preserve layout and page numbers, extract tables appropriately, and validate OCR quality. Then chunk the extracted content, index it and test retrieval on real questions. If visual layout itself carries meaning, use a layout-aware or multimodal approach instead of relying only on flattened text.

### Q73. What is OCR?

**Answer:** Optical Character Recognition converts text visible in images or scanned pages into machine-readable text. OCR can make documents searchable, but errors in small fonts, handwriting, tables or poor scans can corrupt downstream answers. Preserve the original page reference and evaluate extraction quality.

### Q74. How can an LLM work with audio?

**Answer:** Depending on the system, audio can be transcribed into text, represented by learned audio tokens or processed through a multimodal model. Tasks include speech recognition, summarisation, question answering and speech generation. Quality depends on language, noise, accents, timing and model capability.

### Q75. How would you handle video in a retrieval system?

**Answer:** Extract metadata and timestamps, sample or select frames, obtain transcripts where available, generate descriptions or embeddings, and index them with timestamps and source IDs. At query time, retrieve relevant segments and return references that let the user inspect the corresponding time range. Frame sampling must balance coverage, cost and temporal detail.

---

# 11. LLM Evaluation and Observability

### Q76. What is observability for an LLM application?

**Answer:** Observability is the ability to understand system behaviour from traces, logs and metrics. For GenAI, a trace may include retrieval duration, candidate IDs, model latency, token counts, tool calls, validation failures and final status. Sensitive prompts and documents should only be recorded when justified and properly protected.

### Q77. What is time to first token (TTFT)?

**Answer:** TTFT is the elapsed time from a request starting to the first generated token being delivered. It affects perceived responsiveness in streaming applications. Total completion latency and throughput should also be measured, because a fast first token does not guarantee a fast complete answer.

### Q78. What is token usage, and why monitor it?

**Answer:** Token usage counts input and output tokens according to the model/provider's accounting rules. It affects context limits, latency and cost. Track usage by feature and model, and watch for unexpectedly long prompts, retrieved context or generated outputs.

### Q79. What is a regression test for a prompt or model change?

**Answer:** It runs a fixed, versioned evaluation set against a new configuration and compares metrics with a baseline. The set should include common tasks, edge cases, unanswerable questions, security cases and examples from past failures. A change should be reviewed for both gains and regressions.

### Q80. How do you measure response quality when there is no single correct wording?

**Answer:** Use task-specific rubrics and criteria such as factual correctness, completeness, relevance, grounding, clarity and policy compliance. Exact string matching is unsuitable for many generative tasks. Human ratings, pairwise comparisons, structured checks and calibrated automated judges can be combined.

### Q81. What is online evaluation?

**Answer:** Online evaluation measures system behaviour in actual usage, using permitted feedback, sampled review and production metrics. It can reveal real query distributions and failure modes that offline datasets miss. It must respect privacy, consent, security and sampling bias.

---

# 12. Production Performance, Scaling and Cost

### Q82. How do you reduce LLM latency?

**Answer:** First measure where time is spent. Then consider a smaller or faster model, shorter prompts, fewer retrieved chunks, reranking only when beneficial, streaming, parallel independent calls, caching, batching and improved infrastructure. Test quality and reliability alongside latency; reducing tokens can remove important evidence.

### Q83. What is semantic caching?

**Answer:** Semantic caching attempts to reuse a previous result when a new query is sufficiently similar to a cached query. It can reduce repeated inference cost, but similarity alone does not prove that the answer remains correct for the new user or context. Use strict tenant and permission boundaries, freshness rules and conservative thresholds.

### Q84. What is the difference between caching an embedding and caching an answer?

**Answer:** An embedding cache reuses the vector for the same input text, reducing repeated embedding work. An answer cache reuses a generated result, which is more sensitive to changes in user permissions, source data, model version, prompt version and conversation context. Answer caching needs more careful invalidation and access control.

### Q85. How do you estimate cost per request?

**Answer:** Estimate input and output token usage, multiply by the applicable model prices, and add retrieval, reranking, embedding, storage and infrastructure costs where relevant. Pricing changes by provider and model, so use current pricing for the actual deployment. Measure actual usage in production rather than relying only on estimates.

### Q86. What is batching?

**Answer:** Batching processes multiple inputs in one operation to improve hardware or API efficiency. It is common for embedding jobs and offline inference. Batch size must respect token limits, memory, provider constraints and latency requirements.

### Q87. What is quantisation in deployment?

**Answer:** Quantisation reduces the precision used to store or process model values, which can lower memory requirements and sometimes improve throughput. It can affect output quality and hardware compatibility. Benchmark the actual quantised model on target tasks and hardware.

### Q88. What is graceful degradation?

**Answer:** Graceful degradation means preserving useful functionality when a component fails. For example, if an optional reranker is unavailable, the system may fall back to the base retriever if quality requirements permit. It should not silently produce a less trustworthy answer without monitoring or an appropriate user-visible status.

### Q89. How would you design for high concurrency?

**Answer:** Use asynchronous I/O where appropriate, bounded concurrency, queueing for expensive jobs, rate limits, backpressure, connection pooling and horizontal scaling. Measure provider limits and model-serving capacity. Avoid unbounded task creation and ensure cancellation releases resources.

---

# 13. Security, Privacy and Prompt-Injection Defence

### Q90. What is indirect prompt injection?

**Answer:** It occurs when malicious instructions are embedded in content the application retrieves or processes, such as a document, web page or email. The user may not have written those instructions, but the model can still encounter them in context.

### Q91. What is the safest way to handle retrieved content?

**Answer:** Treat it as untrusted data, clearly delimit it from system instructions, and never let its text grant new permissions. Enforce permissions and tool constraints in ordinary code. Do not place secrets in context and test whether malicious content can cause data disclosure or unauthorised actions.

### Q92. Is a system prompt a security boundary?

**Answer:** No. System instructions can guide model behaviour but should not be relied upon as the only protection for secrets, permissions or consequential actions. Security boundaries belong in authentication, authorisation, server-side validation, network controls and tool implementation.

### Q93. What is least privilege?

**Answer:** Least privilege gives a user, service or tool only the access required for its task. A document-search tool should not automatically have permission to delete documents; an agent should not receive unrestricted database credentials. Narrow permissions limit the impact of model mistakes or prompt injection.

### Q94. How do you prevent cross-tenant data leakage in RAG?

**Answer:** Enforce tenant and user permissions in the retrieval service and data layer, not through prompts alone. Apply mandatory filters before results reach the model, validate access to each returned source, isolate caches by permission context and test adversarial cross-tenant queries. Audit logs and automated access-control tests are important.

### Q95. How should sensitive data be handled in model requests?

**Answer:** Minimise the data sent, redact or transform sensitive fields where practical, use approved providers and configurations, restrict logging and retention, and follow applicable policies and legal obligations. Do not assume all model APIs have the same data-use or retention terms.

### Q96. What is output validation?

**Answer:** Output validation checks that a model response meets expected syntax, schema, range and business constraints. For example, a model may propose a date that is invalid or an account ID that the user cannot access. Validation should happen before the application acts on the result.

### Q97. How would you secure an LLM that can call external tools?

**Answer:** Use an allowlist of tools, validate all arguments, enforce authorisation on every call, isolate credentials, apply timeouts and resource limits, log actions, and require confirmation for high-impact operations. Return only the data needed for the next step. Tool outputs should also be treated as potentially untrusted.

---

# 14. GenAI Coding and Implementation Questions

## Q98. Write a simple cosine similarity function in Python.

```python
import math

def cosine_similarity(a: list[float], b: list[float]) -> float:
    if len(a) != len(b):
        raise ValueError("Vectors must have the same dimension")

    dot = sum(x * y for x, y in zip(a, b))
    norm_a = math.sqrt(sum(x * x for x in a))
    norm_b = math.sqrt(sum(y * y for y in b))

    if norm_a == 0 or norm_b == 0:
        raise ValueError("Cosine similarity is undefined for a zero vector")

    return dot / (norm_a * norm_b)

print(cosine_similarity([1, 0], [0.9, 0.1]))
```

**Follow-up:** Why should a real vector index use a tested library? Efficient nearest-neighbour search requires indexing, numerical handling and scaling beyond a simple loop.

## Q99. Write a function to select the top-k items by score.

```python
def top_k(items, k):
    if k < 0:
        raise ValueError("k must be non-negative")
    return sorted(items, key=lambda item: item["score"], reverse=True)[:k]

items = [
    {"id": "a", "score": 0.71},
    {"id": "b", "score": 0.93},
    {"id": "c", "score": 0.84},
]
print(top_k(items, 2))
```

**Complexity:** Sorting all \(n\) items is \(O(n\log n)\). For very large candidate sets and small \(k\), a heap can reduce the work to roughly \(O(n\log k)\).

## Q100. Write a simple chunking function.

```python
def chunk_words(text: str, size: int = 100, overlap: int = 20):
    if size <= 0:
        raise ValueError("size must be positive")
    if overlap < 0 or overlap >= size:
        raise ValueError("overlap must be in [0, size)")

    words = text.split()
    step = size - overlap

    for start in range(0, len(words), step):
        chunk = words[start:start + size]
        if not chunk:
            break
        yield " ".join(chunk)
        if start + size >= len(words):
            break
```

**Important limitation:** This is a teaching example based on words, not model tokens. Production chunking should consider token counts, sentence and section boundaries, tables, metadata and the embedding model's input limit.

## Q101. How would you validate an LLM-generated JSON object?

**Answer:** Parse the JSON, validate it against a schema, then check business rules. Reject or safely handle missing fields, unexpected values and malformed output. A schema library such as Pydantic can help in Python, but the exact implementation depends on the API contract.

```python
import json

def parse_json_object(raw: str):
    value = json.loads(raw)
    if not isinstance(value, dict):
        raise ValueError("Expected a JSON object")
    return value
```

This checks only basic JSON structure. It does not validate required fields or business semantics.

## Q102. How do you implement bounded retry logic?

**Answer:** Retry only errors that are likely to be transient, use a maximum attempt count and exponential backoff with jitter, and respect provider retry instructions. Avoid retrying invalid requests or authentication failures. State-changing tools need idempotency protection before retrying.

## Q103. What is the difference between synchronous and asynchronous API calls?

**Answer:** A synchronous call waits for the result before proceeding in that execution flow. An asynchronous call can yield while waiting for I/O, allowing other work to proceed. Async is useful for concurrent network-bound requests, but it requires careful exception handling, cancellation and concurrency limits.

## Q104. How would you implement a document ingestion pipeline?

**Answer:**
1. Accept a file through an authenticated endpoint.
2. Validate its type, size and content.
3. Store it in an approved location with a stable document ID.
4. Extract text or run OCR.
5. Clean the content without losing important structure.
6. Chunk the text and attach metadata and permissions.
7. Generate embeddings in bounded batches.
8. Upsert chunks into the index idempotently.
9. Record indexing status and extraction errors.
10. Support document update and deletion.

Do not mark a document as searchable until its indexing stage has completed successfully.

## Q105. How would you prevent duplicate indexing?

**Answer:** Assign stable document and chunk identifiers, track document versions or content hashes, and use idempotent upserts. On an update, replace or retire the old version according to the versioning policy. Test retries and partial failures so they do not leave duplicate or stale chunks.

---

# 15. Advanced Scenario-Based Interview Questions

## Scenario 1: Retrieval is good, but the answer is still wrong.

**Answer:** I would inspect the exact prompt and retrieved evidence. The model may ignore a relevant passage, combine conflicting passages incorrectly or infer more than the evidence supports. I would reduce irrelevant context, improve evidence ordering and instructions, require source-linked claims, test abstention and compare models if necessary. I would measure end-to-end quality after each change.

## Scenario 2: Retrieval misses a document that clearly contains the answer.

**Answer:** Verify that the document was ingested and the text was extracted correctly. Inspect chunk boundaries, metadata filters, query representation and top-ranked candidates. Compare dense retrieval with BM25 and hybrid search, test the embedding model, and consider query rewriting or reranking. Use labelled queries and Recall@k to verify the improvement.

## Scenario 3: A long policy document exceeds the context limit.

**Answer:** I would not send the whole document by default. I would retrieve relevant sections, preserve section titles and page references, rerank candidates and fit them into a token budget. For questions requiring whole-document synthesis, I might use hierarchical summarisation or a multi-stage process and verify that the final result covers all required sections.

## Scenario 4: The system cites a source that does not support its claim.

**Answer:** I would distinguish citation existence from citation correctness. Store source IDs and exact passages, constrain citations to retrieved candidates, and evaluate claim-to-source entailment. I would inspect whether the wrong passage was retrieved or whether the model attached an incorrect citation. Citation validation should be part of the evaluation suite.

## Scenario 5: A model update improves average scores but breaks an important use case.

**Answer:** I would examine per-category and worst-case metrics, not just the average. Keep a regression set for high-impact tasks, compare error types and determine whether the change affects prompts, formatting, refusal behaviour or factuality. Roll back or route the affected task to a known-good configuration until the regression is resolved.

## Scenario 6: The application is too expensive.

**Answer:** Instrument token usage and cost by feature. Identify whether the cost comes from large prompts, repeated requests, too many retrieval or agent steps, embeddings, reranking or an unnecessarily expensive model. Test shorter context, caching where safe, batching, a smaller model or a simpler workflow. Compare cost per successful task with quality and latency.

## Scenario 7: A company wants a chatbot over confidential HR documents.

**Answer:** Start with data classification and a permission model. Authenticate users, enforce document-level access control during retrieval, isolate tenant or role filters, minimise provider exposure and restrict logging. Test direct and indirect prompt injection, cross-user data leakage, citations and deletion. High-impact HR decisions should have appropriate human oversight and policy review.

## Scenario 8: An agent is asked to send an email to an external customer.

**Answer:** I would separate drafting from sending. The agent can draft a message using approved context, but the backend should validate the recipient and content and require confirmation before sending if the action is consequential. Use a restricted mail tool, audit the action and protect against retrieved text that tries to change recipients or disclose data.

## Scenario 9: You have one week to build a document Q&A prototype.

**Answer:** I would narrow the scope and build a reliable baseline: one supported document type, ingestion, chunking, embedding search, a simple grounded prompt and source references. I would create a small evaluation set early, then improve retrieval and error handling. I would avoid premature multi-agent designs and clearly document prototype limitations.

## Scenario 10: The model answers from outdated documents.

**Answer:** I would track document versions and timestamps, define source precedence, remove or mark stale records, and filter or rerank based on validity dates. The answer should disclose conflicts or uncertainty where appropriate. I would add tests for updates and deletions so stale information cannot silently remain authoritative.

## Scenario 11: A user reports that the chatbot is biased.

**Answer:** I would ask for concrete examples and define the expected behaviour and harm. Then I would build a representative test set, inspect training or retrieval sources, compare outcomes across relevant cases, and evaluate prompts, model behaviour and downstream rules. Mitigations should be tested for both effectiveness and unintended regressions.

## Scenario 12: A tool call returns an error halfway through a workflow.

**Answer:** The orchestrator should classify the error, decide whether it is retryable, preserve the state needed to resume and avoid repeating non-idempotent actions. If recovery is not safe, it should stop and report a clear failure or partial result. Logs should include a request or trace ID without exposing secrets.

---

# 16. Rapid-Fire Questions

### Q106. What is RAG recall?

The proportion of relevant evidence retrieved within the selected top-k results, under the evaluation's relevance labels.

### Q107. What is RAG faithfulness?

Whether the generated answer is supported by the retrieved evidence.

### Q108. What is a retriever?

The component that selects candidate documents or chunks for a query.

### Q109. What is a reranker?

A component that scores and reorders retrieved candidates for relevance.

### Q110. What is a corpus?

The collection of documents or records available for retrieval.

### Q111. What is an index?

A data structure that supports efficient search over a collection.

### Q112. What is an upsert?

An operation that inserts a record if absent or updates it if present, depending on the database semantics.

### Q113. What is idempotent ingestion?

Rerunning ingestion for the same document version does not create unintended duplicates or inconsistent state.

### Q114. What is a retrieval filter?

A condition restricting candidates by metadata such as tenant, date, source type or access permissions.

### Q115. What is a cross-encoder?

A model that evaluates a query and candidate together to produce a relevance score.

### Q116. What is a bi-encoder?

A model that independently embeds two inputs, enabling efficient vector comparison.

### Q117. What is RRF?

Reciprocal Rank Fusion, a method for combining ranked lists from different retrievers.

### Q118. What is SFT?

Supervised fine-tuning on examples of desired input-output behaviour.

### Q119. What is LoRA?

A parameter-efficient adaptation method that learns low-rank weight updates.

### Q120. What is QLoRA?

Fine-tuning with a quantised base model and trainable low-rank adapters.

### Q121. What is an agent tool budget?

A limit on the number, duration, token usage or cost of tool interactions.

### Q122. What is human approval gating?

A requirement for a person to approve a consequential action before execution.

### Q123. What is semantic caching?

Reusing a stored result for a sufficiently similar query, subject to freshness and permission checks.

### Q124. What is TTFT?

Time to first token, a measure of how quickly streaming output begins.

### Q125. What is backpressure?

A mechanism that prevents incoming work from overwhelming downstream services.

### Q126. What is a dead-letter queue?

A place to route jobs that repeatedly fail so they can be inspected or handled separately.

### Q127. What is model drift?

A change in input patterns or system performance over time that makes the deployed solution less effective.

### Q128. What is a golden dataset?

A curated, versioned set of examples with trusted answers or evaluation labels used for regression testing.

### Q129. What is a prompt template?

A reusable structure that inserts task instructions, variables and context into a model request.

### Q130. What is a model fallback?

A tested alternative model or service used when the primary model is unavailable or unsuitable, subject to data and quality constraints.

### Q131. What is a token budget?

A limit or allocation for input and output tokens within a request or workflow.

### Q132. What is a safety filter?

A component that checks input or output against defined safety or policy criteria. It should be tested for both missed harmful content and excessive blocking.

### Q133. Why should LLM output not determine permissions?

Permissions must be enforced by trusted application logic. Model output can be wrong or manipulated and must not replace authentication or authorisation.

### Q134. What is a canary deployment?

A release strategy that sends a small portion of traffic to a new version first, monitors results and expands or rolls back based on evidence.

### Q135. What is a rollback plan?

A defined procedure for returning to a previous stable version of a model, prompt, index or application when a release causes regressions.

---

# 17. Final Revision Checklist

Mark each item only when you can explain it aloud and answer a follow-up question.

- [ ] Draw a complete RAG architecture from ingestion to response.
- [ ] Explain the difference between RAG, fine-tuning and prompt engineering.
- [ ] Compare fixed-size, semantic and structure-aware chunking.
- [ ] Explain chunk overlap, parent-child retrieval and metadata.
- [ ] Explain dense retrieval, BM25 and hybrid search.
- [ ] Explain HNSW/ANN at a high level.
- [ ] Explain bi-encoders, cross-encoders and reranking.
- [ ] Explain query rewriting, multi-query retrieval and HyDE.
- [ ] Distinguish citation validity, answer correctness and faithfulness.
- [ ] Calculate Precision@k and Recall@k for a small example.
- [ ] Explain MRR, nDCG and end-to-end evaluation.
- [ ] Describe an LLM-as-a-judge evaluation with limitations.
- [ ] Explain SFT, LoRA and QLoRA.
- [ ] Explain tool calling, fixed workflows and agents.
- [ ] Design least-privilege tool execution with human approval.
- [ ] Explain multimodal document processing and OCR.
- [ ] Measure latency, TTFT, token usage and cost.
- [ ] Explain caching, batching, rate limits and graceful degradation.
- [ ] Defend against direct and indirect prompt injection.
- [ ] Explain cross-tenant isolation and output validation.
- [ ] Write Python for cosine similarity, top-k selection, chunking and JSON parsing.
- [ ] Debug RAG failures stage by stage.
- [ ] Answer all twelve advanced scenarios using evidence and trade-offs.

## Recommended practice method

1. Pick five questions each day.
2. Answer each in 60–90 seconds without reading.
3. Draw a diagram for RAG, agents and the ingestion pipeline.
4. Implement the coding questions and test edge cases.
5. For every scenario, state the likely causes, the diagnostic evidence, the proposed fix and the metric that will confirm improvement.

---

## Final interview advice

Strong GenAI engineering answers connect a technique to a measurable outcome. Do not simply say “I will use RAG” or “I will use an agent.” Explain why that design fits the problem, what can fail, how you would evaluate it, and how you would protect user data.

**End of Part 2 — Advanced GenAI Engineering.**

Part 3 should focus on hands-on Python and SQL exercises, API/debugging tasks, GenAI system-design interviews, project deep dives, and a realistic interviewer-candidate mock interview.
