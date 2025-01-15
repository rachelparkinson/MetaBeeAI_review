# Data Folder

This folder contains the initial **input dataset** of papers (`input_dataset.csv`) and the **ASReview output** files for various reviewer domains. Below is an overview of the folder structure and the purpose of each file and subfolder.

---

## Folder Contents

data/ ├─ input_dataset.csv └─ asreview_output/ ├─ community/ │ ├─ commu_AB.csv │ └─ commu_RP.csv ├─ individual/ │ ├─ indiv_AB.csv │ └─ indiv_RP.csv ├─ ld50/ │ ├─ letha_ER.csv │ ├─ letha_ES.csv │ ├─ letha_NN.csv │ └─ letha_RP.csv ├─ molecular/ │ ├─ molec_AH.csv │ ├─ molec_AJ.csv │ └─ molec_EA.csv ├─ population/ │ ├─ popul_CB.csv │ └─ popul_RP.csv └─ subindividual/ ├─ subin_RP.csv └─ subin_RT.csv


---

## Files and Directories

1. **`input_dataset.csv`**
   - Contains all papers identified in the initial systematic review step.
   - Criteria for inclusion in this initial dataset:
     1. Research articles
     2. Pertaining to nicotinic cholinergic pesticides
     3. About bees (any species)

2. **`asreview_output/`**
   - Houses subfolders for each **reviewer domain**. 
   - Each subfolder contains one or more CSV files produced by ASReview that assign relevance (i.e., inclusion) of individual papers to that domain.

   **Subfolders**:
   - **`community/`**  
     - Files: `commu_AB.csv`, `commu_RP.csv`  
     - Domain: **Communities** (e.g., effects on bee communities or multi-colony interactions)
   - **`individual/`**  
     - Files: `indiv_AB.csv`, `indiv_RP.csv`  
     - Domain: **Individual** (focus on individual bees)
   - **`ld50/`**  
     - Files: `letha_ER.csv`, `letha_ES.csv`, `letha_NN.csv`, `letha_RP.csv`  
     - Domain: **Lethal dose endpoints** (e.g., LD50 analyses)
   - **`molecular/`**  
     - Files: `molec_AH.csv`, `molec_AJ.csv`, `molec_EA.csv`  
     - Domain: **Molecular** (molecular biology, gene expression, etc.)
   - **`population/`**  
     - Files: `popul_CB.csv`, `popul_RP.csv`  
     - Domain: **Population** (population-level or colony-level studies)
   - **`subindividual/`**  
     - Files: `subin_RP.csv`, `subin_RT.csv`  
     - Domain: **Subindividual** (physiology, histology, or cellular-level effects)

---

## Usage and Notes

- **Merging**: The CSV files in each domain folder (`community`, `individual`, etc.) do **not** necessarily contain all rows from the initial `input_dataset.csv`. Each file represents papers identified for that domain by specific reviewers.
- **File Naming**: For example, `commu_AB.csv` and `commu_RP.csv` indicate two different reviewers (or reviewer teams) for the “community” domain.
- **Integration**: These files are typically merged with the `input_dataset.csv` to create a unified dataset of papers with multiple domain assignments.  

If you need to perform merges or cross-domain analyses:
1. **Start** with `input_dataset.csv` as the baseline for all papers.  
2. **Merge** each CSV in `asreview_output/` based on the paper identifier (e.g., `title`).  
3. **Aggregate** or resolve conflicts if a paper is evaluated by multiple reviewers or domains.

---

**End of README**
