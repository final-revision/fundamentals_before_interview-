# Bruviti AI Placement Final Preparation Notes

## Company Understanding + System Design + Projects + Interview Discussion Topics

This is the final preparation file covering important topics remaining
after: 1. AI/ML Technical Preparation 2. Coding and DSA Preparation

Focus areas: - Bruviti company understanding - Enterprise AI concepts -
Software architecture - Project discussion - Engineering thinking
questions

------------------------------------------------------------------------

# 1. About Bruviti AI

## What does Bruviti do?

Bruviti focuses on enterprise AI solutions that improve service
operations.

The company works on:

-   AI-powered service automation
-   Intelligent workflows
-   AI agents
-   Knowledge management
-   Enterprise decision support

The goal is to help organizations solve complex service problems faster
using AI.

------------------------------------------------------------------------

# 2. Why Enterprise AI is Different From Normal AI Apps?

## Question:

Why is enterprise AI more difficult?

## Answer:

Enterprise systems require:

-   Large amount of company data
-   Security
-   Reliability
-   Integration with existing software
-   Accurate answers
-   Auditability

Example:

A normal chatbot answers questions.

An enterprise AI system may need to:

-   Understand a machine problem
-   Check service history
-   Recommend action
-   Update business systems

------------------------------------------------------------------------

# 3. AI System Architecture

## Question:

Explain architecture of an AI-powered application.

## Answer:

Basic architecture:

User \| Application Interface \| Backend API \| AI Processing Layer \|
LLM / ML Models \| Knowledge Database \| Response

Advanced enterprise architecture:

User Request

↓

API Gateway

↓

AI Agent Layer

↓

Tools / External APIs

↓

Database + Vector Database

↓

Response Generation

------------------------------------------------------------------------

# 4. API and Backend Concepts

## Question:

What is REST API?

## Answer:

REST API allows different applications to communicate using HTTP
methods.

Common methods:

GET: Retrieve data

POST: Create data

PUT: Update data

DELETE: Remove data

Example:

Complaint System:

POST /complaints

Creates a new complaint.

------------------------------------------------------------------------

# 5. Database Design Questions

## Question:

How would you design a complaint/service system database?

## Answer:

Possible tables:

User

-   user_id
-   name
-   email

Complaint

-   complaint_id
-   user_id
-   category
-   description
-   status

Admin

-   admin_id
-   area

Action

-   action_id
-   complaint_id
-   resolution

Relationship:

User \| creates \| Complaint \| handled by \| Admin

------------------------------------------------------------------------

# 6. SQL Knowledge

## Question:

Difference between SQL and NoSQL?

## Answer:

SQL:

-   Structured tables
-   Fixed schema
-   Good for transactions

Examples: MySQL, PostgreSQL

NoSQL:

-   Flexible structure
-   Good for large-scale unstructured data

Examples: MongoDB

------------------------------------------------------------------------

# 7. Cloud and Deployment Basics

## Question:

Why do companies use cloud platforms?

## Answer:

Benefits:

-   Scalability
-   Reliability
-   Global access
-   Easier deployment

Common cloud services:

-   AWS
-   Azure
-   Google Cloud

------------------------------------------------------------------------

# 8. Security in AI Systems

## Question:

What security problems exist in AI applications?

## Answer:

Important risks:

## Data Privacy

Sensitive company data should be protected.

## Prompt Injection

Users may try to manipulate AI instructions.

## Data Leakage

Private information should not appear in responses.

## Authentication

Only authorized users should access systems.

------------------------------------------------------------------------

# 9. AI Evaluation

## Question:

How do you evaluate an AI system?

## Answer:

Different systems require different metrics.

For classification:

-   Accuracy
-   Precision
-   Recall
-   F1 Score

For Generative AI:

-   Response quality
-   Correctness
-   Hallucination rate
-   User satisfaction

------------------------------------------------------------------------

# 10. Project Explanation Preparation

## How to explain any project?

Follow this structure:

## 1. Problem

What issue are you solving?

## 2. Solution

How does your system solve it?

## 3. Technology

Explain:

-   Frontend
-   Backend
-   Database
-   AI models

## 4. Architecture

Explain data flow.

## 5. Challenges

Mention real problems:

-   Data handling
-   Performance
-   Security
-   Accuracy

## 6. Improvements

Future possibilities.

------------------------------------------------------------------------

# 11. GovResolver Project Connection

If asked about your project:

Explain:

Public User

↓

Upload Complaint + Image

↓

AI Categorization

↓

Database Storage

↓

Area Admin Dashboard

↓

Action and Resolution Tracking

Important points:

-   Real-world problem
-   AI-based classification
-   Workflow automation
-   Government service improvement

This connects with Bruviti because both involve:

-   Problem identification
-   Categorization
-   Workflow automation
-   Action recommendation

------------------------------------------------------------------------

# 12. System Design Questions They May Ask

## Q1. Design an AI chatbot system.

Answer:

Components:

1.  User Interface
2.  Backend API
3.  Authentication
4.  LLM service
5.  Knowledge database
6.  Logging system

------------------------------------------------------------------------

## Q2. How would you make an AI system faster?

Answer:

Methods:

-   Cache frequent responses
-   Optimize database queries
-   Use efficient models
-   Reduce unnecessary API calls
-   Use asynchronous processing

------------------------------------------------------------------------

## Q3. How would you handle millions of users?

Answer:

Use:

-   Load balancing
-   Cloud scaling
-   Database optimization
-   Caching
-   Microservices

------------------------------------------------------------------------

# 13. Engineering Thinking Questions

## Q1. A model gives wrong answers. What will you do?

Answer:

Steps:

1.  Analyze incorrect responses
2.  Check training/retrieval data
3.  Improve prompts
4.  Add validation
5.  Improve evaluation process

------------------------------------------------------------------------

## Q2. Accuracy is high but users are unhappy. Why?

Answer:

Possible reasons:

-   Wrong user expectations
-   Poor user experience
-   Slow response
-   Incorrect real-world usage

Technical accuracy alone is not enough.

------------------------------------------------------------------------

# 14. Important Technologies To Revise

Priority:

## AI

-   LLM
-   RAG
-   AI Agents
-   Embeddings
-   Vector Database

## Backend

-   REST API
-   Database
-   Authentication

## Software Engineering

-   System Design
-   Scalability
-   Security
-   Debugging

## Project

-   Architecture
-   Decisions
-   Challenges

------------------------------------------------------------------------

# 15. Final Interview Preparation Checklist

Before Bruviti visit, revise:

\[ \] Explain Bruviti technology

\[ \] Explain AI Agent

\[ \] Explain RAG

\[ \] Explain your project architecture

\[ \] Explain database design

\[ \] Explain API concepts

\[ \] Explain cloud basics

\[ \] Explain security concerns

\[ \] Explain engineering decisions

\[ \] Practice technical discussion

------------------------------------------------------------------------

# Final Note

Bruviti is likely looking for candidates who can combine:

-   Programming ability
-   AI understanding
-   Problem solving
-   Ability to explain technical decisions

Do not only memorize definitions. Understand how AI systems are built
and used in real products.
