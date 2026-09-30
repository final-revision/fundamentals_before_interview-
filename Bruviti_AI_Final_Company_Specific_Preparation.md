# Bruviti AI — Final Company-Specific Preparation File

## Purpose

This is the **third and final preparation file**.

The first two files covered:

1. General AI/ML + Edge/IoT technical concepts
2. Python coding + DSA + coding interview questions

This file covers the **remaining Bruviti-specific areas** that are important for the company:

- What Bruviti actually builds
- Its current AI product direction
- Aftermarket service AI
- Agentic AI
- AIP architecture
- Domain-specific/small language models
- Ontology and knowledge graphs
- RAG and agentic retrieval
- Enterprise system integration
- API-first architecture
- Edge/offline/air-gapped deployment
- Data sovereignty and security
- AI evaluation and monitoring
- Predictive forecasting
- Real-world AI scenarios
- System-design questions
- Project/resume technical questions
- Questions an interviewer can ask after a technical assessment
- Trade-off questions
- "Why did you choose this?" questions
- Bruviti-specific rapid revision

---

# 1. First Understand What Bruviti Actually Does

## Q1. What is Bruviti?

**Answer:**

Bruviti is an AI technology company focused on **mission-critical service operations for equipment manufacturers**.

Its current platform is called the **Aftermarket Intelligence Platform (AIP)**.

The platform brings together:

- Service data
- Asset/equipment data
- Parts data
- Policy/warranty data
- Enterprise applications
- AI models
- Agentic workflows

The goal is to automate service workflows such as:

- Issue triage
- Diagnosis
- Parts identification
- Technician dispatch
- Warranty processing
- Case resolution
- Service support

Bruviti describes its platform as production AI for mission-critical service operations. Its current product material emphasizes domain-specialized AI, agentic automation, governance, and enterprise deployment.

---

# 2. What is Aftermarket Service?

## Q2. What does "aftermarket service" mean?

**Answer:**

Aftermarket service refers to the services provided **after a product or piece of equipment has been sold**.

For an equipment manufacturer, this can include:

- Installation
- Maintenance
- Repairs
- Spare parts
- Warranty
- Technical support
- Field service
- Troubleshooting

### Example

A company sells an industrial machine.

After the machine is installed:

`Machine develops fault`
→ `Customer reports issue`
→ `Support diagnoses problem`
→ `Required part identified`
→ `Technician dispatched`
→ `Repair completed`
→ `Warranty/claim processed`

Bruviti's AI platform is designed to automate parts of this workflow.

---

# 3. What is AIP?

## Q3. What is Bruviti AIP?

**Answer:**

AIP stands for **Aftermarket Intelligence Platform**.

It is Bruviti's domain-specialized AI platform for aftermarket service operations.

The platform is designed to:

1. Unify enterprise service/asset/parts/policy data.
2. Apply domain logic.
3. Use specialized AI models.
4. Select appropriate workflows.
5. Execute actions across enterprise systems.
6. Monitor outcomes and improve the system.

A simplified view is:

```text
Enterprise Data
      ↓
Data Unification
      ↓
Domain Knowledge / Ontology
      ↓
AI Reasoning
      ↓
Agentic Workflow
      ↓
Enterprise Actions
      ↓
Monitoring / Evaluation
```

---

# 4. Why Does Bruviti Need Domain-Specific AI?

## Q4. Why not simply use a general-purpose LLM?

**Answer:**

A general-purpose LLM may understand language very well, but enterprise equipment-service tasks require highly specific knowledge.

For example:

- Equipment models
- Component relationships
- Failure modes
- Parts
- Service procedures
- Warranty rules
- Customer entitlements
- Technician skills
- Inventory
- Operational constraints

A specialized system can combine:

**Domain data + domain rules + specialized models + enterprise systems**

to produce more controlled and useful decisions.

---

# 5. Small Language Models

## Q5. What is a Small Language Model?

**Answer:**

A Small Language Model (SLM) is a language model with a smaller parameter count and computational requirement than large general-purpose language models.

Advantages can include:

- Lower latency
- Lower compute requirements
- Easier deployment
- Lower resource consumption
- Better suitability for specialized tasks

For enterprise/edge environments, a smaller specialized model can sometimes be more practical than a very large general-purpose model.

---

# 6. LLM vs SLM

| LLM | SLM |
|---|---|
| Usually larger | Usually smaller |
| High compute requirements | Lower compute requirements |
| Broad capabilities | Often specialized |
| May require significant infrastructure | Easier to deploy in constrained environments |
| Useful for broad language tasks | Useful for targeted/domain tasks |

The choice depends on the problem, accuracy requirements, latency, infrastructure, and cost.

---

# 7. Agentic AI

## Q6. What is Agentic AI?

**Answer:**

Agentic AI refers to AI systems that can perform a sequence of actions toward a goal rather than only producing a single response.

A simplified workflow:

```text
Goal
 ↓
Understand problem
 ↓
Retrieve information
 ↓
Reason
 ↓
Choose action
 ↓
Execute action
 ↓
Observe result
 ↓
Continue / correct
```

---

# 8. Traditional AI vs Agentic AI

### Traditional AI

```text
Input
 ↓
Model
 ↓
Prediction
```

### Agentic AI

```text
Goal
 ↓
Reason
 ↓
Retrieve
 ↓
Plan
 ↓
Use tools
 ↓
Take action
 ↓
Observe
 ↓
Continue
```

Bruviti's current AIP material describes agentic workflows that can perform multi-step service operations across systems.

---

# 9. What is an AI Agent?

## Q7. What is an AI agent?

**Answer:**

An AI agent is a software system that can:

- Understand a goal
- Gather relevant information
- Reason about the situation
- Select actions
- Use tools/APIs
- Observe results
- Continue until the task is completed or requires human intervention

---

# 10. Example of a Bruviti-Style Agent

Suppose an industrial machine reports an error.

The system could:

```text
Receive Service Case
       ↓
Identify Equipment
       ↓
Read Error Code
       ↓
Retrieve Technical Information
       ↓
Analyze Symptoms
       ↓
Identify Possible Failure
       ↓
Check Required Part
       ↓
Check Inventory
       ↓
Check Warranty
       ↓
Create/Update Work Order
       ↓
Schedule Technician
```

This is much closer to an **agentic workflow** than a simple chatbot.

---

# 11. What is RAG?

## Q8. What is Retrieval-Augmented Generation?

**Answer:**

RAG combines information retrieval with a generative AI model.

Instead of asking an LLM to answer entirely from its internal training, the system first retrieves relevant information from an external knowledge source.

```text
User/Agent Query
       ↓
Retriever
       ↓
Relevant Documents/Data
       ↓
LLM
       ↓
Answer
```

---

# 12. Why is RAG Useful for Enterprise AI?

**Answer:**

Enterprise information changes frequently and is often private.

Examples:

- Service manuals
- Product documentation
- Warranty rules
- Parts catalogs
- Internal procedures
- Service history

RAG allows the system to retrieve current/relevant information rather than relying only on model memory.

---

# 13. RAG vs Fine-Tuning

| RAG | Fine-Tuning |
|---|---|
| Adds external information at inference time | Changes model behavior through additional training |
| Good for frequently changing knowledge | Good for specialized behavior/style/tasks |
| Knowledge can be updated by changing retrieval source | Updating knowledge may require retraining |
| Useful for private documents | Useful for adapting model behavior |

They can also be used together.

---

# 14. What is an Ontology?

## Q9. What is a service-domain ontology?

**Answer:**

An ontology is a structured representation of entities, concepts, and relationships in a particular domain.

For equipment service, it can represent:

```text
Equipment
   ↓
Component
   ↓
Failure Mode
   ↓
Symptom
   ↓
Repair Procedure
   ↓
Part
```

It can also represent relationships involving:

- Equipment models
- Components
- Symptoms
- Faults
- Parts
- Procedures
- Warranty
- Service history

---

# 15. Why Does an Ontology Help AI?

**Answer:**

An ontology provides structured context.

Instead of treating every piece of text as unrelated information, the system can understand relationships.

Example:

```text
Machine A
   has component → Pump X
Pump X
   can experience → Pressure Failure
Pressure Failure
   may require → Valve Y
Valve Y
   belongs to → Part Category Z
```

This can improve retrieval, reasoning, and consistency.

---

# 16. Knowledge Graph vs Ontology

**Answer:**

An ontology defines the concepts and relationships that are allowed or meaningful in a domain.

A knowledge graph represents actual entities and relationships using those concepts.

Example:

### Ontology

```text
Machine → hasComponent → Component
```

### Knowledge Graph

```text
Machine_101 → hasComponent → Pump_45
```

---

# 17. Agentic Retrieval

## Q10. What is agentic retrieval?

**Answer:**

Agentic retrieval means the system can determine what information it needs, perform one or more retrieval steps, and use the retrieved context as part of a larger reasoning workflow.

Example:

```text
Identify machine
 ↓
Retrieve machine history
 ↓
Retrieve related fault codes
 ↓
Retrieve service manual
 ↓
Retrieve available parts
 ↓
Reason about solution
```

---

# 18. Enterprise Integration

## Q11. How can Bruviti integrate with existing enterprise systems?

**Answer:**

AIP uses an API-first integration approach and can connect with enterprise systems such as:

- CRM
- ERP
- Field Service Management systems
- Contact center platforms
- Databases
- Files/data sources

The important idea is:

```text
Existing Enterprise Systems
          ↕
      Integration Layer
          ↕
       AI Platform
```

This means companies do not necessarily have to replace all their existing systems.

---

# 19. What is API-First Architecture?

## Q12. What does API-first mean?

**Answer:**

API-first means designing the system's interfaces as a primary part of the architecture.

Other systems can interact with the platform through defined APIs.

For example:

```text
CRM
 ↓
API
 ↓
AI Platform
 ↓
API
 ↓
ERP / FSM
```

---

# 20. Bidirectional Integration

## Q13. What does bidirectional integration mean?

**Answer:**

The AI platform can both **read information from** enterprise systems and **write actions/results back** to them.

Example:

```text
CRM → Customer case → AI
AI → Resolution → CRM

ERP → Inventory → AI
AI → Parts request → ERP
```

---

# 21. Legacy Systems

## Q14. How can AI integrate with a legacy system that does not have an API?

**Answer:**

Possible approaches include:

- Database connectors
- File-based integration
- Middleware
- UI/desktop automation
- Event-based integration where available

The key principle is to build an integration layer rather than forcing the AI system to directly depend on the legacy implementation.

Bruviti's technical documentation specifically describes connectors and vision-based desktop automation for legacy systems without APIs.

---

# 22. Edge and Offline Deployment

## Q15. Why would an enterprise AI platform need edge or offline deployment?

**Answer:**

Some environments cannot depend on continuous internet connectivity.

Examples:

- Industrial plants
- Semiconductor fabs
- Secure facilities
- Remote locations
- Critical infrastructure

Edge/offline deployment can provide:

- Local processing
- Low latency
- Operational continuity
- Reduced external network dependency

---

# 23. What is an Air-Gapped Environment?

## Q16. What does air-gapped mean?

**Answer:**

An air-gapped environment is isolated from external networks, particularly the public internet.

Systems operating there must be designed to function without normal external network access.

This is important for highly sensitive or critical environments.

---

# 24. Data Sovereignty

## Q17. What is data sovereignty?

**Answer:**

Data sovereignty refers to keeping data under the required legal, organizational, and infrastructure controls of the organization or jurisdiction governing that data.

For enterprise AI, this can involve:

- Where data is stored
- Who can access it
- Where models run
- Whether data leaves the organization's environment

Bruviti's current technical material emphasizes self-hosted deployment, enterprise perimeter controls, and data remaining within the customer's infrastructure.

---

# 25. Why Is Data Security Important for Enterprise AI?

**Answer:**

Enterprise data can include:

- Customer information
- Equipment information
- Service records
- Internal documentation
- Business processes
- Parts information

Sending sensitive information to uncontrolled external services can create security, privacy, and compliance risks.

Therefore enterprise AI needs:

- Access control
- Encryption
- Audit logs
- Data isolation
- Governance
- Secure deployment

---

# 26. AI Hallucination

## Q18. What is an AI hallucination?

**Answer:**

An AI hallucination occurs when a generative model produces information that appears plausible but is incorrect, unsupported, or fabricated.

Example:

An AI system invents a part number that does not exist.

This can be dangerous in industrial service operations.

---

# 27. How Can Enterprise AI Reduce Hallucination?

**Answer:**

Possible techniques:

1. Retrieval from trusted sources
2. Domain constraints
3. Structured data
4. Ontologies
5. Tool/API verification
6. Output validation
7. Human approval for high-risk actions
8. Evaluation pipelines
9. Audit trails

---

# 28. What Are Guardrails?

## Q19. What are AI guardrails?

**Answer:**

Guardrails are controls that constrain AI behavior.

Examples:

- Allowed actions
- Input validation
- Output validation
- Access restrictions
- Safety policies
- Confidence thresholds
- Human approval
- Tool permissions

Example:

```text
AI wants to issue a warranty payment
          ↓
Policy Check
          ↓
Authorized?
          ↓
YES → Execute
NO → Human Review
```

---

# 29. AI Evaluation

## Q20. Why is evaluating an AI system different from testing a normal program?

**Answer:**

Traditional programs often have deterministic expected outputs.

AI systems can produce different outputs for similar inputs.

Therefore evaluation can consider:

- Accuracy
- Relevance
- Groundedness
- Reliability
- Latency
- Cost
- Safety
- Business outcomes

---

# 30. What Is Model Drift?

## Q21. What is model drift?

**Answer:**

Model drift occurs when the relationship between input data and the target behavior changes over time, causing model performance to decline.

Example:

A machine's operating conditions change after a hardware redesign.

A predictive-maintenance model trained on old equipment may become less accurate.

---

# 31. What Is Data Drift?

**Answer:**

Data drift occurs when the distribution of input data changes over time.

Example:

Training temperature range:

`20°C – 40°C`

Production environment later:

`35°C – 70°C`

The input distribution has changed.

---

# 32. Why Is Monitoring Important?

**Answer:**

A deployed AI system must be monitored because:

- Data changes
- User behavior changes
- Equipment changes
- Models degrade
- Latency changes
- Integrations fail
- Business outcomes change

A production AI platform needs continuous monitoring and evaluation.

---

# 33. Predictive Maintenance

## Q22. What is predictive maintenance?

**Answer:**

Predictive maintenance uses data and analytics/ML to predict equipment problems before failure occurs.

Typical flow:

```text
Sensors
 ↓
Historical + Real-Time Data
 ↓
Feature Processing
 ↓
ML Model
 ↓
Failure/Risk Prediction
 ↓
Maintenance Action
```

---

# 34. Predictive Parts Forecasting

## Q23. What is parts forecasting?

**Answer:**

Parts forecasting estimates future demand for replacement parts.

Inputs may include:

- Historical failures
- Equipment population
- Usage
- Seasonality
- Service history
- Inventory
- Failure patterns

The output can help organizations maintain appropriate inventory.

---

# 35. First-Time Fix Rate

## Q24. What is First-Time Fix Rate?

**Answer:**

First-Time Fix Rate measures how often a service issue is successfully resolved during the first service visit.

Higher first-time resolution generally means fewer repeat visits and less downtime.

AI can help improve it by:

- Better diagnosis
- Correct parts prediction
- Better technician guidance
- Better service information

---

# 36. MTTR

## Q25. What is MTTR?

**Answer:**

MTTR commonly means **Mean Time to Repair** or **Mean Time to Resolution**, depending on the operational context.

It measures the average time required to restore service or resolve an issue.

Reducing MTTR is important in mission-critical service environments.

---

# 37. Bruviti-Style System Design Question

## Q26. Design an AI system that diagnoses equipment faults.

### Possible answer

```text
                  ┌───────────────┐
                  │   Equipment   │
                  └───────┬───────┘
                          │
                       Sensors
                          │
                          ▼
                  ┌───────────────┐
                  │ Edge / Gateway│
                  └───────┬───────┘
                          │
                    Preprocessing
                          │
                          ▼
                ┌──────────────────┐
                │ AI / ML Inference│
                └────────┬─────────┘
                         │
                    Fault detected
                         │
                         ▼
               ┌────────────────────┐
               │ Knowledge / RAG /  │
               │ Domain Ontology    │
               └─────────┬──────────┘
                         │
                         ▼
                 Diagnosis / Action
                         │
              ┌──────────┴──────────┐
              ▼                     ▼
          Technician              ERP/FSM
          Workflow               System
```

### Important considerations

- Low latency
- Data quality
- Model accuracy
- Security
- Explainability
- Fault tolerance
- Offline capability
- Integration
- Monitoring

---

# 38. System Design Follow-Up Questions

After you design the system, an interviewer may ask:

### Q: What if the network goes down?

**Answer:**

Keep critical processing at the edge and synchronize data later when connectivity is restored.

### Q: What if the ML model is wrong?

**Answer:**

Use confidence thresholds, validation, guardrails, and human escalation for high-risk decisions.

### Q: How will you update the model?

**Answer:**

Use controlled model versioning and deployment, monitor performance, validate new models, and roll back if necessary.

### Q: How will you protect the data?

**Answer:**

Use authentication, authorization, encryption, secure communication, audit logs, and appropriate deployment boundaries.

### Q: What happens if an enterprise API is unavailable?

**Answer:**

Use retries with backoff, queues where appropriate, idempotent operations, monitoring, and graceful degradation.

---

# 39. Fault Tolerance

## Q27. What is fault tolerance?

**Answer:**

Fault tolerance is the ability of a system to continue operating, possibly with reduced functionality, when one or more components fail.

Example:

```text
Cloud unavailable
       ↓
Edge continues local inference
       ↓
Store events locally
       ↓
Cloud returns
       ↓
Synchronize data
```

---

# 40. What Is Graceful Degradation?

**Answer:**

Graceful degradation means the system continues providing essential functionality even when some components fail.

Example:

If cloud analytics becomes unavailable:

- Local device still detects critical faults.
- Non-critical analytics waits until the cloud returns.

---

# 41. Idempotency

## Q28. What is idempotency?

**Answer:**

An operation is idempotent if repeating it produces the same intended final state.

Example:

Suppose an API request is:

`Set ticket status = RESOLVED`

Sending it twice should still result in:

`RESOLVED`

This is important when systems retry requests after network failures.

---

# 42. Event-Driven Architecture

## Q29. What is event-driven architecture?

**Answer:**

In event-driven architecture, components communicate through events.

Example:

```text
Machine Fault Detected
        ↓
      Event
        ↓
Message Broker
   ↓          ↓
AI Service   Alert Service
```

Advantages:

- Loose coupling
- Scalability
- Asynchronous processing
- Better integration between services

---

# 43. Message Queue

## Q30. Why use a message queue?

**Answer:**

A message queue allows components to communicate asynchronously.

Benefits:

- Buffering
- Retry
- Load management
- Fault isolation
- Decoupling

Example:

```text
Sensor Events
     ↓
Message Queue
     ↓
AI Processing Workers
```

---

# 44. Real-Time vs Batch Processing

| Real-Time | Batch |
|---|---|
| Processes data quickly after arrival | Processes data in groups |
| Low latency | Higher latency acceptable |
| Alerts/monitoring | Reports/large analytics |
| More infrastructure complexity | Often simpler |

A Bruviti-like service system may use both.

---

# 45. CAP Theorem

## Q31. What is CAP theorem?

**Answer:**

CAP theorem states that a distributed data system cannot simultaneously guarantee all three of:

- Consistency
- Availability
- Partition tolerance

during a network partition.

### Consistency
Every read sees the appropriate latest value.

### Availability
Every request receives a response.

### Partition tolerance
The system continues despite network partition.

---

# 46. Caching

## Q32. Why use caching?

**Answer:**

Caching stores frequently accessed data closer to the application.

Benefits:

- Lower latency
- Reduced database load
- Faster responses

Example:

Frequently accessed equipment metadata can be cached.

---

# 47. Database Questions Relevant to Bruviti

## Q33. Why might an AI enterprise platform use multiple types of databases?

**Answer:**

Different workloads have different requirements.

For example:

- Relational DB → transactional enterprise data
- Document DB → flexible records
- Vector DB → embedding similarity search
- Graph DB → relationships
- Time-series DB → sensor measurements

The architecture should select storage based on the workload.

---

# 48. What Is a Vector Database?

**Answer:**

A vector database stores vector representations called embeddings and allows similarity search.

Typical RAG flow:

```text
Document
 ↓
Embedding Model
 ↓
Vector
 ↓
Vector Database
```

Query:

```text
User Query
 ↓
Embedding
 ↓
Similarity Search
 ↓
Relevant Documents
```

---

# 49. What Is an Embedding?

**Answer:**

An embedding is a numerical vector representation of data such as text.

Similar concepts tend to have vectors that are close according to an appropriate similarity metric.

Embeddings are widely used in:

- Semantic search
- RAG
- Recommendation
- Clustering

---

# 50. Semantic Search vs Keyword Search

### Keyword Search

Looks primarily for exact or related words.

### Semantic Search

Attempts to retrieve information based on meaning using representations such as embeddings.

Example:

Query:

> "machine is overheating"

Semantic search may retrieve documentation about:

- Excessive temperature
- Thermal failure
- Cooling-system problems

even if the exact phrase "overheating" does not appear.

---

# 51. AI + Enterprise Workflow

## Q34. Why is workflow automation important?

**Answer:**

A model prediction by itself does not necessarily solve the business problem.

For example:

```text
AI predicts required part
```

is useful, but a complete workflow might be:

```text
Predict part
 ↓
Check inventory
 ↓
Reserve part
 ↓
Create work order
 ↓
Assign technician
 ↓
Update customer case
```

This is why agentic workflow automation is important.

---

# 52. Human-in-the-Loop

## Q35. What is human-in-the-loop AI?

**Answer:**

Human-in-the-loop AI means humans remain involved in decisions where human judgment or approval is important.

Example:

```text
AI Recommendation
       ↓
Confidence Check
       ↓
High confidence → Automatic action
Low confidence → Human review
```

This is useful for high-impact or uncertain decisions.

---

# 53. AI Explainability

## Q36. Why is explainability important in enterprise AI?

**Answer:**

Enterprise users may need to understand why a system made a recommendation.

For example:

> "Why did the system recommend replacing this part?"

A useful system can provide supporting evidence such as:

- Fault history
- Sensor readings
- Service documentation
- Similar previous cases
- Model reasoning signals where appropriate

---

# 54. Security Questions

## Q37. Authentication vs Authorization

**Answer:**

Authentication:

> Who are you?

Authorization:

> What are you allowed to do?

---

## Q38. What is RBAC?

**Answer:**

RBAC stands for Role-Based Access Control.

Permissions are assigned based on roles.

Example:

```text
Technician → View service cases
Manager → Approve service actions
Admin → Manage users
```

---

# 55. Encryption

## Q39. What is encryption at rest?

**Answer:**

Protecting stored data.

Examples:

- Database
- Disk
- Object storage

---

## Q40. What is encryption in transit?

**Answer:**

Protecting data while it travels between systems, commonly using secure protocols such as TLS.

---

# 56. Logging and Audit Trails

## Q41. Why are audit logs important for AI systems?

**Answer:**

Audit logs can record:

- Who accessed data
- What action was performed
- When it happened
- Which model/version was used
- What system was called
- What decision/action occurred

This is particularly important in enterprise environments.

---

# 57. Model Versioning

## Q42. Why should ML models be versioned?

**Answer:**

Versioning allows teams to:

- Track model changes
- Compare performance
- Reproduce results
- Roll back bad models
- Audit production behavior

Example:

```text
Model v1 → Production
Model v2 → Testing
Model v3 → Development
```

---

# 58. CI/CD for AI

## Q43. What is CI/CD?

**Answer:**

CI/CD refers to practices that automate software integration, testing, and deployment.

For AI systems, the pipeline can additionally include:

- Data validation
- Model evaluation
- Model versioning
- Security checks
- Deployment validation
- Monitoring

---

# 59. MLOps

## Q44. What is MLOps?

**Answer:**

MLOps applies software engineering and DevOps principles to the ML lifecycle.

It covers:

```text
Data
 ↓
Training
 ↓
Evaluation
 ↓
Model Registry
 ↓
Deployment
 ↓
Monitoring
 ↓
Retraining
```

---

# 60. Important Bruviti-Specific Scenario Questions

## Q45. A customer has sensitive industrial data and does not allow it to leave its infrastructure. What architecture could you propose?

**Answer:**

Use an on-premise/private or air-gapped deployment where the AI platform and relevant data remain inside the customer's environment.

Important considerations:

- Data sovereignty
- Access control
- Local model inference
- Auditability
- No unnecessary external API dependency

---

## Q46. A factory has unreliable internet connectivity. How would you design the AI system?

**Answer:**

Use an edge-first architecture for critical operations.

```text
Sensors
 ↓
Edge Gateway
 ↓
Local Processing / AI
 ↓
Immediate Action

        +

Local Storage
 ↓
Synchronize with Cloud when available
```

---

## Q47. The AI recommends a part, but inventory says the part is unavailable. What should happen?

**Answer:**

The workflow should not blindly execute the recommendation.

Possible next step:

```text
AI recommends Part A
        ↓
Check Inventory
        ↓
Unavailable
        ↓
Find compatible alternative
OR
Escalate
OR
Reschedule
```

This demonstrates that **AI prediction and business workflow are different layers**.

---

# 61. Scenario: Model Gives Low Confidence

## Q48. What should happen if an AI model has low confidence?

**Answer:**

Depending on the risk:

- Request additional information
- Retrieve more evidence
- Try another model
- Escalate to human
- Avoid taking an irreversible action

A good production AI system should not assume every prediction is correct.

---

# 62. Scenario: Sensor Data Is Noisy

## Q49. How would you handle noisy sensor data?

**Answer:**

Possible methods:

- Filtering
- Smoothing
- Outlier detection
- Aggregation
- Sensor calibration
- Missing-value handling
- Feature engineering

The method depends on the sensor and application.

---

# 63. Scenario: One Service Fails

## Q50. The AI system depends on five services and one becomes unavailable. What should you consider?

**Answer:**

Consider:

- Retry policy
- Timeout
- Circuit breaker
- Queueing
- Fallback
- Graceful degradation
- Monitoring
- Alerting
- Idempotency

The correct strategy depends on whether the failed service is critical.

---

# 64. Circuit Breaker

## Q51. What is a circuit breaker?

**Answer:**

A circuit breaker prevents repeated calls to a failing service.

Typical states:

```text
Closed
  ↓ failures
Open
  ↓ after recovery period
Half-Open
  ↓ success
Closed
```

It helps prevent cascading failures.

---

# 65. Resume/Project Questions

The technical expert may connect questions to the projects on your resume.

Prepare to explain every project using:

```text
Problem
 ↓
Solution
 ↓
Architecture
 ↓
Technology
 ↓
Your contribution
 ↓
Challenges
 ↓
Trade-offs
 ↓
Result
```

---

# 66. If They Ask About Your AI Project

Prepare these questions:

### Q: Why did you choose this model?

Answer using:

- Dataset
- Accuracy
- Latency
- Resource constraints
- Interpretability
- Deployment environment

### Q: How did you evaluate it?

Mention:

- Train/test split
- Appropriate metrics
- Validation
- Error analysis

### Q: What happens if the model fails?

Mention:

- Validation
- Confidence thresholds
- Fallback
- Human intervention

---

# 67. If They Ask About Your Backend Project

Prepare:

- API architecture
- Authentication
- Database
- Validation
- Error handling
- Logging
- Deployment
- Scalability
- Security

A common architecture:

```text
Frontend
   ↓
REST API
   ↓
Backend
   ↓
Database
```

---

# 68. "Why Did You Choose This Technology?"

Never answer only:

> "Because it is popular."

Better structure:

```text
Requirement
 ↓
Technology choice
 ↓
Reason
 ↓
Trade-off
```

Example:

> "I chose MongoDB because the data structure was flexible and document-oriented. The trade-off is that relational workloads requiring complex joins may be better suited to SQL."

---

# 69. "How Would You Scale Your Project?"

Possible answer:

1. Load balancing
2. Horizontal scaling
3. Database indexing
4. Caching
5. Asynchronous processing
6. Message queues
7. CDN where appropriate
8. Monitoring
9. Containerization
10. Database scaling strategy

---

# 70. "What Was the Most Difficult Technical Problem?"

Use:

```text
Problem
 ↓
Why it happened
 ↓
Investigation
 ↓
Solution
 ↓
Trade-off
 ↓
What you learned
```

Do not invent a technically impressive problem you did not actually encounter.

---

# 71. Very Important: Bruviti's Current Interview Philosophy

Bruviti has publicly discussed changing its technical interview approach.

A recent post from Bruviti describes technical interviews using **realistic, open-ended problems** rather than only blank-editor timed coding exercises. The company says candidates may use normal tools, including AI, and that interviewers are interested in:

- How candidates think
- Why they choose an approach
- Trade-offs
- What they trust AI to do
- What they verify themselves
- How they would improve the solution

This is especially important to understand for the technical interaction after the written assessment.

**Source:** Bruviti's public LinkedIn post by Saurabh Moghe, shared by Bruviti. [Current as of September 2026.]

---

# 72. What This Means for Your Technical Interaction

Do not prepare only:

> "Can I write the code?"

Also prepare:

> "Can I explain why I wrote it this way?"

Be ready for:

### Q:
Why did you choose a dictionary?

### Q:
What happens if the input is very large?

### Q:
What are the edge cases?

### Q:
What would you change in production?

### Q:
What if the database is unavailable?

### Q:
What if the API fails?

### Q:
What if the model gives incorrect output?

### Q:
What did you verify yourself?

### Q:
What would you improve with more time?

---

# 73. AI-Assisted Coding

If an interviewer asks about using AI while coding:

A strong technical answer is:

> "I can use AI to accelerate exploration, generate alternatives, or help investigate an unfamiliar API, but I verify the generated code, understand the logic, test edge cases, and take responsibility for the final implementation."

This matches the engineering philosophy Bruviti has publicly described.

---

# 74. AI Coding Verification

If AI generates code, verify:

- Correctness
- Complexity
- Security
- Edge cases
- Dependencies
- API behavior
- Error handling
- Test cases

Never blindly trust generated code.

---

# 75. Questions You Should Ask Yourself About Any Solution

Before finalizing a technical solution:

### Correctness
Does it solve the problem?

### Complexity
Can it handle the expected input size?

### Reliability
What happens when something fails?

### Security
Can unauthorized users access it?

### Scalability
What happens when usage increases 100×?

### Maintainability
Can another developer understand it?

### Observability
Can we detect failures?

### Cost
Is the architecture unnecessarily expensive?

---

# 76. Bruviti Technology Stack — What to Understand Conceptually

You do not need to memorize every vendor/tool.

Understand these layers:

```text
┌──────────────────────────────┐
│ Business Workflow            │
├──────────────────────────────┤
│ Agentic AI / Automation      │
├──────────────────────────────┤
│ Domain Reasoning / Models     │
├──────────────────────────────┤
│ Ontology / Knowledge / RAG    │
├──────────────────────────────┤
│ Data & Integration Layer     │
├──────────────────────────────┤
│ Enterprise Systems            │
├──────────────────────────────┤
│ Infrastructure / Edge / Cloud│
└──────────────────────────────┘
```

The important thing is understanding how the layers interact.

---

# 77. High-Priority Bruviti Questions

If you have very little time, prepare these first:

1. What does Bruviti do?
2. What is AIP?
3. What is aftermarket service?
4. What is Edge AI?
5. Why combine edge and cloud?
6. What is Agentic AI?
7. What is an AI agent?
8. What is RAG?
9. RAG vs fine-tuning?
10. What is an ontology?
11. Why use an ontology?
12. What is a knowledge graph?
13. What is an embedding?
14. What is vector search?
15. Why use domain-specific models?
16. Why use small language models?
17. How can AI integrate with ERP/CRM/FSM?
18. What is API-first architecture?
19. What is bidirectional integration?
20. What is an air-gapped environment?
21. What is data sovereignty?
22. How do you protect enterprise AI data?
23. What are AI guardrails?
24. What is hallucination?
25. How can hallucination be reduced?
26. What is model drift?
27. What is MLOps?
28. How do you monitor a production AI system?
29. How would you design an equipment fault-detection system?
30. What happens if the network goes down?
31. What happens if an API fails?
32. What happens if the AI model is wrong?
33. How would you scale the system?
34. How would you make the system fault tolerant?
35. How would you explain your project architecture?

---

# 78. Rapid-Fire Final Revision

### Bruviti
**Q: What is Bruviti?**  
A: An AI company focused on mission-critical aftermarket service operations.

**Q: What is AIP?**  
A: Aftermarket Intelligence Platform.

**Q: What is aftermarket service?**  
A: Service, maintenance, repair, parts, warranty, and support after equipment is sold.

**Q: What is agentic AI?**  
A: AI capable of reasoning and executing multi-step actions toward a goal.

**Q: What is RAG?**  
A: Retrieval-Augmented Generation.

**Q: What is an ontology?**  
A: Structured representation of concepts and relationships in a domain.

**Q: What is an embedding?**  
A: Numerical representation of data used for similarity-based operations.

**Q: What is vector search?**  
A: Searching for semantically similar vectors.

**Q: What is data sovereignty?**  
A: Keeping data under required organizational/legal/infrastructure control.

**Q: What is an air-gapped environment?**  
A: An isolated environment without normal external network connectivity.

**Q: What is model drift?**  
A: Model performance degradation caused by changes in real-world data/relationships.

**Q: What is MLOps?**  
A: Practices for managing the ML lifecycle from development to production monitoring.

**Q: What is a guardrail?**  
A: A control that constrains or validates AI behavior.

**Q: What is hallucination?**  
A: AI output that is incorrect or unsupported but appears plausible.

---

# 79. Final Preparation Priority

Your three preparation files should now be studied in this order:

## File 1 — AIML / Edge / IoT

Study:

**AI → ML → Deep Learning → IoT → Edge → Cloud → Edge AI → Model deployment**

## File 2 — Coding / DSA

Study:

**Python → Arrays → Strings → Hashing → Two Pointers → Sliding Window → Binary Search → Stack → Linked List → BFS/DFS → Complexity**

## File 3 — Bruviti-Specific

Study:

**Bruviti → AIP → Aftermarket Service → Agentic AI → RAG → Ontology → Enterprise Integration → Edge/Offline → Security → Evaluation → System Design → Project Discussion**

---

# 80. Final Mental Model

If you remember only one architecture for the company, remember this:

```text
             REAL-WORLD EQUIPMENT
                     │
                     ▼
             Sensors / Systems
                     │
                     ▼
              Data Integration
                     │
                     ▼
        ┌────────────────────────┐
        │ Domain Knowledge       │
        │ Ontology / RAG         │
        └───────────┬────────────┘
                    │
                    ▼
          Specialized AI Models
                    │
                    ▼
             Agentic Reasoning
                    │
                    ▼
            Business Decision
                    │
                    ▼
       ┌────────────────────────┐
       │ Enterprise Systems     │
       │ ERP / CRM / FSM / etc. │
       └───────────┬────────────┘
                   │
                   ▼
               ACTION
                   │
                   ▼
          Monitoring / Evaluation
                   │
                   ▼
          Continuous Improvement
```

And at the infrastructure level:

```text
             CLOUD / PRIVATE CLOUD
                     ↕
              EDGE / ON-PREMISE
                     ↕
              DEVICES / SYSTEMS
```

The central idea is:

**Bruviti is not simply building a chatbot or an ML prediction model. It is building AI-driven systems that understand domain data, reason about service problems, integrate with enterprise software, and execute real operational workflows.**

---

# Sources Used for Company-Specific Research

The company-specific sections above are based primarily on Bruviti's current public materials:

- Bruviti official website and company/about information
- Bruviti Aftermarket Intelligence Platform information
- Bruviti technical documentation
- Bruviti system-integration documentation
- Bruviti data-sovereignty/security documentation
- Bruviti industry-solution information
- Bruviti public LinkedIn engineering/interview discussion

The most important current source for interview preparation is Bruviti's public discussion of its technical interview approach: the company describes realistic, open-ended problems, tool/AI use, ambiguity, trade-off analysis, and verification as part of what it wants to evaluate.

---

# Final Reminder

Do not try to memorize this entire file.

Understand the relationships:

**Equipment → Data → Knowledge → AI → Reasoning → Workflow → Enterprise Action → Monitoring**

That is the technical picture that connects Bruviti's AI, edge, enterprise integration, and service-automation work.
