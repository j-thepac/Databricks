# Databricks
- Managed spark Platform 
- clean Room : Shared spaced for external vendors 
- All catalogs are auto created on AWS eg: Catalog > Settings  > Metastore
- Data can reside in any Cloud Vendor
- .dbc file to import template Eg: Folder Structure , Schema etc.,
- Fivetran connector used to connect to external vendors 
- dbutils.help()
  
## Important 
- Workspace : Code / Project
- Catalog : Store Data
- Data Ingestion : Connect External Data 
- Auto Loader : Managed Streaming Solution for File Drops
- Data Governance
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
       - Eg: (Dev , Staging , prod)  or   ( Bronze , Silver , Gold ) or  (Finance , Sales)
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
