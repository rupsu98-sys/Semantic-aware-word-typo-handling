# Semantic-aware-word-typo-handling
Semantic-Aware Typo Handling for Academic Queries

This project explores how typo handling in natural language queries can be improved by moving beyond surface-level spell correction and incorporating semantic and linguistic context, especially for academic and educational inputs.

Rather than automatically correcting every misspelled word, the system is designed to assess whether a typo meaningfully affects the interpretation of a query.

🔍 Motivation

Traditional spell-checking systems work reasonably well for everyday language but often behave inconsistently when dealing with academic or domain-specific vocabulary. During initial experimentation, common approaches:

Incorrectly corrected academic terms

Produced ambiguous or misleading suggestions

Failed to distinguish between high-impact semantic errors and low-impact spelling noise

This project was motivated by the observation that not all typos are equally important, and that semantic relevance should guide correction decisions.

Project Structure

The system is organized into two conceptual phases.

Phase 1: Lexical Typo Detection

In the first phase, a conventional typo detection and correction pipeline is implemented.

What this phase does:

Tokenizes user queries

Identifies potentially misspelled words

Generates plausible correction candidates using a spell-checker

Key observation:

While effective for common vocabulary, this phase alone proved unreliable for academic terms, motivating a shift away from unconditional correction toward semantic evaluation. No corrections are enforced at this stage—typos are treated as candidates, not errors.


Phase 2: Semantic Impact Evaluation (RAG-Inspired)

To address the limitations observed in Phase 1, the second phase introduces a lightweight, retrieval-augmented approach to determine whether a typo is semantically important.

Instead of asking:

“Is this word misspelled?”

The system asks:

“Does this misspelling affect the meaning of the query?”

Signals used:

FAISS-based retrieval
Corrected word forms are used to retrieve context from a small academic reference corpus to assess domain relevance.

KNN neighborhood analysis
Embedding-based similarity is used to examine whether a word clusters with academically salient terms.

FrameNet grounding (where available)
Frame semantics are used as a linguistic signal to support semantic interpretation.

These signals are combined using an explicit, interpretable decision logic to classify typos as:

⚠️ Semantically important

✅ Likely ignorable

🧠 Design Philosophy

Emphasis on interpretability over optimization

Modular design to support future extensions

Linguistically motivated decision-making rather than black-box correction

Focus on academic query robustness


⚙️ Technologies Used

Python

Sentence Transformers

FAISS

Scikit-learn (KNN)

NLTK FrameNet

OpenStax (academic reference text)

🚧 Limitations

This project is intended as a proof-of-concept, not a production system.

Current limitations include:

Small, domain-limited academic corpus

Sparse FrameNet coverage for technical terms

Rule-based decision logic

No annotated ground-truth labels

These constraints are intentional and help keep the system transparent and extensible.


🚀 Future Directions

Possible extensions include:

Learning-based typo impact classifiers

Larger and more diverse academic corpora

Corpus-based keyness and term salience measures

Deeper semantic resources or ontologies

Integration as a preprocessing or clarification layer for LLM-based systems

🎯 Why This Project Matters

This project demonstrates how linguistic theory, retrieval-based NLP, and distributional semantics can be combined to address a practical and often overlooked problem in language understanding: deciding when a typo actually matters.
