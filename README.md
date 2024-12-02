# MetaBeeAI_review

Python code to compare output from ASReview across reviewers and domains.

Domains included:
1. Molecular
2. Sub-individual
3. Individual
4. Population
5. Landscape
6. Lethal dose

Reviewers (2 to 3 per domain) were provided with a dataset containing 1053 papers. Every reviewer was provided with a subset of these papers, with a 100-paper overlap with another reviewer to check for consistency in assessing relevancy within each domain. 

The dataset had been prescreened from a larger dataset containing 4,509 papers.

The original dataset (4,509 papers) was obtained from Scopus and Web of Knowledge using the search terms: 

(bee OR bees OR honey* OR bumble* OR solitary OR stingless OR “wild bees" OR pollinator* OR osmia OR apis OR bombs OR xylocop* OR halictid* OR colletid* OR peponap* OR megachil* OR nomi* OR andren* OR melip*) 
AND
(neonicotinoid* OR sulfoximine* OR butenolide* OR cholinergic OR imidacloprid OR clothianidin OR acetamiprid OR thiamethoxam OR dinotefuran OR nitenpyram OR thiacloprid OR acetamiprid OR flupyr* OR sulfoxaflor OR spinosyn OR spinosad OR “seed treatment”) 

This set was screened in ASReview by Rachel Parkinson to narrow down to papers that were about a) bees and b) nicotinic cholinergic pesticides. All off-topic papers were removed at this stage.
