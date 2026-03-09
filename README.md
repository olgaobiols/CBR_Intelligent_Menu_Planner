# Case-Based Reasoning for Intelligent Menu Generation

A **Hybrid Case-Based Reasoning (CBR)** system designed to plan and recommend personalized gastronomic menus for events. [cite_start]This project integrates symbolic knowledge (ontologies) with sub-symbolic representations (FlavorGraph latent vector spaces) to solve complex culinary constraints[cite: 1].

[cite_start]Developed as part of the **Knowledge-Based Systems (SBC)** course for the **Bachelor's Degree in Artificial Intelligence (UPC)**[cite: 1].

## Authors
- [cite_start]**Blanca Mira Fradera** [cite: 1]
- [cite_start]**Laida Queral Llopart** [cite: 1]
- [cite_start]**Olga Obiols Fuentes** [cite: 1]

## Problem Overview
[cite_start]The system automates menu planning for a catering company ("RicoRico"), handling diverse requirements[cite: 1]:
- [cite_start]**Hard Constraints**: Management of 15 normalized allergy categories and strict diets (vegan, halal, celiac, etc.)[cite: 1].
- [cite_start]**Qualitative Preferences**: Preferred culinary styles (Japanese, smoked, tropical), event formality, and seasonality[cite: 1].
- [cite_start]**Logistics**: Guest count and target budget optimization[cite: 1].

[cite_start]Unlike rule-based systems, this CBR approach uses "algorithmic creativity" to **adapt** existing recipes to new user constraints while ensuring food safety[cite: 1].

## Implementation: The CBR Cycle
[cite_start]The project implements the full 4R cycle[cite: 1, 36, 35, 37]:

1. [cite_start]**Retrieve**: Uses a weighted global similarity function and *Adaptation-Guided Retrieval* to find the most useful cases that are easily adaptable to the user's specific restrictions[cite: 36].
2. **Reuse & Adapt**:
    - **Symbolic Adaptation**: Handles dietary restrictions and "Banned Pairs" (ingredients rejected together by the user).
    - [cite_start]**Sub-symbolic Adaptation**: Utilizes **FlavorGraph** embeddings and *Vector Steering* to perform creative ingredient substitutions based on molecular and flavor profiles[cite: 15].
    - [cite_start]**Technique Module**: Selects cooking techniques (standard vs. haute cuisine) and uses a *Rollback* mechanism to stay within budget[cite: 9].
    - [cite_start]**Beverage Module**: Dynamic pairings based on structural and aromatic affinity[cite: 10].
3. **Revise**: Multi-dimensional evaluation (global satisfaction, taste, originality). [cite_start]Features a **Dual Memory Architecture** to distinguish between personal preferences (Channel A) and learned domain consensus (Channel B)[cite: 35].
4. [cite_start]**Retain**: Selective retention policy that learns new cases based on their utility, novelty, and safety[cite: 37].

## Technologies
- [cite_start]**Python**: Core logic and CBR cycle orchestration[cite: 12].
- [cite_start]**FlavorGraph**: Pre-trained vector embeddings for calculating semantic and chemical distances between ingredients[cite: 15].
- [cite_start]**Gemini API (LLM)**: Used exclusively as a formalization layer to generate the final menu text and dish presentations[cite: 1].
- [cite_start]**Hugging Face**: Menu image generation for a complete visual experience[cite: 1].

## Repository Structure
- [cite_start]`/src`: Implementation of cycle phases (`Retriever.py`, `Revise.py`, `Retain.py`) and specialized operators[cite: 36, 35, 37].
- [cite_start]`/data`: Knowledge base including ingredients, beverages, latent styles, and the case base[cite: 43, 47, 45, 48].
- [cite_start]`/models`: Mathematical representation of FlavorGraph embeddings[cite: 40].

## How to Run
1. Install the required Python dependencies.
2. Configure your Gemini API key (optional, for advanced text generation).
3. Execute the main orchestrator:
   ```bash
   python src/main.py
    ```

## Key Features & Explainability (XCBR)
* 
**Explainability**: Every decision (pairing, allergy substitution) is justified to the user in natural language.


* 
**Active Learning**: If multiple users reject a specific combination, the system automatically generates a **Global Constraint Rule**.


* 
**Robustness**: Validated with complex test cases ranging from informal dinners to large corporate banquets.