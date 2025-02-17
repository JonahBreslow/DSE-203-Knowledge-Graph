# DSE-203-Knowledge-Graph
# Integrating Sunshine Act Data and Physician Prescriptions Data
    1. Lam Ho
    2. Jonah Breslow
    3. Jeffrey Kagan
    
## Motivation:
To investigate the flow of money from drug manufacturers to physicians and how that relates to drug prescriptions. Ultimately, we would like to provide a tool with the capability to identify networks of abuse.

## What this repository contains:
This repository contains jupyter notebooks that process, transform, entity-match, and integrate physician payment data from the Sunshine Act with physician prescription data from Medicare Part D data. Additionally, we utilize an FDA database to gain more information regarding pharmaceutical companies and their respective drugs.

You will see a large swath of jupyter lab notebooks in this repo. Each of these notebooks provides a very specific and modular step within the integration process. The main and most important notebook is called ["Papermill_Workflow.ipynb"](https://github.com/JonahBreslow/DSE-203-Knowledge-Graph/blob/main/Papermill_Workflow.ipynb). This is the most important notebook to run.

Additionally, our PowerPoint presentation of the project is included as well.

## How to use this repository:
1. Clone this repo
2. Find the file called Data.zip.001 at the root of the repository
3. Unzip in place, if your computer prompts you, select the option to add files from zip into existing folders.    
4. Make sure you have all dependencies installed
   - In the future, we will update this repo with the required venv with all dependencies installed
   - Some dependencies you will need:
      - Pandas
      - Numpy
      - Dedupe
      - Papermill
      - Pickle
      - py_stringmatching
      - (probably more)
5. Run the ["Papermill_Workflow.ipynb"](https://github.com/JonahBreslow/DSE-203-Knowledge-Graph/blob/main/Papermill_Workflow.ipynb).
   - **NOTE:** The first cell may take up to 10 hours if the parameter "run_flatten" is changed to True. Keep it false and the following cells are far quicker.
6. This generates output csv files into the *"Nodes"* and *"Edges"* folder. 
7. Copy these files into the *"import"* directory in your Neo4j application.
8. Run the *"Cypher_Load"* script in your Neo4j browser
9. Knowledge graph is created!

## Data 
1. For your information, all sources can be found below
    1. S [CMS Open Payments Data](https://openpaymentsdata.cms.gov/dataset/qsys-b88w)
       - Place this download file in the data folder *'Data/OP_DTL_GNRL_PGYR2019_P06302021.csv'*
    2. Download [Part D Prescriptions Data](https://data.cms.gov/provider-summary-by-type-of-service/medicare-part-d-prescribers/medicare-part-d-prescribers-by-provider-and-drug/data/2019) (**PLEASE NOTE:** pre-filter the data to just CA)
       - Place this download file in the data folder *'Data/Medicare_Part_D_Prescribers_by_Provider_and_Drug_2019.csv'*
    3. Download OpenFDA Data and place them in the folder *'Data/openfda_json'*
       - [openfda_1](https://download.open.fda.gov/drug/label/drug-label-0001-of-0010.json.zip)
       - [openfda_2](https://download.open.fda.gov/drug/label/drug-label-0002-of-0010.json.zip)
       - [openfda_3](https://download.open.fda.gov/drug/label/drug-label-0003-of-0010.json.zip)
       - [openfda_4](https://download.open.fda.gov/drug/label/drug-label-0004-of-0010.json.zip)
       - [openfda_5](https://download.open.fda.gov/drug/label/drug-label-0005-of-0010.json.zip)
       - [openfda_6](https://download.open.fda.gov/drug/label/drug-label-0006-of-0010.json.zip)
       - [openfda_7](https://download.open.fda.gov/drug/label/drug-label-0007-of-0010.json.zip)
       - [openfda_8](https://download.open.fda.gov/drug/label/drug-label-0008-of-0010.json.zip)
       - [openfda_9](https://download.open.fda.gov/drug/label/drug-label-0009-of-0010.json.zip)
       - [openfda_10](https://download.open.fda.gov/drug/label/drug-label-0010-of-0010.json.zip) 

## Presentation
A google presentation of this project can be found [here](https://docs.google.com/presentation/d/1CTyec4oKKbCgzUxYoKQenyqb7slMrhzmdhBv3PKmnYQ/edit#slide=id.g10623ce2b3e_2_283)


## Data Descriptions:

### CMS Open Payments(Sunshine Act)
1. Covers period 2013 to 2020. Covers the whole year in each period
2. 3 Types of Payments:
   - General Payments
   - Research Payments
   - Ownership Payments
3. Each type of sheet includes information:
   - Receiving institution or doctor
   - Purpose of payment
   - Paying insitution or person
4. See [PDF page 22](https://www.cms.gov/OpenPayments/Downloads/OpenPaymentsDataDictionary.pdf) for data dictionary
### Part D Prescriptions
1. Data Methodolgy:
>The Medicare Part D Prescribers by Provider and Drug dataset provides information on prescription drugs prescribed to Medicare beneficiaries enrolled in Part D by physicians and other health care providers. This dataset contains the total number of prescription fills that were dispensed and the total drug cost paid organized by prescribing National Provider Identifier (NPI), drug brand name (if applicable) and drug generic name.
2. Columns:
   - Prescriber Data (Name, NPI, City, State, Specialty)
   - Drug Data (Brand, USAN Generic Name - Short Version)
   - Prescription Data (Number of Medicare Part D Claims, Including Refills, Number of Standardized 30-Day Fills, Including Refills, Number of Day’s Supply for All Claims, Aggregate Cost Paid for All Claims, Aggregate Cost Paid for All Claims, etc.)
3. [Methodology Full Description](https://data.cms.gov/resources/medicare-part-d-prescribers-by-provider-and-drug-data-dictionary)
### Openfda
Data available in OpenFDA. There are more fields, we focused on these:
1. brand_name
2. generic_name
3. manufacturer_name
4. product_ndc
5. product_type	route
6. substance_name
10. is_original_packager
12. pharm_class_epc
13. pharm_class_pe
14. pharm_class_cs
15. pharm_class_moa
![image](https://user-images.githubusercontent.com/56984198/145657807-013b5121-1598-4f85-9e8c-b3a82a42cefd.png)
