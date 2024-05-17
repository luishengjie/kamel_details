# Repository to generate MIMIC-IV-ICD-10-N3 dataset

This respository contains the steps to generate the MIMIC-IV-ICD-10-N3 dataset used in this paper [KAMEL: Knowledge Aware Medical Entity Linkage to Automate Health Insurance Claims Processing](https://ojs.aaai.org/index.php/AAAI/article/view/30314). To cite the original article:

```
@article{Lui_Xiang_Krishnaswamy_2024, 
title={KAMEL: Knowledge Aware Medical Entity Linkage to Automate Health Insurance Claims Processing}, 
volume={38}, 
url={https://ojs.aaai.org/index.php/AAAI/article/view/30314}, 
DOI={10.1609/aaai.v38i21.30314}, 
number={21}, 
journal={Proceedings of the AAAI Conference on Artificial Intelligence}, author={Lui, Sheng Jie and Xiang, Cheng and Krishnaswamy, Shonali}, year={2024}, month={Mar.}, 
pages={22797-22805} }
```

The MIMIC-IV files can be obtained from [this website](https://physionet.org/content/mimiciv/2.2/). You can download it to the directory `mimicdata/physionet.org`


## Steps to generate MIMIC-IV-ICD-10-N3 dataset
The original script used to generate the MIMIC-IV-ICD-10-N3 dataset uses Python 3.11. We set all random seeds to `2023`.

1. Download the [MIMIC-IV dataset](https://physionet.org/content/mimiciv/2.2/).
2. Load `diagnoses_icd.csv.gz` as a pandas DataFrame: 
    * Apply the filter `icd_version==10`
    * Perform a [groupby](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.groupby.html) on `subject_id` and `hadm_id`, then aggregate the icd_code into lists.
3. Load `discharge.csv.gz` as a pandas DataFrame: 
4. Merge (inner join) the grouped dataframe from step 2 with discharge summary from step 3.
5. Generate Negative Samples:
    * Randomly select one-third of the rows from the dataframe generated in step 4.
    * For each selected row, generate dummy ICD codes that do not belong in the same chapter as the original ICD code.
6. Concatenate dataframes generated from step 4 and 5 to obtain the complete dataset.
7. Obtain the train and test dataset by performing a [random split](https://scikit-learn.org/stable/modules/generated/sklearn.model_selection.train_test_split.html) where `test_size=0.3`.




