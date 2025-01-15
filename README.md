# MetaBeeAI_review

This repository contains Python code and associated data to compare **ASReview** outputs across multiple domains (e.g., Molecular, Sub-individual, Individual, Population, Community, and Lethal Dose) and multiple reviewers within each domain. The goal is to assess consistency and identify relevant papers in each domain from a prescreened dataset of bee-related pesticide research.

---

## Overview

### ASReview Process
- **Initial Dataset**: Started with **4,509** papers from Scopus and Web of Knowledge. Search terms included:

(bee OR bees OR honey* OR bumble* OR solitary OR stingless OR “wild bees" OR pollinator* OR osmia OR apis OR bombs OR xylocop* OR halictid* OR colletid* OR peponap* OR megachil* OR nomi* OR andren* OR melip*) AND (neonicotinoid* OR sulfoximine* OR butenolide* OR cholinergic OR imidacloprid OR clothianidin OR acetamiprid OR thiamethoxam OR dinotefuran OR nitenpyram OR thiacloprid OR acetamiprid OR flupyr* OR sulfoxaflor OR spinosyn OR spinosad OR “seed treatment”)

## Prescreening

From the larger set of **4,509** papers (obtained via Scopus and Web of Knowledge), a **prescreening** step was performed in **ASReview** by Rachel Parkinson. This step filtered out off-topic papers, resulting in **1,053** papers about:

1. Bees
2. Nicotinic cholinergic pesticides

### Reviewer Assignments

Each reviewer domain (e.g., Molecular, Sub-individual, Individual, Population, Landscape, Lethal Dose) received a subset of these **1,053** papers. There was a **100-paper overlap** between reviewers in the same domain to check consistency. Depending on the domain, each had 2 or 3 reviewers evaluating relevancy.

---

## Repository Structure

```bash
MetaBeeAI_review/
├── README.md              # High-level overview (this file)
├── notebooks/             # Jupyter notebooks for data merging & analysis
│   ├── 01_merge_datasets.ipynb
│   ├── 02_review_output.ipynb
│   └── README.md          # Explanation of the notebooks
├── data/                  # Folder containing the input dataset & ASReview outputs
│   ├── input_dataset.csv
│   └── asreview_output/
│       ├── community/
│       ├── individual/
│       ├── ld50/
│       ├── molecular/
│       ├── population/
│       └── subindividual/
│   └── README.md          # Explanation of data folder structure & files
├── output/                # Folder with merged CSV, cleaned dataset, etc.
│   ├── merged_dataset.csv
│   ├── cleaned_merged_dataset.csv
│   └── not_included_papers.csv
│   └── README.md          # Explanation of output files
├── requirements.txt       # Python dependencies (if applicable)
└── .gitignore             # Common ignores (venv, etc.)
```

## Key Points

- **Notebooks**  
  - **`01_merge_datasets.ipynb`** merges the input CSV (`input_dataset.csv`) with each domain’s ASReview output, then deduplicates papers.  
  - **`02_review_output.ipynb`** analyzes reviewer agreement, overlaps across domains, and generates summary plots/tables.

- **Data Folder**  
  - **`input_dataset.csv`** contains the 1,053 prescreened papers.  
  - **`asreview_output/`** is subdivided by domain, containing CSV files where each reviewer marked papers as included or excluded.

- **Output Folder**  
  - **`merged_dataset.csv`**: All papers merged with reviewer domain inclusions.  
  - **`cleaned_merged_dataset.csv`**: Deduplicated final version of the merged dataset.  
  - **`not_included_papers.csv`**: Papers that were not marked as included by any reviewer/domain.

---

## Usage

1. **Clone Repository**  
```bash
git clone https://github.com/YourUsername/MetaBeeAI_review.git
cd MetaBeeAI_review
```
2. **Install Dependencies (if using Python)**
``` bash
Copy code
pip install -r requirements.txt
(Adjust if using conda or another environment manager.)
```
## Run Notebooks

- **`01_merge_datasets.ipynb`**: Merges domain outputs with `input_dataset.csv` and creates `cleaned_merged_dataset.csv`.
- **`02_review_output.ipynb`**: Loads the cleaned dataset for analysis of reviewer agreement, domain overlaps, etc.

---

## Check Outputs

- All merged/analysis output files appear in the `output/` folder, including:
  - **`merged_dataset.csv`**
  - **`cleaned_merged_dataset.csv`**
  - **`not_included_papers.csv`**

---

## Contributing

Contributions are welcome! For major changes, please open an issue first to discuss the proposed updates.  
Remember to add or update tests as appropriate.

---

## License

This work is licensed under the [Creative Commons Attribution 4.0 International License](https://creativecommons.org/licenses/by/4.0/).

---

**Thank you for exploring MetaBeeAI_review!**  
For questions or suggestions, feel free to open an issue or contact the maintainers.
