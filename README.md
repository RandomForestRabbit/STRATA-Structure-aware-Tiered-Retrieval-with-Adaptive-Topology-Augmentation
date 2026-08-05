# STRATA
### Structure-aware Tiered Retrieval with Adaptive Topology-Augmentation

STRATA is a retrieval-augmented generation (RAG) system for PDF question answering
that goes beyond fixed-size chunking and flat vector search. It combines two ideas:

1. **Hybrid Boundary-Aware Chunking** — chunk boundaries are determined by a
   combined signal of semantic drift (embedding similarity between adjacent
   segments), entity/topic continuity (noun-phrase overlap), and document
   structure (headings, table rows, list items) — instead of splitting on a
   fixed token count.

2. **Graph-Augmented Retrieval** — chunks are linked into a lightweight
   entity-relation graph (LightRAG-style dual-level indexing: fine-grained
   entity links + high-level topic clusters), enabling multi-hop retrieval
   that plain vector similarity search misses — e.g., pulling in a chunk that
   shares an entity with the query but doesn't read as topically similar on
   its own.

STRATA is evaluated across four structurally distinct PDF types — tabular
documents, image-heavy documents, long-form prose, and short instructional
text — to measure where structure-aware chunking and graph augmentation
actually help, and where they don't.

## Why

Standard RAG pipelines chunk documents by token count and retrieve purely by
embedding similarity. This breaks down in predictable ways: chunking mid-table-row
severs an answer from its context, and vector search alone can miss relevant
facts that are lexically distant from the query even when they're directly
connected via a shared entity. STRATA targets both failure modes directly and
measures the improvement — and the limits — on a per-document-type basis.

## Pipeline
