# Student_Guide_RAG
A study-guide RAG chatbot built with Qwen, LoRA, BGE embeddings and Qdrant. Combines semantic and BM25 search with reranking, source citations and a Gradio interface to answer questions using the learner guide and decline unsupported questions.
# A Retrieval-Augmented Chatbot for the EDAB6808 Learner Guide

**EDAB6808 · Assignment 5 · University of the Free State**

## Project overview

This project develops a learner-guide question-answering chatbot using Retrieval-Augmented Generation (RAG). It retrieves relevant passages from the EDAB6808 Learner Guide, uses those passages to generate an answer, identifies supporting sources and refuses requests the guide cannot support.

The learner guide is the assessed knowledge source. The system is a course-specific prototype rather than a general-purpose university assistant.

## System approach

1. Extract and clean the guide's PDF text while retaining page and section metadata.
2. Divide the document into **35 chunks**, of which **33 are eligible for retrieval**.
3. Encode passages using **BGE embeddings** and store the vectors and source metadata in **Qdrant Local**.
4. Combine semantic retrieval with **BM25 keyword search** using Reciprocal Rank Fusion.
5. Rerank candidate evidence and select passages, with additional coverage handling for multi-part questions.
6. Generate evidence-grounded answers using **Qwen2.5-3B-Instruct**, adapted with **LoRA**.
7. Map passage identifiers to source citations, apply refusal checks and present the answer through **Gradio**.

## Evaluation and key findings

The test set contains **31 questions**: 20 direct factual questions, five multi-section questions and six unsupported questions.

| Evaluation measure | Final reported result |
| --- | --- |
| Required source-page coverage | **25/25 answerable questions (100%)** |
| Automatic answer-check passes | **23/25 answerable questions (92%)** |
| Citation-page-check passes | **19/25 answerable questions (76%)** |
| Unsupported questions refused | **6/6 (100%)** |

LoRA increased the overall automatic answer-check pass rate from **88% to 92%**, but multi-section passes decreased from **80% to 60%**. Adaptation therefore produced a mixed outcome rather than a uniform improvement.

The main finding is that retrieving the correct source pages does not ensure that the generated answer combines or cites all required evidence correctly.

## Repository materials

| Material | Contents |
| --- | --- |
| Colab/Jupyter notebook (`.ipynb`) | Document preparation, indexing, retrieval, generation, LoRA adaptation, evaluation and the Gradio interface. |
| Executive report (`.pdf`) | Architecture, experiments, evaluation definitions, results and reflection. |

## Tools and skills

Python, Google Colab, PyMuPDF, Sentence Transformers/BGE, Qdrant, BM25, Transformers, PEFT/LoRA and Gradio. The project connects document processing, semantic search, language-model adaptation, application design and AI evaluation.

## Interpretation and limitations

The reported percentages use project-specific automatic keyword and expected-page checks; they are not a complete measure of factual accuracy. Retrieval, answer quality, citation support and refusal behaviour should be assessed separately. The test set is small, and the observed gains do not establish performance on a wider range of student questions.

The Gradio demonstration depends on an active runtime. A temporary demonstration URL is not permanent hosting; the notebook and executive report provide the enduring record of the project.

## Credits

Collaborative coursework completed by the **EDAB6808 project group**, including **Reatile Seekoei**, at the University of the Free State. Model, library and research references are documented in the executive report.
