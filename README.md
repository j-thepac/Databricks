# Databricks
- Managed spark Platform 
- clean Room : Shared spaced for external vendors 
- All catalogs are auto created on AWS eg: Catalog > Settings  > Metastore
  
## Layers 
1. Workspace : Code / Project
2. Catalog : Store Data

## Important :
1. UnityCatalog : Everything under Catalog Explorer Eg: Catalogs, schemas, tables, views
   
## Workspace : 
    1. Complete Workspace
    2. Create : 
        - Folder
        - Git
        - Files
        - Notebook
        - Query
        - Alert
        - Pipeline
        - Dashboard
        - Genie,ML
Catalog : 
Jobs and Pipelines : Notebooks
SQL :
Genie



## Catalog 
    - Unity Catalog = Catalog Explorer
    - Used to Store Data 
    - Unity Catalog contains
        - Catalog :
           - Eg: (Dev , Staging , prod)  or   ( Bronze , Silver , Gold ) or  (Finance , Sales)
           - ```Create Catalog C;
                Use Catalog C;
                create schema C.bronze;
                SELECT * FROM C.schema.T
             ```
            - Catalog can contain : Volumne , Table . Model , Secret , Connection , Service , Skill , Metric View
        - External Location :
        - Volume: 
            - similar to Docker Volume Mapping in Docker or  
        - Secret : 
        - Credential
        - Connection
        - Service 
        - Skill 
        

Data Types
    - Managed : Internal and Managed 
    - External : 
        - Eg : S3
    - External to Managed : 
        - create table T using Delta location 's3://path' as select

## Data Governance :
1. RBAC
2. User --> Group <---- Access
3. Settings > Identity and Access > Add Users , groups 
