# TaxDoc Copilot - Multi-Agent RAG + Streaming Data Platform

Overview
TaxDoc Copilot is an enterprise-grade GenAI data product that demonstrates how large organizations can transform document-heavy tax workflowds using **Retrieval-Augmented Geneartion (RAG), multi-agent orchestration, and scalable data engineering.**

The platform ingests unstructures tax documents and structured dataseta, processes them via batch and streaming pipelines, and serves **auditable, governed, low-latency GenAI answers** backed by vector search, SQL, and MongoDB aggregations.

This project is intentionally designed to mirror production responsibilities of an **AI Data Engineer / Manager** working on GenAI-enabled data platforms.

## Key Capabilities
- End-to-end **RAG system** with citations, confidence checks, and evaluation metrics.
- **Multi-agent orchestration** (planner/worker/verifier) with retires and fallbacks
- **Vector database ownership** (Milvus / Zillz Cloud): schema, indexing, tuning
- **Streaming + batch data pipelines** using Kafka and Spark
- **Governed SQL generation** with guardrails and observability
- **MongoDB-based GenAI data services** with aggregation pipelines and change streams
- Enterprise-grade **observability, evaluation, and runbooks**

## High-Level Architecture
**Sources**
-> Document Ingest API(PDF / HTML / DOCX)
-> Azure Blob Storage (raw artifacts)

**Streaming & Processing**
-> Kafka topics (document_ingest, metadata_updates)
-> Spark (batch + Structured Streaming)

**Serving Layers**
- Vector StoreL: Milvus / Zillz Cloud (embeddings + metadata)
- Operational Store: MongoDB (document metadata, extracted fields)
- Relational Store: Postgres / Azure SQL (structured tax tables)

**GenAI Layer**
-> Planner Agent -> Retrieval / SQL / MongoDB Tools -> Verifier Agent
-> Answer with citations, tool traces, and confidence signals

## Tech Stack
**Languages & Frameworks**
- Python, FastAPI, Pydantic
- LangGraph (multi-agent orchestration)

**Data & Streaming**
- Apache Kafka
- Apache Spark (batch + Structured Streaming)

**Storage**
- Azure Blob Storage (raw documents)
- Milvus / Zillz Cloud (vector database)
- MongoDB (semi-structures GenAI workloads)
- Postgres / Azure SQL (structured data)

**Observability & Quality**
- OpenTelemetry (tracing)
- Prometheus / Grafana (metrics & dashboards)
- Custom evaluation harness (Recall@k, latency, faithfulness)

**Infrastructure**
- Docker & Docker Compose
- Github Actions (CI/CD skeleton)

## Multi-Agent Design
**1. Planner Agent**
- Interprets user intent
- Decides execution path:
  - Retrieval-only (vector search)
  - Retrieval + SQL
  - Retrieval + Mongo aggregation
  - Hybrod strategy

**2. Retrieval Agent**
- Hybrid search (vector + keyword)
- Metadata filtering (jurisdiction, year, document type)
- Reranking and recall optimization

**3. SQL Agent (Guardrailed)**
- Generates SQL using schema allowlists
- Validates queries (parser, dry-run, row limits)
- Logs cost, latency, and scanned rows

**4. Verifier Agent**
-  Ensures citation coverage
-  Flags conflicting sources
-  Rejects uncited claims
-  Applies confidence thresholds

## Vector Database Design (Milvus / Zillz)
**Collection Schema**
- id (primary key)
- embedding (float vector)
- document_id
- chunk_id
- jurisdiction
- tax_year
- document_type
- source_uri

**Indexing Stragtegies**
- HNSW for low-latency retrieval
- IVF_FLAT for high-recall batch queries
- Partitioning by tax_year / client_id

**Peformance Metrics**
- Recall@k
- p50 / p95 latency
- Query throughput

## MongoDB Design
- Document metadata and extracted entities
- Aggregation pipelines for case summaries
- Change streams trigger re-embedding on updates
- Indexing for query patterns used by agents

## Data Pipelines
**Batch Pipelines**
- Historical document backfill
- Bulk embedding and index creation

**Streaming Pipelines**
- Real-time document ingestion
- Metadata updates via Kafka
- Spark jobs maintain consistency across MongoDB and Milvus

## Evaluation & Quality
- Golden question-answer dataset
- Retrieval metrics: Recall@k, nDCG
- Answer faithfulness: citation overlap checks
- Operational metrics: latency SLOs, error rates

## Observability
- End-to-end tracing across agent tool calls
- Metrics:
    - Vector DB latency
    - Retrieval hit rate
    - SQL failures
    - Kafka consumer lag
- Debug-friendly logs with correlation IDs

## Repositiory Structure
<img width="232" height="329" alt="image" src="https://github.com/user-attachments/assets/be29c6d0-d3b7-4d0e-900c-40adee783c34" />

## Runbooks (Sample)
- Vector DB latency degradation
- Kafka consumer lag
- SQL generation failures
- Embedding pipeline backlogs

## Why This Project Matters
TaxDoc Copilot demonstrates **real-world GenAI data engineering leadership:**
- Production-grade RAG
- Vector database ownership
- Streaming + batch data platforms
- Governance, safety, and observability

It is intentionally scoped and arcgitectured to reflect **enterprise GenAI transformation work** rather than a toy LLM demo.


