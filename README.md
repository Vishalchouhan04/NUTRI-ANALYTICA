NUTRI-ANALYTICA — Personalized Diet Recommendation System
📑 Table of contents

General info

How it works

Features

Architecture

Technologies

Setup (local & Docker)

API (preview)

Citation

📜 General info

NUTRI-ANALYTICA is a personalized diet recommendation web app that analyzes a user’s BMI, physical attributes, and health goals to provide tailored nutritional guidance. The product direction was shaped through user discovery (surveys/interviews) and iterative testing to focus on clarity, usefulness, and goal-based outcomes. 

Vishal_Chouhan

Why a content-based approach?

Works immediately without needing other users’ data (no cold start).

Easy to explain why items are recommended (transparent).

Naturally respects dietary constraints and preferences.

Simple to extend with new attributes (ingredients, macros, cuisine, allergens).

Known challenges: novelty/diversity can be lower; relies on good item metadata; and can be heavy at scale without indexing.

🧠 How it works

Profile intake: Users provide age, height, weight, activity, and goals (e.g., weight loss, maintenance, muscle gain). The system derives BMI and daily targets. 

Vishal_Chouhan

Vectorization: Recipe/meal items are represented by nutritional and ingredient features.

Similarity search: A Nearest-Neighbors layer (cosine similarity) retrieves meals close to the user’s target vector (macros/micros/preferences).

Goal alignment: Results are re-ranked to better match goal constraints (calorie bands, macro ratios) and flagged for allergens/exclusions.

Explainability: Each suggestion carries a short “why this” note (e.g., “high-protein, low-carb; fits 500–550 kcal window”).

Under the hood we use a brute-force cosine similarity for small/medium datasets; you can switch to BallTree/KDTree/ANN when scaling.

✨ Features

Personalized plan suggestions driven by BMI + goals. 

Vishal_Chouhan

Adjustable macro targets and exclusions (e.g., vegetarian, nut-free).

“Custom recommend” mode to hand-tune nutrition sliders.

Clear rationales and basic nutrition breakdown per meal.

Mobile-first, accessible UI with Tailwind. 

Vishal_Chouhan

🧩 Architecture

NUTRI-ANALYTICA follows a lightweight, service-oriented split:

Core ML Service (Python + Flask):
Computes embeddings, runs similarity search, and returns recommendations via REST. 

Vishal_Chouhan

Web App (React + Tailwind):
Responsive front-end with interactive forms, results, and explainability cards. 

Vishal_Chouhan

App/Proxy Layer (Node.js + Express):
Handles auth/session, rate limits, and composes data from Core ML + DB. 

Vishal_Chouhan

Data Store:

MongoDB for user profiles, sessions, logs (prod). 

Vishal_Chouhan

SQLite for quick local development and fixtures. 

Vishal_Chouhan

Note: If you prefer a single-service build, you can run the Flask API and a minimal UI only.

🚀 Technologies

Core: Python, Flask, scikit-learn, NumPy, pandas 

Vishal_Chouhan

Front-end: React, Tailwind CSS (mobile-first) 

Vishal_Chouhan

App/Backend: Node.js (Express) + MongoDB (prod), SQLite (local) 

Vishal_Chouhan

Tooling: Docker & Docker Compose
