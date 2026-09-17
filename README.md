# PAKGOV-RAG

**Bilingual Urdu-English Retrieval-Augmented Generation for Pakistani Government and Legal Documents**

[![Status](https://img.shields.io/badge/status-early--stage-orange)](https://github.com/salikhussain71-code/PAKGOV-RAG-project)
[![Language](https://img.shields.io/badge/language-Python-blue)](https://www.python.org/)
[![License](https://img.shields.io/badge/license-MIT-green)](LICENSE)

> A research-oriented project investigating bilingual Urdu-English retrieval-augmented generation (RAG) for Pakistani government and legal documents, with a focus on document processing, Urdu text normalization, information retrieval, grounded generation, citation support, and systematic evaluation.

---

## Table of Contents

* [Overview](#overview)
* [Motivation](#motivation)
* [Research Question](#research-question)
* [Research Objectives](#research-objectives)
* [Scope](#scope)
* [Current Status](#current-status)
* [Planned Research Pipeline](#planned-research-pipeline)
* [Planned System Architecture](#planned-system-architecture)
* [Document Sources](#document-sources)
* [Data and Dataset Design](#data-and-dataset-design)
* [Retrieval Strategy](#retrieval-strategy)
* [Generation Strategy](#generation-strategy)
* [Evaluation Plan](#evaluation-plan)
* [Error Analysis](#error-analysis)
* [Reproducibility](#reproducibility)
* [Repository Structure](#repository-structure)
* [Technology Stack](#technology-stack)
* [Research Roadmap](#research-roadmap)
* [Limitations](#limitations)
* [Responsible Use](#responsible-use)
* [Contributing](#contributing)
* [License](#license)
* [Author](#author)

---

## Overview

PAKGOV-RAG is a research project focused on building and evaluating a bilingual Urdu-English Retrieval-Augmented Generation system for Pakistani government and legal documents.

The project explores how retrieval-based AI systems can help users find and understand information contained in official documents while maintaining a connection between generated answers and their underlying source passages.

The initial domain includes documents associated with Pakistani public institutions and government/legal information, including sources such as:

* Federal Board of Revenue (FBR)
* Higher Education Commission (HEC)
* National Database and Registration Authority (NADRA)
* Securities and Exchange Commission of Pakistan (SECP)
* Supreme Court of Pakistan

The project is designed as a **research and engineering study**, rather than simply a chatbot implementation.

---

## Motivation

A large amount of important public information is distributed across government notices, regulations, policies, forms, reports, legal documents, and other official publications.

Many information-retrieval and question-answering systems are primarily evaluated on English-language data.

PAKGOV-RAG focuses on the problem of retrieving and grounding information when users interact with Pakistani government and legal documents in either:

* English
* Urdu
* Urdu-English mixed queries

The project therefore investigates the complete pipeline:

```text
Official Documents
        ↓
Document Processing
        ↓
OCR / Text Extraction
        ↓
Urdu Text Normalization
        ↓
Chunking
        ↓
Information Retrieval
        ↓
Reranking
        ↓
Grounded Generation
        ↓
Source Attribution
        ↓
Evaluation
```

---

## Research Question

The central research question is:

> **How effectively can a bilingual Urdu-English retrieval and generation pipeline retrieve and answer questions over Pakistani government and legal documents while maintaining accurate grounding in the underlying source material?**

The project will investigate this question through controlled experiments rather than relying only on qualitative demonstrations.

---

## Research Objectives

The project aims to:

1. Build a reproducible document-ingestion pipeline for government and legal documents.
2. Investigate OCR and text-processing challenges for Urdu and mixed-language documents.
3. Develop an Urdu-aware text normalization pipeline.
4. Establish a traditional lexical retrieval baseline.
5. Establish a dense-retrieval baseline.
6. Compare lexical, dense, and hybrid retrieval approaches.
7. Investigate reranking for retrieved passages.
8. Develop a grounded generation pipeline.
9. Preserve source information throughout the retrieval and generation process.
10. Evaluate retrieval and answer quality using measurable criteria.
11. Analyze common system failure modes.
12. Document limitations and reproducibility requirements.

---

## Scope

### In Scope

The initial scope includes:

* Pakistani government documents
* Pakistani legal/public documents
* Urdu-language text
* English-language text
* Urdu-English queries
* OCR and document processing
* Information retrieval
* Dense retrieval
* Hybrid retrieval
* Reranking
* Retrieval-Augmented Generation
* Source attribution
* Retrieval evaluation
* Generation evaluation
* Human evaluation
* Error analysis

### Out of Scope

The system is not intended to:

* replace lawyers or legal professionals
* provide guaranteed legal advice
* make official government decisions
* determine legal outcomes
* replace official government services
* provide unsupported answers when evidence is unavailable

---

## Current Status

**Status: Early Stage — Research Design, Literature Review, Data Collection, and Pipeline Planning**

Current work is focused on:

* defining the research scope
* reviewing relevant literature
* identifying authoritative document sources
* designing the dataset structure
* planning the document-ingestion pipeline
* defining retrieval and generation experiments
* designing an evaluation methodology

No performance claims are made at this stage.

Experimental results will only be reported after the corresponding experiments have been implemented and evaluated.

---

## Planned Research Pipeline

### Phase 1 — Document Collection

Identify relevant documents from authoritative sources.

For each document, the project will aim to maintain metadata such as:

```text
document_id
organization
title
document_type
publication_date
source_url
language
collection_date
processing_status
```

The project will distinguish between:

* original source documents
* extracted text
* processed text
* generated indexes
* evaluation data

---

### Phase 2 — OCR and Text Extraction

Government and legal documents may exist in different formats, including digitally generated and scanned documents.

The pipeline will investigate:

```text
PDF / Document
      ↓
Text Extraction
      ↓
OCR when required
      ↓
Raw Text
```

OCR output will be treated as potentially noisy and will therefore be evaluated and cleaned before retrieval.

---

### Phase 3 — Urdu Text Normalization

The project will investigate preprocessing required for Urdu and related Arabic-script text.

Potential processing steps include:

* Unicode normalization
* character normalization
* whitespace normalization
* punctuation handling
* unwanted-character removal
* consistent representation of relevant Urdu characters
* preservation of meaningful linguistic information

The exact preprocessing pipeline will be determined experimentally.

---

### Phase 4 — Document Chunking

Processed documents will be divided into retrieval units.

The project will investigate how chunking decisions affect retrieval quality.

Potential variables include:

* chunk size
* overlap
* document structure
* paragraph boundaries
* section boundaries
* metadata preservation

Each chunk should retain enough metadata to trace it back to its source document.

---

### Phase 5 — Retrieval

The project will establish multiple retrieval baselines.

#### Lexical Retrieval

A BM25-based baseline will provide a traditional information-retrieval reference point.

#### Dense Retrieval

Dense vector representations will be investigated for semantic retrieval across multilingual queries and documents.

#### Hybrid Retrieval

Lexical and dense retrieval approaches will be combined and evaluated against the individual baselines.

---

### Phase 6 — Reranking

A reranking stage may be introduced after initial retrieval.

The planned comparison is:

```text
Query
  ↓
Initial Retrieval
  ↓
Top-k Candidates
  ↓
Reranker
  ↓
Top Relevant Passages
```

The effect of reranking will be measured rather than assumed to improve performance.

---

### Phase 7 — Grounded Generation

Retrieved passages will be provided to a generation model to produce an answer grounded in retrieved evidence.

The intended architecture is:

```text
User Query
    ↓
Retriever
    ↓
Relevant Passages
    ↓
Reranker
    ↓
Evidence
    ↓
Generation Model
    ↓
Answer + Sources
```

The system should avoid presenting unsupported information as though it came from the retrieved documents.

---

### Phase 8 — Evaluation

The project will evaluate the system at multiple levels.

#### Retrieval Evaluation

Potential metrics include:

* Recall@k
* Precision@k
* Mean Reciprocal Rank (MRR)
* nDCG

The final evaluation metrics will depend on the design of the evaluation dataset.

#### Generation Evaluation

The project will investigate measures related to:

* faithfulness
* answer relevance
* context relevance
* citation/source correctness

Automated evaluation will be supplemented where appropriate by human evaluation.

---

## Planned System Architecture

The planned high-level architecture is:

```text
                    ┌─────────────────────┐
                    │  Official Sources   │
                    └──────────┬──────────┘
                               │
                               ▼
                    ┌─────────────────────┐
                    │ Document Ingestion  │
                    └──────────┬──────────┘
                               │
                               ▼
                    ┌─────────────────────┐
                    │ OCR / Text Extract  │
                    └──────────┬──────────┘
                               │
                               ▼
                    ┌─────────────────────┐
                    │ Text Normalization  │
                    └──────────┬──────────┘
                               │
                               ▼
                    ┌─────────────────────┐
                    │ Chunking + Metadata │
                    └──────────┬──────────┘
                               │
                ┌──────────────┴──────────────┐
                ▼                             ▼
       ┌────────────────┐             ┌────────────────┐
       │ Lexical Search │             │ Dense Retrieval│
       │     BM25       │             │   Embeddings   │
       └───────┬────────┘             └───────┬────────┘
               │                              │
               └──────────────┬───────────────┘
                              ▼
                    ┌─────────────────────┐
                    │ Hybrid Retrieval    │
                    └──────────┬──────────┘
                               │
                               ▼
                    ┌─────────────────────┐
                    │     Reranking       │
                    └──────────┬──────────┘
                               │
                               ▼
                    ┌─────────────────────┐
                    │ Grounded Generation │
                    └──────────┬──────────┘
                               │
                               ▼
                    ┌─────────────────────┐
                    │ Answer + Sources    │
                    └─────────────────────┘
```

---

## Document Sources

The project intends to prioritize authoritative sources.

Potential source organizations include:

* Federal Board of Revenue (FBR)
* Higher Education Commission (HEC)
* National Database and Registration Authority (NADRA)
* Securities and Exchange Commission of Pakistan (SECP)
* Supreme Court of Pakistan

Documents will be collected and used according to the applicable source terms, permissions, and legal/licensing conditions.

Source URLs and relevant metadata will be recorded whenever appropriate.

---

## Data and Dataset Design

The project will maintain structured metadata for documents and retrieval units.

A document record may include:

```text
document_id
organization
title
document_type
publication_date
source_url
language
collection_date
page_number
section
processing_status
```

The project will distinguish between:

```text
Raw Documents
      ↓
Extracted / OCR Text
      ↓
Cleaned Text
      ↓
Chunks
      ↓
Indexes
      ↓
Evaluation Dataset
```

Large source collections and generated indexes will not automatically be committed to the Git repository.

Instead, the repository will document how authorized data can be obtained and processed.

---

## Retrieval Strategy

The retrieval experiments will progressively compare:

```text
BM25
  ↓
Dense Retrieval
  ↓
Hybrid Retrieval
  ↓
Hybrid + Reranking
```

The purpose of this structure is to establish measurable baselines before adding additional system components.

This allows the project to determine which components actually contribute to retrieval performance.

---

## Generation Strategy

The generation stage will consume retrieved evidence rather than relying solely on the model's internal knowledge.

The planned design is:

```text
Question
   ↓
Retrieve evidence
   ↓
Rank evidence
   ↓
Provide evidence to generator
   ↓
Generate answer
   ↓
Return source references
```

Candidate generation approaches may include multilingual or instruction-tuned models appropriate for the project's computational and research constraints.

The final model choice will be documented based on experimental requirements rather than assumed in advance.

---

## Evaluation Plan

The evaluation will be designed before final performance claims are made.

The project will investigate three major dimensions:

### 1. Retrieval Quality

Questions include:

* Did the system retrieve the relevant document?
* Did it retrieve the relevant passage?
* How does hybrid retrieval compare with individual baselines?
* Does reranking improve the ranking of relevant evidence?

### 2. Answer Quality

Questions include:

* Is the answer supported by retrieved evidence?
* Does the answer address the user's question?
* Does the answer introduce unsupported information?
* Are source references correct?

### 3. Human Evaluation

Where appropriate, human evaluation may assess:

* relevance
* factual support
* completeness
* clarity
* citation correctness

The evaluation methodology and criteria will be documented before reporting results.

---

## Error Analysis

A major component of the project will be systematic failure analysis.

Potential failure categories include:

```text
Document ingestion failure
        ↓
OCR error
        ↓
Text normalization error
        ↓
Chunking error
        ↓
Retrieval failure
        ↓
Reranking failure
        ↓
Generation error
        ↓
Citation/source error
```

The project will use these categories to identify weaknesses in the overall pipeline.

---

## Reproducibility

The project aims to make experiments reproducible wherever possible.

Reproducibility documentation will include:

* environment configuration
* dependency versions
* preprocessing procedures
* dataset metadata
* retrieval configuration
* model configuration
* experiment configuration
* evaluation methodology
* random seeds where applicable
* generated results

The repository will separate source code from generated artifacts and large datasets.

---

## Repository Structure

The repository is being developed progressively.

The planned structure is:

```text
PAKGOV-RAG-project/
│
├── data/
│   ├── raw/
│   ├── interim/
│   └── processed/
│
├── docs/
│   ├── literature-review.md
│   ├── dataset-card.md
│   ├── methodology.md
│   ├── evaluation.md
│   └── limitations.md
│
├── ingestion/
│   ├── download/
│   ├── ocr/
│   ├── cleaning/
│   └── chunking/
│
├── retrieval/
│   ├── bm25/
│   ├── dense/
│   ├── hybrid/
│   └── reranking/
│
├── generation/
│   ├── models/
│   ├── prompting/
│   └── citation/
│
├── evaluation/
│   ├── retrieval/
│   ├── generation/
│   └── human/
│
├── experiments/
│   ├── configs/
│   ├── results/
│   └── notebooks/
│
├── app/
│   ├── api/
│   └── demo/
│
├── scripts/
├── tests/
│
├── .github/
│   └── workflows/
│
├── .gitignore
├── LICENSE
├── README.md
├── CONTRIBUTING.md
├── SECURITY.md
├── CITATION.cff
├── pyproject.toml
└── requirements.txt
```

> The repository structure will evolve as the research progresses. Directories will be added when they contain actual project functionality or documentation.

---

## Technology Stack

The planned technology stack includes:

* **Python** — primary programming language
* **PyTorch** — machine learning framework
* **Hugging Face Transformers** — transformer-based NLP models
* **FAISS** — vector similarity search
* **LangChain** — selected RAG/application components where appropriate
* **Tesseract OCR** — OCR experimentation
* **FastAPI** — planned API layer
* **Gradio** — planned research/demo interface
* **Docker** — planned reproducible deployment environment
* **RAG evaluation tools** — evaluation experiments

Technology choices may change during experimentation.

The project will prioritize transparent baselines and reproducible experiments over unnecessary framework complexity.

---

## Research Roadmap

### Phase 1 — Research Design

* [x] Define initial project scope
* [x] Define initial research direction
* [ ] Finalize research questions
* [ ] Complete literature review
* [ ] Define evaluation methodology

### Phase 2 — Data

* [ ] Identify authoritative sources
* [ ] Define dataset schema
* [ ] Collect permitted documents
* [ ] Implement document ingestion
* [ ] Implement OCR pipeline
* [ ] Implement Urdu text normalization
* [ ] Implement document chunking

### Phase 3 — Retrieval

* [ ] Implement BM25 baseline
* [ ] Implement dense retrieval
* [ ] Implement hybrid retrieval
* [ ] Implement reranking
* [ ] Build retrieval evaluation dataset
* [ ] Run retrieval experiments

### Phase 4 — Generation

* [ ] Select generation approach
* [ ] Implement grounded generation
* [ ] Implement source attribution
* [ ] Evaluate generated answers

### Phase 5 — Evaluation

* [ ] Retrieval evaluation
* [ ] Generation evaluation
* [ ] Citation evaluation
* [ ] Human evaluation
* [ ] Error analysis
* [ ] Ablation experiments

### Phase 6 — Application

* [ ] Build API
* [ ] Build research/demo interface
* [ ] Add reproducible deployment
* [ ] Document usage

### Phase 7 — Research Output

* [ ] Consolidate experimental results
* [ ] Document limitations
* [ ] Prepare research report
* [ ] Prepare paper manuscript
* [ ] Release reproducibility materials where permitted

---

## Limitations

This project is an experimental research system.

Potential limitations include:

* OCR errors
* incomplete document coverage
* inconsistent document formatting
* Urdu linguistic variation
* Urdu-English code-switching
* retrieval failures
* incorrect ranking
* incomplete answers
* unsupported generated claims
* incorrect source attribution
* model limitations
* dataset limitations
* changes to government documents over time

Performance should therefore be interpreted within the documented evaluation setting.

---

## Responsible Use

PAKGOV-RAG is intended for research and information-retrieval experimentation.

It should not be treated as an authoritative replacement for:

* official government services
* official government publications
* legal professionals
* qualified experts
* formal legal advice

Users should verify important information against the original authoritative source.

The system may produce incorrect or incomplete answers, particularly when source documents are ambiguous, unavailable, poorly scanned, or incorrectly processed.

---

## Contributing

The project is currently under active research development.

Future contribution guidelines will cover:

* issue reporting
* feature proposals
* research discussions
* development setup
* coding standards
* testing
* pull requests
* documentation

Before contributing data or documents, contributors should verify that they have the appropriate rights and permissions to redistribute them.

---

## License

The project source code is released under the **MIT License**.

See [LICENSE](LICENSE) for the full license text.

The MIT License applies to the project's code and does not automatically grant rights to third-party documents, datasets, government publications, or other external materials used during research.

---

## Author

**Salik Hussain**

AI/ML Research Aspirant focused on:

* Natural Language Processing
* Urdu NLP
* Low-Resource NLP
* Information Retrieval
* Retrieval-Augmented Generation
* Multilingual AI

GitHub: [@salikhussain71-code](https://github.com/salikhussain71-code)

---

## Project Status

**PAKGOV-RAG is an ongoing research project.**

The repository will be updated as the system progresses from research design and data preparation toward implementation, controlled experiments, evaluation, and reproducible research results.

No performance claims are made until they are supported by documented experiments.
