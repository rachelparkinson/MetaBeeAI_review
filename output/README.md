# Output Folder

This folder contains the primary output files generated by the three notebooks in this project. Below is a brief description of each file:

1. **`merged_dataset.csv`**  
   - Produced by **01_merge_datasets.ipynb** after merging the initial input dataset (`input_dataset.csv`) with the ASReview domain files.  
   - Contains all papers from the input dataset and any matching “included” columns from the domain-based CSVs.

2. **`cleaned_merged_dataset.csv`**  
   - Also generated in **01_merge_datasets.ipynb** after removing duplicate rows based on the paper `title`.  
   - Serves as the main consolidated dataset used in subsequent analyses.

3. **`not_included_papers.csv`**  
   - Created in **01_merge_datasets.ipynb** and updated in **03_remove_unassigned.ipynb** to list papers that were never marked as included in **any** of the reviewer domain outputs.  
   - Helps identify articles that may be out of scope or not assigned to a particular domain.

4. **`included_papers.csv`**  
   - Generated in **03_remove_unassigned.ipynb**.  
   - Contains only the papers that were marked as included in at least one domain by any reviewer.  
   - Serves as a filtered dataset of relevant papers.

5. **`final_dataset.csv`**  
   - Created in **03_remove_unassigned.ipynb** by merging `included_papers.csv` and `relevant_unassigned_papers.csv` (from the `../data/` folder).  
   - Represents the final comprehensive dataset, including all relevant and assigned papers.

6. **`missing_doi.csv`**  
   - Produced in **03_remove_unassigned.ipynb** by identifying rows in the `final_dataset.csv` where the `doi` column is missing.  
   - Lists papers without a DOI, allowing for further investigation or DOI retrieval.

---

Feel free to explore these CSV files to see how the data was transformed and consolidated. These outputs are used by the notebooks to facilitate analyses on reviewer agreement, domain overlaps, and to identify unassigned papers or missing DOIs.
