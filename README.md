# Databricks
- Managed spark Platform 
- clean Room : Shared spaced for external vendors 
- All catalogs are auto created on AWS eg: Catalog > Settings  > Metastore
- Data can reside in any Cloud Vendor
- .dbc file to import template Eg: Folder Structure , Schema etc.,
- Fivetran connector used to connect to external vendors 
- dbutils.fs.ls(path)
- spark.read.table('catalog.schema.table')
- Project Structure
  - Workspace and Catalog should follow same Folders structure
  - Eg: Sales > ProjectA > (bronze , silver , gold )

## Contents 
- Workspace : Code / Project
- Catalog : Store Data
- Data Ingestion : Connect External Data 
- Auto Loader : Managed Streaming Solution for File Drops
- Data Governance
- Jobs and Pipelines
- SDP / LDP : LakeFlow Declarative Pipelines / Spark Declarative Pipelines 
- DAB : Declarative Bundles (Deployment)
- Databricks SQL (Query )
- Genie (AI)
- LakeFlow Designer /  Visual Prep (ADF)
- Datbricks LakeBase
- Databricks CLI for Calude Code Integration
  
## Activity: Build Medallion Architecture ingesting Data from S3 for project Myproject
### Pre- Req
1. Create AWS account and create S3
2. Create Databricks account
3. Create External Location in Databricks and connect to S3
4. Drop files to S3 loaction for ingestion

### Steps : Use Genie for creation 

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
  
## Catalog 
- Unity Catalog = Everything under Catalog Explorer Eg: Catalogs, schemas, tables, views
- Used to Store Data 
- Contains:
    - Catalog :
       - ```Create Catalog C;
            Use Catalog C;
            create schema C.bronze;
            SELECT * FROM C.schema.T ```
        - Catalog  : Volume , Table (Delta) , Model , Secret , Connection , Service , Skill , Metric View
        - Upload files directly as Delta table
    - External Location : Wizard to Connect to External Vendors for Read and Writing
    - Volume: Similar to Blob Storage
          - Managed : Managed by Databricks
          - External : Managed by External Location
    - Secret : 
    - Credential
    - Connection
    - Service 
    - Skill
      
## Data Ingestion
1. Provide CDC
2. Query Based Capture

## AutoLoader 
1. Spark Structured Stream
2. Used for File drop
3. Needs Checkpoint location (created next to drop location)
4. Create External Location for s3
```
df = (spark.readStream
    .format("cloudFiles")
    .option("cloudFiles.format", "json")
    .option("cloudFiles.schemaLocation", checkpointPath)
    .option("cloudFiles.schemaEvolutionMode", "rescue")
    .load("s3://src")
)

df.writeStream \
    .format("delta") \
    .option("checkpointLocation", checkpointPath) \
    .trigger(processingTime="30 seconds") \
    .start("s3://destination")
```

## Data Governance :
1. RBAC
2. User --> Group <---- Access
3. Settings > Identity and Access > Add Users , groups 

## Jobs and Pipelines 
- Jobs : Pipeline using Notebooks 
- ETL pipleine : LDP 
- Ingestion Pipeline

## Spark Declarative Pipeline (SDP) / LakeFlow Declarative Pipeline (LDP) :
1. Decorators
2. Builtin SCD Types
3. Types: 
    - @pipelines.table : Read Streaming Table
    - @pipelines.materialized_view : Batch processing / Intermittent DF
    - Validations
      - @dp.expect("title", "C IS NOT NULL")
      - @dp.expect_or_drop("coord_exist", "lC IS NOT NULL")
5. Pipeline > ETL pipleine
6. SQL and Pyspark (declarative Syntx)
      ``` SQL
      create or alter materialized View V as
      select * from T
      ```
      
      ```Pyspark
      from pyspark import pipelines
      @pipelines.materialized_view 
      def fn():return spark.read.format("csv") #spark.read.table("fn")
      ```
## Automation  Bundles
- Create a Bundle of Databricks artifacts and Deploy
- Artifacts : Everything except Data 
- Steps:
  - Create Git Repo with default README.md
  - Open Data Bricks > Landing Page> Profile > Settings > Linked Accounts  > Git Integration > Finish Setup
  - Workspace > Create > Git Folder > Paste Git Repo Link
  - Click on "main" button > Create new branch "feature"
  - Click on "main" button > Pull
  - Worspace > Create "Dev_catalog" and "Prod_catalog"
  - Create > Bundle > Default Python > next > Uncheck "Include ETL pipeline" "Include sample.." ,  default "dev" , select personal schema"no" > create only
      - Once created > resource > open "sample_job.yml" > modify as required : name , params  , notebook etc., 
      - Modify ipynb  using Genie Eg: CREATE SCHEMA IF NOT EXISTS and Catalog . 
      - ipynb geneie : Use paramterise catalog and schema to create tables
      - databricks.yml : Notice all lines 1) parameters decalred are used in below env 2)Under Workspaces hard code schema and Catalog for different env
    - COmmit and push
    - Once merge to main . In Databricks sync with main
    - Databricks > BUndle Editor> Deploument> Deploy
    - Goto Pipeline and Jobs > Run the job
      - Once job is run > Catalog > Schema > Table > History and check logs (select compute)  
   
    
## Databricks SQL
- Run Queries quickly
  - Parameterize the Queries
- Contains : Queries , Dashboards

## Genie
1. Types : Inline Code Help and Interactive Agentic AI
2. Add Schdules in Genie
3. Genie can be integrated to Dashboards

## LakeFlow Designer /  Visual Prep  
1. Similar to ADF
2. Data Engineering  >  Visual Prep

##  LakeBase 
- Home > Compute > Lakebase
