```python
import os
import pandas as pd
```

Define paths for input data and output and load data


```python
input_dataset_path = "../data/input_dataset.csv"

# Load input dataset
input_df = pd.read_csv(input_dataset_path)
```

Check the first few rows of the input dataset.


```python
print("Input Dataset:")
display(input_df.head())
```

    Input Dataset:
    


<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>record_id</th>
      <th>type_of_reference</th>
      <th>title</th>
      <th>authors</th>
      <th>secondary_title</th>
      <th>abstract</th>
      <th>year</th>
      <th>doi</th>
      <th>volume</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>JOUR</td>
      <td>Functional orthologs of honeybee CYP6AQ1 in st...</td>
      <td>['Xiao, XZ', 'Haas, J', 'Nauen, R']</td>
      <td>ECOTOXICOLOGY AND ENVIRONMENTAL SAFETY</td>
      <td>Flupyradifurone (FPF), a novel butenolide inse...</td>
      <td>2023</td>
      <td>10.1016/j.ecoenv.2023.115719</td>
      <td>268</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>JOUR</td>
      <td>Design and structure optimization of novel but...</td>
      <td>['Zhu, K.', 'Lu, X.', 'Li, X.', 'Han, Q.', 'Zo...</td>
      <td>Journal of Molecular Structure</td>
      <td>The discovery of new neonicotinoid alternative...</td>
      <td>2023</td>
      <td>10.1016/j.molstruc.2023.135257</td>
      <td>1282</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>JOUR</td>
      <td>The threat of pesticide and disease co-exposur...</td>
      <td>['Yordanova, M', 'Evison, SEF', 'Gill, RJ', 'G...</td>
      <td>INTERNATIONAL JOURNAL FOR PARASITOLOGY-PARASIT...</td>
      <td>Brood diseases and pesticides can reduce the s...</td>
      <td>2022</td>
      <td>10.1016/j.ijppaw.2022.03.001</td>
      <td>17</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>JOUR</td>
      <td>Pesticide and resource stressors additively im...</td>
      <td>['Stuligross, C', 'Williams, NM']</td>
      <td>PROCEEDINGS OF THE ROYAL SOCIETY B-BIOLOGICAL ...</td>
      <td>Bees and other beneficial insects experience m...</td>
      <td>2020</td>
      <td>10.1098/rspb.2020.1390</td>
      <td>287</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>JOUR</td>
      <td>Synergistic toxicity and physiological impact ...</td>
      <td>['Zhu, Y.C.', 'Yao, J.', 'Adamczyk, J.', 'Lutt...</td>
      <td>PLoS ONE</td>
      <td>Imidacloprid is the most widely used insectici...</td>
      <td>2017</td>
      <td>10.1371/journal.pone.0176837</td>
      <td>12</td>
    </tr>
  </tbody>
</table>
</div>


Step 2: Find and load the ASReview output files. Iterate through each subfolder in asreview_output. Find csv files and merge with input dataset.


```python
asreview_output_path = "../data/asreview_output"

# Iterate through each subfolder in asreview_output
for subfolder in os.listdir(asreview_output_path):
    subfolder_path = os.path.join(asreview_output_path, subfolder)
    
    # Check if it's a directory
    if os.path.isdir(subfolder_path):
        # List all CSV files in the subfolder
        for file_name in os.listdir(subfolder_path):
            if file_name.endswith(".csv"):
                file_path = os.path.join(subfolder_path, file_name)
                
                # Load the output CSV file
                output_df = pd.read_csv(file_path)
                
                # Check if the output file contains the required columns
                if 'title' in output_df.columns and 'included' in output_df.columns:
                    # Extract only the "title" and "included" columns
                    temp_df = output_df[['title', 'included']].copy()
                    
                    # Rename the "included" column to the filename (without ".csv")
                    column_name = file_name.replace(".csv", "")
                    temp_df.rename(columns={"included": column_name}, inplace=True)
                    
                    # Merge with the input dataset using the "title" column
                    input_df = input_df.merge(temp_df, on='title', how='left')
```

Display and save output as .csv


```python
output_path = "../output/merged_dataset.csv"
input_df.to_csv(output_path, index=False)

print(f"Final merged dataset saved to: {output_path}")
display(input_df.head())
```

    Final merged dataset saved to: ../output/merged_dataset.csv
    


<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>record_id</th>
      <th>type_of_reference</th>
      <th>title</th>
      <th>authors</th>
      <th>secondary_title</th>
      <th>abstract</th>
      <th>year</th>
      <th>doi</th>
      <th>volume</th>
      <th>commu_AB</th>
      <th>...</th>
      <th>letha_ES</th>
      <th>letha_NN</th>
      <th>letha_RP</th>
      <th>molec_AH</th>
      <th>molec_AJ</th>
      <th>molec_EA</th>
      <th>popul_CB</th>
      <th>popul_RP</th>
      <th>subin_RP</th>
      <th>subin_RT</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>JOUR</td>
      <td>Functional orthologs of honeybee CYP6AQ1 in st...</td>
      <td>['Xiao, XZ', 'Haas, J', 'Nauen, R']</td>
      <td>ECOTOXICOLOGY AND ENVIRONMENTAL SAFETY</td>
      <td>Flupyradifurone (FPF), a novel butenolide inse...</td>
      <td>2023</td>
      <td>10.1016/j.ecoenv.2023.115719</td>
      <td>268</td>
      <td>NaN</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>JOUR</td>
      <td>Functional orthologs of honeybee CYP6AQ1 in st...</td>
      <td>['Xiao, XZ', 'Haas, J', 'Nauen, R']</td>
      <td>ECOTOXICOLOGY AND ENVIRONMENTAL SAFETY</td>
      <td>Flupyradifurone (FPF), a novel butenolide inse...</td>
      <td>2023</td>
      <td>10.1016/j.ecoenv.2023.115719</td>
      <td>268</td>
      <td>NaN</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>JOUR</td>
      <td>Design and structure optimization of novel but...</td>
      <td>['Zhu, K.', 'Lu, X.', 'Li, X.', 'Han, Q.', 'Zo...</td>
      <td>Journal of Molecular Structure</td>
      <td>The discovery of new neonicotinoid alternative...</td>
      <td>2023</td>
      <td>10.1016/j.molstruc.2023.135257</td>
      <td>1282</td>
      <td>NaN</td>
      <td>...</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>JOUR</td>
      <td>The threat of pesticide and disease co-exposur...</td>
      <td>['Yordanova, M', 'Evison, SEF', 'Gill, RJ', 'G...</td>
      <td>INTERNATIONAL JOURNAL FOR PARASITOLOGY-PARASIT...</td>
      <td>Brood diseases and pesticides can reduce the s...</td>
      <td>2022</td>
      <td>10.1016/j.ijppaw.2022.03.001</td>
      <td>17</td>
      <td>NaN</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>JOUR</td>
      <td>Pesticide and resource stressors additively im...</td>
      <td>['Stuligross, C', 'Williams, NM']</td>
      <td>PROCEEDINGS OF THE ROYAL SOCIETY B-BIOLOGICAL ...</td>
      <td>Bees and other beneficial insects experience m...</td>
      <td>2020</td>
      <td>10.1098/rspb.2020.1390</td>
      <td>287</td>
      <td>NaN</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 24 columns</p>
</div>


Merge any duplicate rows


```python
# Step 1: Check for duplicates in the merged dataset
# Load the merged dataset
merged_dataset_path = "../output/merged_dataset.csv"
merged_df = pd.read_csv(merged_dataset_path)

# Step 2: Identify duplicates based on the 'title' column
duplicates = merged_df[merged_df.duplicated(subset='title', keep=False)]

if not duplicates.empty:
    print("\nDuplicated rows detected:")
    display(duplicates)
    
    # Step 3: Merge duplicated rows by aggregating values
    # Here we keep the first non-null value or combine them logically
    merged_df = (
        merged_df.groupby('title', as_index=False)  # Group by the 'title' column
        .first()                                   # Use the first non-duplicated row
    )
else:
    print("\nNo duplicated rows detected.")

# Step 4: Save the cleaned dataset
cleaned_output_path = "../output/cleaned_merged_dataset.csv"
merged_df.to_csv(cleaned_output_path, index=False)

print(f"Cleaned dataset saved to: {cleaned_output_path}")
display(merged_df.head())
```

    
    Duplicated rows detected:
    


<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>record_id</th>
      <th>type_of_reference</th>
      <th>title</th>
      <th>authors</th>
      <th>secondary_title</th>
      <th>abstract</th>
      <th>year</th>
      <th>doi</th>
      <th>volume</th>
      <th>commu_AB</th>
      <th>...</th>
      <th>letha_ES</th>
      <th>letha_NN</th>
      <th>letha_RP</th>
      <th>molec_AH</th>
      <th>molec_AJ</th>
      <th>molec_EA</th>
      <th>popul_CB</th>
      <th>popul_RP</th>
      <th>subin_RP</th>
      <th>subin_RT</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>JOUR</td>
      <td>Functional orthologs of honeybee CYP6AQ1 in st...</td>
      <td>['Xiao, XZ', 'Haas, J', 'Nauen, R']</td>
      <td>ECOTOXICOLOGY AND ENVIRONMENTAL SAFETY</td>
      <td>Flupyradifurone (FPF), a novel butenolide inse...</td>
      <td>2023</td>
      <td>10.1016/j.ecoenv.2023.115719</td>
      <td>268</td>
      <td>NaN</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>JOUR</td>
      <td>Functional orthologs of honeybee CYP6AQ1 in st...</td>
      <td>['Xiao, XZ', 'Haas, J', 'Nauen, R']</td>
      <td>ECOTOXICOLOGY AND ENVIRONMENTAL SAFETY</td>
      <td>Flupyradifurone (FPF), a novel butenolide inse...</td>
      <td>2023</td>
      <td>10.1016/j.ecoenv.2023.115719</td>
      <td>268</td>
      <td>NaN</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>21</th>
      <td>21</td>
      <td>JOUR</td>
      <td>Non-additive gene interactions underpin molecu...</td>
      <td>['Paten, AM', 'Colin, T', 'Coppin, CW', 'Court...</td>
      <td>SCIENCE OF THE TOTAL ENVIRONMENT</td>
      <td>Understanding the cumulative risk of chemical ...</td>
      <td>2022</td>
      <td>10.1016/j.scitotenv.2021.152614</td>
      <td>814</td>
      <td>NaN</td>
      <td>...</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>22</th>
      <td>21</td>
      <td>JOUR</td>
      <td>Non-additive gene interactions underpin molecu...</td>
      <td>['Paten, AM', 'Colin, T', 'Coppin, CW', 'Court...</td>
      <td>SCIENCE OF THE TOTAL ENVIRONMENT</td>
      <td>Understanding the cumulative risk of chemical ...</td>
      <td>2022</td>
      <td>10.1016/j.scitotenv.2021.152614</td>
      <td>814</td>
      <td>NaN</td>
      <td>...</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>31</th>
      <td>30</td>
      <td>JOUR</td>
      <td>MALDI-imaging analyses of honeybee brains expo...</td>
      <td>['Catae, AF', 'Menegasso, ARD', 'Pratavieira, ...</td>
      <td>PEST MANAGEMENT SCIENCE</td>
      <td>BACKGROUND Toxicological studies evaluating th...</td>
      <td>2019</td>
      <td>10.1002/ps.5226</td>
      <td>75</td>
      <td>NaN</td>
      <td>...</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>1384</th>
      <td>1037</td>
      <td>JOUR</td>
      <td>Acute oral toxicity, apoptosis, and immune res...</td>
      <td>['Gao, J', 'Guo, Y', 'Chen, J', 'Diao, QY', 'W...</td>
      <td>FRONTIERS IN PHYSIOLOGY</td>
      <td>The potential toxicity of flupyradifurone (FPF...</td>
      <td>2023</td>
      <td>10.3389/fphys.2023.1150340</td>
      <td>14</td>
      <td>NaN</td>
      <td>...</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1392</th>
      <td>1045</td>
      <td>JOUR</td>
      <td>The Effects of Exposure to Flupyradifurone on ...</td>
      <td>['Guo, Y', 'Diao, QY', 'Dai, PL', 'Wang, Q', '...</td>
      <td>INSECTS</td>
      <td>Simple Summary Honey bees play an invaluable r...</td>
      <td>2021</td>
      <td>10.3390/insects12040357</td>
      <td>12</td>
      <td>NaN</td>
      <td>...</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1393</th>
      <td>1045</td>
      <td>JOUR</td>
      <td>The Effects of Exposure to Flupyradifurone on ...</td>
      <td>['Guo, Y', 'Diao, QY', 'Dai, PL', 'Wang, Q', '...</td>
      <td>INSECTS</td>
      <td>Simple Summary Honey bees play an invaluable r...</td>
      <td>2021</td>
      <td>10.3390/insects12040357</td>
      <td>12</td>
      <td>NaN</td>
      <td>...</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1398</th>
      <td>1050</td>
      <td>JOUR</td>
      <td>Honey bee (Apis mellifera) exposomes and dysre...</td>
      <td>['Broadrup, RL', 'Mayack, C', 'Schick, SJ', 'E...</td>
      <td>PLOS ONE</td>
      <td>Honey bee (Apis mellifera) health has been sev...</td>
      <td>2019</td>
      <td>10.1371/journal.pone.0213249</td>
      <td>14</td>
      <td>NaN</td>
      <td>...</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1399</th>
      <td>1050</td>
      <td>JOUR</td>
      <td>Honey bee (Apis mellifera) exposomes and dysre...</td>
      <td>['Broadrup, RL', 'Mayack, C', 'Schick, SJ', 'E...</td>
      <td>PLOS ONE</td>
      <td>Honey bee (Apis mellifera) health has been sev...</td>
      <td>2019</td>
      <td>10.1371/journal.pone.0213249</td>
      <td>14</td>
      <td>NaN</td>
      <td>...</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
<p>572 rows × 24 columns</p>
</div>


    Cleaned dataset saved to: ../output/cleaned_merged_dataset.csv
    


<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>title</th>
      <th>record_id</th>
      <th>type_of_reference</th>
      <th>authors</th>
      <th>secondary_title</th>
      <th>abstract</th>
      <th>year</th>
      <th>doi</th>
      <th>volume</th>
      <th>commu_AB</th>
      <th>...</th>
      <th>letha_ES</th>
      <th>letha_NN</th>
      <th>letha_RP</th>
      <th>molec_AH</th>
      <th>molec_AJ</th>
      <th>molec_EA</th>
      <th>popul_CB</th>
      <th>popul_RP</th>
      <th>subin_RP</th>
      <th>subin_RT</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>4.13 Synergistic effects between variety of in...</td>
      <td>1049</td>
      <td>CONF</td>
      <td>['Raimets, R', 'Mänd, M', 'Cresswell, JE']</td>
      <td>HAZARDS OF PESTICIDES TO BEES</td>
      <td>In recent year's severe decline in honey bees ...</td>
      <td>2018</td>
      <td>10.5073/jka.2018,462.052</td>
      <td>462</td>
      <td>NaN</td>
      <td>...</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>5.1 Large-scale monitoring of effects of cloth...</td>
      <td>365</td>
      <td>CONF</td>
      <td>['Sterk, G', 'Peters, B', 'Gao, ZL', 'Zumkier,...</td>
      <td>HAZARDS OF PESTICIDES TO BEES</td>
      <td>beta-cyfluthrin / kg seed) on the development,...</td>
      <td>2018</td>
      <td>10.5073/jka.2018.462.054</td>
      <td>462</td>
      <td>NaN</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>A Combined LD50 for Agrochemicals and Pathogen...</td>
      <td>20</td>
      <td>JOUR</td>
      <td>['Siviter, H', 'Matthews, AJ', 'Brown, MJF']</td>
      <td>ENVIRONMENTAL ENTOMOLOGY</td>
      <td>Neonicotinoid insecticides are the most common...</td>
      <td>2022</td>
      <td>10.1093/ee/nvab139</td>
      <td>51</td>
      <td>NaN</td>
      <td>...</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
      <td>A Comparison of Pollen and Syrup Exposure Rout...</td>
      <td>564</td>
      <td>JOUR</td>
      <td>['Weitekamp, C.A.', 'Koethe, R.W.', 'Lehmann, ...</td>
      <td>Environmental Entomology</td>
      <td>Bumble bees are important pollinators for both...</td>
      <td>2022</td>
      <td>10.1093/ee/nvac026</td>
      <td>51</td>
      <td>NaN</td>
      <td>...</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4</th>
      <td>A Four-Year Field Program Investigating Long-T...</td>
      <td>963</td>
      <td>JOUR</td>
      <td>['Pilling, E.', 'Campbell, P.', 'Coulson, M.',...</td>
      <td>PLoS ONE</td>
      <td>Neonicotinoid residues in nectar and pollen fr...</td>
      <td>2013</td>
      <td>10.1371/journal.pone.0077193</td>
      <td>8</td>
      <td>NaN</td>
      <td>...</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 24 columns</p>
</div>


Create file with papers that aren't in any domain.


```python
# Step 1: Check for papers that are not included in any of the reviews
# Load the cleaned merged dataset
cleaned_merged_dataset_path = "../output/cleaned_merged_dataset.csv"
cleaned_merged_df = pd.read_csv(cleaned_merged_dataset_path)

# Step 2: Check if any paper is not included in any of the reviews
not_included_df = cleaned_merged_df[cleaned_merged_df.iloc[:, 4:].isnull().all(axis=1)]

# Step 3: Save the dataset with papers that are not included in any of the reviews
not_included_output_path = "../output/not_included_papers.csv"
not_included_df.to_csv(not_included_output_path, index=False)

```
