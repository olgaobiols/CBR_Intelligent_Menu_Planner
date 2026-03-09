# Case-Based Reasoning for Intelligent Menu Generation

A **Hybrid Case-Based Reasoning (CBR)** system designed to plan and recommend personalized gastronomic menus for events. This project integrates symbolic knowledge (ontologies) with sub-symbolic representations (FlavorGraph latent vector spaces) to solve complex culinary constraints.

Developed as part of the **Knowledge-Based Systems (SBC)** course for the **Bachelor's Degree in Artificial Intelligence (UPC)**.

## Authors
- **Blanca Mira Fradera**
- **Laida Queral Llopart**
- **Olga Obiols Fuentes**

## Problem Overview
The system automates menu planning for a catering company ("RicoRico"), handling diverse requirements:
- **Hard Constraints**: Management of 15 normalized allergy categories and strict diets (vegan, halal, celiac, etc.).
- **Qualitative Preferences**: Preferred culinary styles (Japanese, smoked, tropical), event formality, and seasonality.
- **Logistics**: Guest count and target budget optimization.

Unlike rule-based systems, this CBR approach uses "algorithmic creativity" to **adapt** existing recipes to new user constraints while ensuring food safety.

## Implementation: The CBR Cycle
The project implements the full 4R cycle:

1. **Retrieve**: Uses a weighted global similarity function and *Adaptation-Guided Retrieval* to find the most useful cases that are easily adaptable to the user's specific restrictions.
2. **Reuse & Adapt**:
    - **Symbolic Adaptation**: Handles dietary restrictions and "Banned Pairs" (ingredients rejected together by the user).
    - **Sub-symbolic Adaptation**: Utilizes **FlavorGraph** embeddings and *Vector Steering* to perform creative ingredient substitutions based on molecular and flavor profiles.
    - **Technique Module**: Selects cooking techniques (standard vs. haute cuisine) and uses a *Rollback* mechanism to stay within budget.
    - **Beverage Module**: Dynamic pairings based on structural and aromatic affinity.
3. **Revise**: Multi-dimensional evaluation (global satisfaction, taste, originality). Features a **Dual Memory Architecture** to distinguish between personal preferences (Channel A) and learned domain consensus (Channel B).
4. **Retain**: Selective retention policy that learns new cases based on their utility, novelty, and safety.

## Technologies
- **Python**: Core logic and CBR cycle orchestration.
- **FlavorGraph**: Pre-trained vector embeddings for calculating semantic and chemical distances between ingredients.
- **Gemini API (LLM)**: Used exclusively as a formalization layer to generate the final menu text and dish presentations.
- **Hugging Face**: Menu image generation for a complete visual experience.

## Repository Structure
- `/src`: Implementation of cycle phases (`Retriever.py`, `Revise.py`, `Retain.py`) and specialized operators (ingredients, beverages, techniques).
- `/data`: Knowledge base including ingredients, beverages, latent styles, and the case base.
- `/models`: Mathematical representation of FlavorGraph embeddings (`.pickle`).

## How to Run
1. Install the required Python dependencies.
2. Configure your Gemini API key (optional, for advanced text generation).
3. Execute the main orchestrator:
   ```bash
   python src/main.py
   ```

## Key Features & Explainability (XCBR)
* **Explainability**: Every decision (pairing, allergy substitution) is justified to the user in natural language.
* **Active Learning**: If multiple users reject a specific combination, the system automatically generates a **Global Constraint Rule**.
* **Robustness**: Validated with complex test cases ranging from informal dinners to large corporate banquets.
