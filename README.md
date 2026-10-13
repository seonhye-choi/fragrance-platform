# Sillage — Fragrance Ingredient Intelligence Platform

> A multi-source fragrance ingredient intelligence platform integrating chemistry, regulation, sensory, and market data.

[![Python](https://img.shields.io/badge/Python-3.12-blue)](https://python.org)
[![Streamlit](https://img.shields.io/badge/Streamlit-1.x-red)](https://streamlit.io)
[![License](https://img.shields.io/badge/License-MIT-green)](LICENSE)

---
![Home](assets/screenshot_home.png)
![Ingredients](assets/screenshot_ingredients.png)
![Connections](assets/screenshot_connections.png)
---


## Overview

Fragrance ingredient data is scattered across chemistry databases, regulatory bodies, academic papers, and consumer platforms — with no unified view.

**Sillage** integrates five public data sources into a single ingredient-level intelligence pipeline, with provenance tracked at every layer. At its core: **66 ingredients personally curated through direct olfactory experience** — the layer no public database provides.

---

## Motivation

This project was built to demonstrate two things simultaneously:

1. **Fragrance domain expertise** — personal sensory curation, IFRA regulatory knowledge, industry application mapping
2. **Data engineering capability** — multi-source ETL pipeline, SQLite data modeling, Streamlit dashboard architecture

Target audience: R&D roles at global beauty and fragrance companies (L'Oréal, Givaudan, Firmenich), and graduate program applications (ISIPCA).

---

## Features

| Page | Description |
|---|---|
| **① Ingredients** | Per-ingredient view: chemical data, sensory notes, IFRA regulation, market occurrence, industry signals |
| **② Compare** | Side-by-side comparison of up to 5 ingredients with cosine similarity matching |
| **③ Connections** | Interactive network graph: Ingredient × Industry × Odor Family |
| **④ Market** | Occurrence analytics across 59,325 perfumes (Parfumo 2024 snapshot) |
| **⑤ Intelligence** | Real-time signals: Reddit r/fragrance, industry news, academic papers |
| **⑥ Blend** | Blend simulator + sensory language → ingredient mapping |

---

## Architecture

```
Data Sources
     │
     ├── PubChem API          (CAS, molecular formula, molecular weight)
     ├── IFRA 51st Amendment  (regulatory limits, 18 application categories)
     ├── Pyrfume              (odor descriptors — GoodScents + Leffingwell)
     ├── Parfumo TidyTuesday  (59,325 perfume profiles, 2024 snapshot)
     └── Semantic Scholar     (academic research signal)
     │
Collectors (Python)
     │
   SQLite
(329 ingredients · 4 data layers)
     │
Streamlit Dashboard
(6 pages · Plotly · PyVis · scikit-learn)
```

### Data Quality Tiers

| Tier | Description | Count |
|---|---|---|
| ★★★ CURATED | Personally evaluated — full 4-layer data | 66 ingredients |
| ★★☆ MAPPED | Auto-mapped — chemical + odor descriptors | ~200 ingredients |
| ★☆☆ REGISTERED | IFRA-registered — material layer only | ~63 ingredients |

---

## Tech Stack

| Layer | Technology |
|---|---|
| Dashboard | Streamlit |
| Database | SQLite |
| Data Pipeline | Python 3.12 (requests, pandas) |
| Visualization | Plotly, NetworkX, PyVis |
| Similarity | scikit-learn (cosine similarity) |
| Data Sources | PubChem API, IFRA, Pyrfume, Parfumo, Semantic Scholar |
| Deployment | Streamlit Cloud |

---

## Getting Started

```bash
# 1. Clone
git clone https://github.com/seonhye-choi/fragrance-platform.git
cd fragrance-platform

# 2. Install dependencies
python -m venv .venv
source .venv/bin/activate        # Windows: .venv\Scripts\activate
pip install -r requirements.txt

# 3. Set up environment variables (Optional)
cp .env.example .env
# Note: Core dashboard and intelligence features run out-of-the-box with SQLite.

# 4. Run the data pipeline
python collectors/pubchem_collector.py
python collectors/ifra_collector.py
python collectors/pyrfume_collector.py
python collectors/scholar_collector.py
python processors/load_to_db.py

# 5. Launch
streamlit run dashboard/app.py
```

---

## Project Roadmap & Progress

### Phase 1: Core Foundation & Data Scale-Up (Completed ✅)
- ✅ **Multi-Source ETL Pipeline**: Expanded from 66 curated items to 329 fragrance ingredients across 5 authoritative sources (PubChem, IFRA 51st, Pyrfume, Parfumo, Semantic Scholar).
- ✅ **3-Tier Data Architecture**: Unified SQLite schema tracking provenance across Curated (olfactory evaluated), Mapped (chemical + sensory descriptors), and Registered (regulatory) tiers.
- ✅ **Interactive 6-Page Streamlit Dashboard**: Integrated Material, Sensory, Usage, Occurrence, Similarity Matching, and Blend simulator.
- ✅ **Market Analytics Engine**: Occurrence and co-occurrence patterns analyzed across 59,325 perfumes (Parfumo 2024 snapshot).

### Phase 2: Refinement & Advanced Intelligence (In Progress 🔄)
- 🔄 **Sensory Data Cleansing & NLP Enrichment**: Standardizing and harmonizing sensory descriptors across scaled ingredients.
- 🔄 **Community Pulse Pipeline**: Robust RSS/API collection and trend extraction for r/fragrance signals.
- 🔄 **Cloud Deployment**: Streamlit Cloud deployment and AWS migration planning (SQLite → RDS, Collectors → Lambda + EventBridge).

### Phase 3: Future Enhancements (Planned 🚀)
- AI-generated highlight quotes and sensory insights (Claude API)
- Odor detection threshold modeling and GC-MS analytical data integration

---

## Data Sources & Licensing

| Source | Terms |
|---|---|
| PubChem | Public domain (NIH) |
| IFRA 51st Amendment | Public — non-commercial |
| Pyrfume (GoodScents, Leffingwell) | Open data |
| Parfumo TidyTuesday | Non-commercial use only |
| Semantic Scholar | Open access API |
| Personal sensory data | Original — direct olfactory evaluation |
