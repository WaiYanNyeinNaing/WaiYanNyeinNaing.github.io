---
layout: page
title: rads-agent
description: Meta-Agent for Retrieval-Augmented Data Science
img: assets/img/blog/rads-agent/rads_architecture.png
importance: 1
category: work
github: https://github.com/WaiYanNyeinNaing/rads-agent
---

`rads-agent` is an autonomous system that transforms raw, unorganized datasets into a functional Retrieval-Augmented Data Science (RADS) cluster.

By functioning as a zero-tuning Meta-Agent layer, the system autonomously:

- Analyzes raw tabular data and telemetry for latent structure.
- Builds dynamic semantic layers tailored to the specific context.
- Generates algorithms and retrieval patterns for rapid data intelligence.

It bridges the gap between massive raw files and business execution by orchestrating a dedicated cluster of agents that model and converse with your data.

### Motivation: Why I Built This

Every data project starts with the same tedious boilerplate: downloading files, extracting CSVs, inferring schemas, loading data into Pandas or a database, and writing baseline aggregation queries. I built `rads-agent` to automate this "plumbing" phase. The goal is to drop a Kaggle URL and immediately start querying, analyzing, and visualizing the data without writing setup code.

### The Problem Statement

Directly exposing raw, flat CSV files to an LLM leads to hallucinations. Standard Text-to-SQL fails on raw data because it lacks business logic, clear entity relationships, and governed metric definitions. To make LLMs reliable for data analysis, they need a structured semantic layer. However, manually setting up a database server and defining schemas for every exploratory dataset is far too slow and defeats the purpose of rapid prototyping.

### The Solution

`rads-agent` is an autonomous Python system that bridges raw files and reliable LLM querying. It transforms unstructured Kaggle datasets into a functional, local data environment equipped with an auto-generated semantic layer.

<div class="row mt-3 justify-content-center">
    <div class="col-sm mt-3 mt-md-0 text-center">
        {% include figure.liquid loading="eager" path="assets/img/blog/rads-agent/rads_architecture.png" class="img-fluid rounded z-depth-1 blog-img-small" %}
    </div>
</div>
<div class="caption">
    The high-level architecture of rads-agent.
</div>

The architecture is driven by four core components:

1. **Automated Ingestion (`kaggle_agent.py`):** Interfaces with the Kaggle API to automatically download and extract raw CSVs directly into the local file system.

<div class="row mt-3 justify-content-center">
    <div class="col-sm mt-3 mt-md-0 text-center">
        {% include figure.liquid loading="eager" path="assets/img/blog/rads-agent/ingest_screenshot.png" class="img-fluid rounded z-depth-1 blog-img-small" %}
    </div>
</div>
<div class="caption">
    Automated ingestion skipping the boilerplate data download steps.
</div>

2. **Embedded Analytical Engine (`database_manager.py`):** Uses **DuckDB** for high-performance, in-process SQL querying. It automatically mounts raw CSVs as "Bronze" views using DuckDB’s `read_csv_auto` function. Because DuckDB uses a vectorized execution engine, it processes complex aggregations over millions of rows in milliseconds—running completely local without the need for external database servers.
3. **Semantic Modeling (`semantic_engine.py`):** Profiles a sample of the raw data and prompts the LLM to generate a structured JSON schema mapping dimensions and measures. It then compiles DuckDB-compatible SQL to build clean, aggregated "Gold" views. This semantic layer provides the LLM with the exact structure and context it needs for accurate query generation.
4. **Execution & UI (`app.py` & `eda_agent.py`):** A Gradio frontend exposing a dual-interface:
   - **Semantic Chat:** Translates user questions into precise DuckDB SQL, executing them against the Gold views via LLM tool-calling for deterministic data retrieval.
   - **EDA Agent:** Writes and executes dynamic Python code (`pandas`, `matplotlib`, `seaborn`) locally via `exec()`. It intercepts rendering functions (like `plt.show()`) to capture charts as base64 strings, streaming visualizations directly back to the chat interface.

<div class="row mt-3 justify-content-center">
    <div class="col-sm mt-3 mt-md-0 text-center">
        {% include figure.liquid loading="eager" path="assets/img/blog/rads-agent/chat_screenshot.png" class="img-fluid rounded z-depth-1 blog-img-small" %}
    </div>
</div>
<div class="caption">
    Semantic Chat executing text-to-SQL workflows accurately.
</div>

<div class="row mt-3 justify-content-center">
    <div class="col-sm mt-3 mt-md-0 text-center">
        {% include figure.liquid loading="eager" path="assets/img/blog/rads-agent/advanced_eda.png" class="img-fluid rounded z-depth-1 blog-img-small" %}
    </div>
</div>
<div class="caption">
    Advanced Exploratory Data Analysis powered by the EDA Agent.
</div>

### The Impact

By combining the vectorized speed of DuckDB with the code-generation capabilities of Gemini, `rads-agent` reduces the time-to-insight for new datasets from hours to minutes. It provides developers and data practitioners with a zero-infrastructure, automated Medallion architecture that runs entirely on a local machine, transforming static files into a fully conversational data cluster.

**Repository:** <a href="https://github.com/WaiYanNyeinNaing/rads-agent" target="_blank">WaiYanNyeinNaing/rads-agent</a>
