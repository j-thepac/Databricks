# Databricks

## Layers 
1. Workspace : Code / Project
2. Catalog : Data 

## Workspace : 
    1. Complete Workspace
    2. Create : Folder,Git,Files,Notebook,Query,Alert,Pipeline,Dashboard,Genie,ML
Catalog : 
Jobs and Pipelines : Notebooks
SQL :
Genie

## Data Governance :
    1. RBAC
    2. User --> Group <---- Access
    3. Settings > Identity and Access > Add Users , groups 

## Catalog (LakeHouse)
    Databricks has 1 lakehouse like structure and has multiple schemas under it called catalogs .  
    1. Store Data
    2. Eg: Dev , Staging , prod  /  Bronze , Silve , Gold /  Finance , Sales 
    3. UnityCatalog : Everything under Catalog Exlorer is UNity Catalog Eg: Catalogs, schemas, tables, views
    7. SELECT * FROM prod.gold.sales_summary;
    8. Create > Catalog , External Location , Volume , Secret , credential , Connection , Service , Skill
Create Catalog Sales;
Use Catalog Sales;
create schema C.bronze;
create schema C.silver;
create schema C.gold;
         

Data Types
    - Managed : Internal and Managed 
    - External : 
        - Eg : S3
    - External to Managed : 
        - create table T using Delta location 's3://path' as select

Volumes : 
