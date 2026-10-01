# RealCheck-AI-Based-Video-Verification

An AI-powered research assistant for asking questions about SEC filings and receiving grounded answers with source citations.

## Overview

**Document Copilot** is a full-stack Generative AI application designed to help financial research analysts work with large collections of SEC filings.

Instead of manually searching through hundreds of pages of financial documents, users can ask questions in natural language and receive answers based on relevant information retrieved from the underlying documents.

The application follows a **Retrieval-Augmented Generation (RAG)** approach. Relevant document passages are retrieved first, and the LLM then generates an answer using those passages as context.

The main focus of the project is **grounded and verifiable AI responses**, where generated answers are supported by relevant source citations.

---

## Problem Statement

Financial analysts often spend significant time reading SEC filings such as 10-K and 10-Q reports to find specific information.

For example, an analyst may want to find:

- Revenue trends
- Business segment performance
- Risk factors
- AI and cloud investments
- Capital expenditure
- Geographic revenue exposure
- Supplier concentration
- Changes in management discussion and analysis

Finding this information manually across large documents can be repetitive and time-consuming.

Document Copilot aims to simplify this process by providing a conversational interface over a collection of SEC filings.

---

## Key Features

### Natural Language Search

Users can ask questions about SEC filings using normal conversational language.

Example:

> How did the company's revenue mix change over the last five years?

### Retrieval-Augmented Generation

The application uses a RAG pipeline to retrieve relevant information before generating an answer.

```text
User Question
      ↓
Query Processing
      ↓
Document Retrieval
      ↓
Relevant Document Chunks
      ↓
Context Construction
      ↓
LLM
      ↓
Answer + Citations
```

### Hybrid Search

The retrieval layer combines:

- Semantic search using embeddings
- PostgreSQL full-text search
- Reciprocal Rank Fusion (RRF)

This allows the system to consider both semantic similarity and exact keyword matches.

### Source Citations

Generated answers are associated with the document passages used as evidence.

This allows users to verify the information instead of relying blindly on the generated response.

### Authentication

The application uses Supabase Auth for user authentication.

### Chat History

The architecture supports persistent chat threads and messages so users can maintain their previous research conversations.

### Streaming Responses

The backend supports streaming generated responses to the frontend so users can start seeing the response before the complete generation process finishes.

---

## System Architecture

```text
                         ┌──────────────────┐
                         │      User        │
                         └────────┬─────────┘
                                  │
                                  ▼
                    ┌─────────────────────────┐
                    │ React + TypeScript      │
                    │       Frontend          │
                    └────────────┬────────────┘
                                 │
                                 │ API Request + JWT
                                 ▼
                    ┌─────────────────────────┐
                    │        FastAPI          │
                    │        Backend          │
                    └────────────┬────────────┘
                                 │
               ┌─────────────────┼─────────────────┐
               │                 │                
