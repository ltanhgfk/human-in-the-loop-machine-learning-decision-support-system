# Vietnamese NLP Decision Support System

> Master's research software artifact implementing a human-in-the-loop machine learning system for Vietnamese agricultural question classification, expert routing, and decision support through SMS/MMS.

## Research Highlights

* Master's research project in **Information Systems**.
* Research and software implementation for **Vietnamese agricultural question classification**.
* Integration of **Vietnamese text processing, feature engineering, and Support Vector Machine (SVM)** classification.
* Human-in-the-loop workflow combining **machine prediction, human verification, and domain-expert decision support**.
* Similarity-based retrieval using **term-frequency representations and cosine similarity**.
* The current cosine-similarity implementation was reconstructed in 2026 from the reported historical design; the original implementation source is no longer available.
* Historical model evaluation using **10-fold cross-validation**, with a reported accuracy of **68.35%**.
* End-to-end integration of machine learning into a practical information-system architecture.
* Public research software release with sanitized configuration, documentation, and privacy safeguards.

---

## Overview

This repository preserves the source-level implementation of my Master's research project in Information Systems.

The project investigates how classical machine learning and Vietnamese natural language processing can be integrated into a practical information system for agricultural advisory services.

The system processes Vietnamese agricultural questions received through SMS/MMS-oriented services, classifies questions into agricultural topics using a linear-kernel Support Vector Machine (SVM), supports human verification, routes questions toward appropriate domain experts, retrieves previously answered questions using similarity-based information retrieval, and incorporates human-labelled information into subsequent model retraining.

The central design principle is **human-in-the-loop decision support**.

The machine-learning component assists human coordinators and agricultural experts rather than attempting to replace expert decision-making.

---

## Research Context

The system was developed as a semi-automatic agricultural advisory system for rice-related questions through mobile information services.

The research explored the integration of:

* Vietnamese text processing;
* domain-specific feature engineering;
* classical machine learning;
* information retrieval;
* human verification;
* expert routing; and
* decision-support workflows.

The project therefore represents not only a machine-learning classifier, but an attempt to integrate machine learning into a larger information-system environment.

### Academic Publication

**Lương Thế Anh, Nguyễn Thái Nghe, Nguyễn Chí Ngôn (2014).**

**Xây dựng hệ thống hỗ trợ khuyến nông trên cây lúa qua mạng thông tin di động.**

*Tạp chí Khoa học Trường Đại học Cần Thơ*, 33, 9–21.

---

## Research Problem

Agricultural advisory services may receive questions expressed in natural Vietnamese language and require appropriate routing to domain experts.

The research addressed the problem of integrating automated text classification into this workflow while retaining human verification and expert involvement.

At a high level, the system addresses the following research question:

> How can machine-learning-based Vietnamese text classification be integrated into a practical agricultural information system to support expert-assisted decision making?

The resulting system was designed as a **semi-automatic decision-support workflow**, rather than a fully autonomous advisory system.

---

## System Workflow

```text
                    SMS / MMS
                        │
                        ▼
             Vietnamese Text Processing
                        │
              ┌─────────┴─────────┐
              │                   │
       Word Segmentation     Stop-word Processing
              │                   │
              └─────────┬─────────┘
                        ▼
             Feature Construction
                        │
                        ▼
                Sparse Text Vector
                        │
                        ▼
              Linear-Kernel SVM
                        │
                        ▼
                Topic Classification
                        │
              ┌─────────┴─────────┐
              │                   │
              ▼                   ▼
     Human Verification    Similarity Retrieval
              │                   │
              └─────────┬─────────┘
                        ▼
                  Expert Routing
                        │
                        ▼
                 Expert Response
                        │
                        ▼
             Human-Labelled Information
                        │
                        ▼
                   Retraining
```

This workflow illustrates the distinction between:

**machine prediction → human verification → expert decision support**

rather than:

**machine prediction → autonomous decision**.

---

## System Architecture

The implementation combines several layers of an information system:

```text
┌─────────────────────────────────────────────┐
│              SMS / MMS Interface            │
└──────────────────────┬──────────────────────┘
                       │
                       ▼
┌─────────────────────────────────────────────┐
│        Vietnamese Text Processing            │
│  Segmentation / Stopwords / Feature Build   │
└──────────────────────┬──────────────────────┘
                       │
                       ▼
┌─────────────────────────────────────────────┐
│          Machine Learning Module             │
│          Linear-Kernel SVM Classifier        │
└──────────────────────┬──────────────────────┘
                       │
                       ▼
┌─────────────────────────────────────────────┐
│        Topic Classification / Routing        │
└───────────────┬─────────────────┬───────────┘
                │                 │
                ▼                 ▼
┌──────────────────────┐  ┌──────────────────────┐
│ Human Verification   │  │ Similarity Retrieval │
└──────────┬───────────┘  └──────────┬───────────┘
           │                         │
           └────────────┬────────────┘
                        ▼
              ┌───────────────────┐
              │  Expert Routing   │
              └─────────┬─────────┘
                        ▼
              ┌───────────────────┐
              │ Expert Response   │
              └─────────┬─────────┘
                        ▼
              ┌───────────────────┐
              │ Human-Labelled    │
              │ Information       │
              └─────────┬─────────┘
                        ▼
              ┌───────────────────┐
              │ Model Retraining  │
              └───────────────────┘
```

---

## Vietnamese NLP

The system processes Vietnamese agricultural questions before classification.

The documented processing pipeline includes:

1. Vietnamese word segmentation.
2. Stop-word processing.
3. Keyword and feature construction.
4. Sparse vector representation.

The NLP component is domain-specific and was designed for Vietnamese agricultural questions rather than general-purpose multilingual NLP.

This is particularly relevant to the research context because Vietnamese text processing introduces challenges associated with domain vocabulary, word segmentation, and limited historical resources compared with languages with substantially larger NLP ecosystems.

---

## Feature Engineering

The system uses domain-specific keywords and sparse bag-of-words-style representations to transform Vietnamese questions into machine-learning features.

The feature representation provides the input to the classification component.

The repository should therefore be understood as implementing a classical text-classification pipeline rather than a neural language representation.

---

## Machine Learning Approach

The classification component uses a **Support Vector Machine (SVM)** with a **linear kernel** for multi-class agricultural topic classification.

### Machine Learning Pipeline

| Stage                | Approach                                          |
| -------------------- | ------------------------------------------------- |
| Input                | Vietnamese agricultural questions                 |
| Preprocessing        | Word segmentation and stop-word processing        |
| Feature construction | Domain-specific keywords / sparse text features   |
| Representation       | Sparse vector                                     |
| Classifier           | Linear-kernel SVM                                 |
| Task                 | Multi-class agricultural topic classification     |
| Human involvement    | Verification and expert routing                   |
| Learning cycle       | Human-labelled information can support retraining |

The implementation reflects the machine-learning methods used during the original research period.

---

## Human-in-the-Loop Decision Support

A central characteristic of the system is the involvement of human coordinators and domain experts.

The machine-learning model performs classification, but the overall workflow retains human verification and expert involvement.

This design provides an important distinction between:

* automated classification;
* human verification;
* expert routing; and
* expert response.

The system is therefore better characterized as a **human-in-the-loop decision-support system** than as an autonomous artificial-intelligence system.

---

## Similarity-Based Retrieval

The system also provides retrieval of previously answered questions.

The documented retrieval mechanism uses:

* term-frequency representations; and
* cosine similarity.

This enables previously processed questions and responses to be used as a source of similar information.

Importantly, this mechanism is a **classical information-retrieval approach**.

It is not:

* semantic embedding search;
* transformer-based retrieval;
* Retrieval-Augmented Generation (RAG); or
* LLM-based question answering.

This distinction is intentionally preserved to avoid retroactively applying modern terminology to the original implementation.

---

## Expert Routing

After classification and verification, agricultural questions can be routed toward the appropriate domain expert.

The expert remains responsible for providing and verifying the agricultural response.

This component connects the machine-learning classification layer with the larger information-system workflow.

---

## Model Retraining

Human-labelled information can be incorporated into subsequent learning cycles.

The intended workflow therefore includes:

```text
Question
   ↓
Classification
   ↓
Human Verification
   ↓
Expert Response
   ↓
Human-Labelled Information
   ↓
Retraining
```

This provides a historical example of integrating human feedback into an applied machine-learning workflow.

The repository does not claim that this constitutes modern reinforcement learning or contemporary preference optimization.

---

## Experimental Evaluation

The preserved research record reports:

### 10-Fold Cross-Validation

**Accuracy: 68.35%**

The reported result comes from the original research implementation and evaluation.

The repository preserves this value as historical research evidence.

It should not be interpreted as:

* a modern benchmark;
* a state-of-the-art result;
* a direct comparison with transformer-based systems; or
* evidence of performance on a contemporary dataset.

### Evaluation Summary

| Evaluation Component | Historical Research Record        |
| -------------------- | --------------------------------- |
| Learning method      | Linear-kernel SVM                 |
| Input                | Vietnamese agricultural questions |
| Representation       | Sparse text features              |
| Validation           | 10-fold cross-validation          |
| Reported accuracy    | **68.35%**                        |
| Research domain      | Agricultural advisory services    |

The complete interpretation of the experimental result should be made together with the thesis and the original research publication.

---

## Technology Stack

| Layer                 | Technology                       |
| --------------------- | -------------------------------- |
| Programming language  | Java                             |
| Web application       | JSP / Servlet                    |
| Database              | MySQL                            |
| Machine learning      | Linear-kernel SVM                |
| NLP                   | Vietnamese text processing       |
| Text representation   | Sparse / term-frequency features |
| Information retrieval | Cosine similarity                |
| Communication context | SMS / MMS-oriented services      |

The codebase targets a legacy Java/web environment reflecting the technology used during the original development period.

It does not currently provide a modern Maven/Gradle one-command build.

---

## Repository Structure

```text
RSSAPP/
│
├── Java backend
├── NLP processing
├── classification
└── runtime components

RSSWEB/
│
├── JSP
├── Servlet
└── web application components

config/
│
└── Safe example runtime configuration

database/
│
├── Sanitized database schema
└── Fictional demonstration data

docs/
│
├── ML_PIPELINE.md
├── BUILD.md
├── DATA_PRIVACY.md
├── KNOWN_LIMITATIONS.md
├── DEPENDENCIES.md
└── MY_CONTRIBUTION.md
```

The exact structure may evolve as the repository documentation is improved, but the underlying research source code is preserved rather than rewritten into a modern framework.

---

## Research Contribution

This project demonstrates my experience in integrating machine learning into a practical information-system architecture.

My research and implementation contributions include work across the following areas:

* Vietnamese text processing for agricultural questions.
* Domain-specific feature construction.
* Machine-learning-based question classification.
* Integration of a linear-kernel SVM classifier.
* Human verification within the classification workflow.
* Expert routing for agricultural questions.
* Similarity-based retrieval of previously answered questions.
* Integration of human-labelled information into model retraining.
* Development of an end-to-end information-system workflow connecting machine learning with domain expertise.

The project therefore represents both **machine-learning implementation** and **information-systems research**.

---

## Research Significance

Although the implementation uses classical machine-learning methods, several research themes remain relevant to contemporary intelligent information systems:

* Human-in-the-loop AI.
* Domain-specific natural language processing.
* Low-resource language processing.
* Intelligent decision-support systems.
* Expert-assisted AI.
* Information retrieval.
* Human feedback in machine-learning workflows.
* Integration of AI components into real-world information systems.

The historical implementation provides a concrete research foundation for understanding how machine learning can be embedded within a larger socio-technical information system.

---

## Future Research Directions

The original implementation should not be confused with the following technologies, which were not part of the demonstrated historical system:

* Transformer models.
* Large Language Models (LLMs).
* RAG.
* Neural embeddings.
* Modern deep-learning architectures.

However, the research problem provides several potential directions for future investigation.

### 1. Transformer-Based Vietnamese NLP

A future system could investigate transformer-based Vietnamese language models for question representation and classification.

### 2. LLM-Assisted Expert Decision Support

Large language models could potentially be investigated as an assistance layer while retaining human expert verification.

### 3. Retrieval-Augmented Decision Support

The historical cosine-similarity retrieval component could provide a conceptual starting point for investigating modern semantic retrieval and RAG architectures.

### 4. Explainable AI

Future work could investigate methods for explaining classification decisions to coordinators and domain experts.

### 5. Human Feedback and Continuous Learning

The existing human-verification workflow could motivate research into more systematic approaches for incorporating expert feedback into model improvement.

These are **future research directions**, not capabilities claimed by the original implementation.

---

## Historical Scope

This repository represents an original research and software artifact from the development period of the Master's research.

It preserves the distinction between the original implementation and later technological developments.

The system is therefore **not presented as**:

* a modern deep-learning system;
* a transformer implementation;
* an LLM application;
* an embedding-based retrieval system; or
* a RAG system.

The original system included MMS/image handling. Automatic image classification, however, was identified as future work rather than a demonstrated component of the thesis implementation.

---

## Public Research Release

This repository is intended as a sanitized public research release.

The public version deliberately excludes sensitive or private material, including:

* real or historical user records;
* phone numbers;
* addresses;
* email addresses;
* personal identifiers;
* credentials;
* private SMS/MMS payloads;
* private images;
* historical database dumps or backups;
* private training datasets;
* trained model files;
* compiled binaries;
* dependency JAR files; and
* private runtime configuration.

Only sanitized or fictional demonstration material is intended to remain in the public repository.

See:

* [`docs/DATA_PRIVACY.md`](docs/DATA_PRIVACY.md)
* [`PUBLIC_REPOSITORY_MANIFEST.md`](PUBLIC_REPOSITORY_MANIFEST.md)

for additional information.

---

## Reproducibility

This repository is primarily a **research software artifact and source-level release**.

The public release is intended to make the following aspects inspectable:

* system architecture;
* NLP processing;
* machine-learning workflow;
* information-retrieval mechanism;
* expert-routing workflow; and
* research documentation.

A complete historical deployment may require:

* a compatible legacy Java environment;
* third-party libraries;
* database configuration;
* historical runtime configuration; and
* compatible SMS/MMS gateway infrastructure or services.

The original private training data and trained models are not included in the public repository.

Therefore, this repository should not be interpreted as a one-command reproducible benchmark.

See [`docs/BUILD.md`](docs/BUILD.md) for environment and build information.

---

## Known Limitations

The project has several documented limitations.

1. The system uses classical machine-learning methods rather than contemporary deep-learning architectures.
2. The software relies on a legacy Java/web technology environment.
3. The original private training data is not included in the public release.
4. The original trained model files are not included in the public release.
5. The reported evaluation reflects the historical research dataset and experimental environment.
6. The public repository does not reproduce the complete historical production environment.
7. Similarity retrieval is based on term-frequency representations and cosine similarity rather than modern semantic embeddings.
8. The system should not be interpreted as an autonomous agricultural advisory system.
9. Future research would be required to evaluate modern neural, transformer, LLM, or RAG-based approaches.

These limitations are presented explicitly to maintain research transparency.

---

## Research Integrity and Historical Transparency

This repository intentionally distinguishes three different stages:

```text
Original Master's Research
          │
          ▼
Original Software Implementation
          │
          ▼
2026 Public Repository Preparation
          │
          ▼
Future Research Directions
```

The 2026 repository preparation does not retroactively attribute modern AI technologies to the original research.

Modern technologies such as transformers, LLMs, semantic embeddings, and RAG are presented only as potential future research directions.

---

## Documentation

Additional documentation is available in the `docs/` directory.

* [`docs/ML_PIPELINE.md`](docs/ML_PIPELINE.md) — machine-learning pipeline and terminology
* [`docs/BUILD.md`](docs/BUILD.md) — build and environment information
* [`docs/DATA_PRIVACY.md`](docs/DATA_PRIVACY.md) — public-release and privacy policy
* [`docs/KNOWN_LIMITATIONS.md`](docs/KNOWN_LIMITATIONS.md) — known technical and research limitations
* [`docs/DEPENDENCIES.md`](docs/DEPENDENCIES.md) — dependency information
* [`docs/MY_CONTRIBUTION.md`](docs/MY_CONTRIBUTION.md) — contribution and research context
* [`PUBLIC_REPOSITORY_MANIFEST.md`](PUBLIC_REPOSITORY_MANIFEST.md) — public-release inventory

---

## Publication

If you use or reference the research described in this repository, please cite the original publication:

```bibtex
@article{luong2014agricultural,
  author  = {Lương Thế Anh and Nguyễn Thái Nghe and Nguyễn Chí Ngôn},
  title   = {Xây dựng hệ thống hỗ trợ khuyến nông trên cây lúa qua mạng thông tin di động},
  journal = {Tạp chí Khoa học Trường Đại học Cần Thơ},
  volume  = {33},
  pages   = {9--21},
  year    = {2014}
}
```

---

## Academic Portfolio Context

This repository forms part of my academic research portfolio in:

* Information Systems
* Machine Learning
* Natural Language Processing
* Intelligent Decision Support Systems
* Human-in-the-Loop AI
* Data-Driven Applications

It documents my earlier research experience in designing and implementing an intelligent information system and provides a foundation for further research into modern intelligent systems.

---

## Why This Project Is Relevant to Future Research

The purpose of this repository is not to present a 2014 system as a modern AI system.

Instead, it demonstrates an early research experience in combining:

```text
Vietnamese Language Processing
            +
Machine Learning
            +
Information Retrieval
            +
Human Expertise
            +
Decision Support
            =
Intelligent Information System
```

This research foundation motivates future investigation into more advanced approaches for human-centered and domain-specific intelligent systems.

---

## License

See the repository license for the terms under which the publicly released source code and documentation may be used.

---

## Author

**Lương Thế Anh**

Master's Research in Information Systems

Research interests:

* Applied Artificial Intelligence
* Machine Learning
* Natural Language Processing
* Intelligent Information Systems
* Decision Support Systems
* Human-in-the-Loop AI

---

## Research Area

**Information Systems · Machine Learning · Natural Language Processing · Decision Support Systems · Human-in-the-Loop AI**
