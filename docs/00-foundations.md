# marginalia — foundations

## Problem
Searching a document when not knowing the exact word looking for is troublesome. Marginalia solves this by providing a mechanism for searching by similarity. A user does not have to know the exact word and can find context similar to his query. 

## Goals
- Users are allowed to add their own documents
- Users can search by relevance
- Users can retrieve previous interactions with the system
- Max of 3 documents per batch

## Non-goals
- No data replication for recovery
- No support for docx, xlsx, html or other file formats
- No caching layer. Every question hits the endpoint and vector store fresh.
- Single tenant in production, but the data model is per-user scoped to allow future multi-tenancy without migration.

## Non-functional requirements
- Latency: p95 question-to-answer end-to-end under 20 seconds
- Scale: support up to 10 documents, 100 questions per day
- Cost: under $5 per month at idle
- Availability: best-effort, single region, no formal SLA
- Security: JWT bearer, secrets via env vars, single tenant, no PII in the corpus
- Operability: one-command local startup via docker-compose
