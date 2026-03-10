# Black Box Optimization Capstone Project

This repository contains the code, data, and documentation for the 13-week Black Box Optimization (BBO) Challenge. The goal is to optimize eight unknown "black box" functions using Sequential Model-Based Optimization (SMBO).

## 📂 Documentation

* **[📄 Datasheet](Datasheet.md):** Details on the dataset composition, collection process, and intended uses.
* **[🃏 Model Card](MODELCARD.md):** Overview of the optimization strategy, performance metrics, and limitations.

## 🚀 Project Overview

* **Methods:** Gaussian Process Regression, Trust Region Optimization, Expected Improvement.
* **Tech Stack:** Python, Scikit-Learn, SciPy.
* **Status:** Active (Week 10 of 13).
Gemini said
## Project Overview: Optimizing the Unknown
This project tackles the challenge of Bayesian Black-Box Optimization (BBO)—the art of finding the "best" settings for complex systems when we don't know the underlying math. From fine-tuning chemical yields to perfecting a 5-ingredient cake recipe and optimizing 8-dimensional machine learning models, I developed a custom AI-driven framework to navigate these invisible landscapes.

# The Process: Search, Learn, Refine
Using Gaussian Processes, my model built a "map" of each problem based on limited data. I balanced two competing goals: Exploration (searching new areas to avoid traps) and Exploitation (narrowing in on known peaks). As the challenge progressed, I moved from broad global searches to high-precision Trust Regions, effectively "zooming in" on the most promising results to squeeze out every decimal of performance.

# The Outcomes
The strategy proved highly effective across diverse scenarios. By the final weeks, the model successfully identified record-breaking configurations in high-dimensional spaces—most notably in Function 8, where it navigated an 8D "needle-in-a-haystack" to achieve a near-optimal score of 9.883. This project demonstrates how probabilistic modeling can solve real-world problems where data is expensive and the answers are hidden.
