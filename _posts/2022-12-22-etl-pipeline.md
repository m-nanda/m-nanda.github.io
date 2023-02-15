---
layout: post
title:  "ETL Pipeline"
date:   2022-12-22
excerpt: "Implemented an ETL pipeline for extracting real-time bitcoin data from API and additional exchange rate conversion data from Google Finance. Utilized Python, Airflow, Docker, and PostgreSQL to process, store and analyze the data. Carried out parallel data extraction, transformation and loading stages, with considerations for data security and optimized memory usage. The result is a data-driven solution that can be used by stakeholders and bitcoin analysts to monitor, analyze, and predict bitcoin prices."
project: true
tag:
- ETL
- Data Pipeline
- Airflow
- Python
- Data Engineering
- Docker
- Batching Method
- Scraping
- PostgreSQL
comments: true
---

# Project Overview

This is an ETL pipeline project with the batching method for collecting and processing real-time bitcoin data and exchange rate conversion data. The main data source is API for real-time bitcoin data from coindesk. The secondary data source is exchage rate that scraped from Google Finance.

# Technologies

* **Python** (main programming language)
  Key Libraries: 
  * `urlopen` and `json` (for API data extraction)
  * `bs4` and `regex` (for scraping Google Finance )
* **Airflow** & **Docker** (ETL development and monitoring)
* **PostgreSQL** (database)

# Workflow
* **Development**
	1. Bottom-Up approach.
    create functions and files and then put them together.
	2. Create database.
    ![Database Architecture in PostgreSQL](https://github.com/m-nanda/ETL-Pipeline/raw/main/img/table_postgres.png "Database Architecture in PostgreSQL")  
	3. Configure dump directory.
    the prevent file conflicts during processing and also to save memory (there are also cost considerations when using a paid service).
    ![Dump Directory](https://github.com/m-nanda/ETL-Pipeline/raw/main/img/dump_dir.png "Dump Directory")
  4. Build pipeline.
      ```python
      with DAG(dag_id='api_source_etl', default_args=default_args,
          schedule_interval='@hourly', catchup=False) as dag:

      dir_prep = PythonOperator(
          task_id='prepare_dump_directory',
          python_callable=dir_preparation
      )
      extract_1 = PythonOperator(
          task_id='extract_api_data',
          python_callable=extract_coindesk
      )
      extract_2 = PythonOperator(
          task_id='scraping_data',
          python_callable=scrape_google_finance
      )
      transform = PythonOperator(
          task_id='transform_data',
          python_callable=transform,
      )
      load = PythonOperator(
          task_id='load_data',
          python_callable=load,
      )
      
      # pipeline
      dir_prep >> [extract_1, extract_2] >> transform >> load
      ```
	5. Build connection to database.

* **Production**
	1. Credential management.  
    PostgreSQL access protected via environment variables.
        ```python
        # get credentials
        USER = os.getenv('PROD_USER') 
        PASS = os.getenv('PROD_PASS') 
        HOST = os.getenv('PROD_HOST') 
        PORT = os.getenv('PROD_PORT') 
        DB = os.getenv('PROD_DB') 
        TABLE = os.getenv('PROD_TABLE') 

        # create connection
        conn = psycopg2.connect(
                    database=DB, 
                    user=USER, 
                    password=PASS, 
                    host=HOST, 
                    port=PORT
                )
        ```
	2. Running pipeline.
    Pipeline created with 4 steps as follows:    
    ![Pipeline Graph](https://github.com/m-nanda/ETL-Pipeline/raw/main/img/pipeline_graph.png "Pipeline Graph")
* **Maintain**
	1. Monitoring pipeline
    ![Monitoring Pipeline in Airflow](https://github.com/m-nanda/ETL-Pipeline/raw/main/img/airflow.png "Monitoring Pipeline in Airflow")
	2. Monitoring result in database
    ![Loaded Data in PostgreSQL](https://github.com/m-nanda/ETL-Pipeline/raw/main/img/loaded_data_result.png "Loaded Data in PostgreSQL")

# Future Improvement

* Adding additional bitcoin data sources.
* Moving to cloud-based data warehouse technology.
* Creating dashboards and reports.

# Conclusion

This project can provide data that have valuable insights for stakeholders and bitcoin analysts to monitor, analyze, and predict bitcoin prices through the use of real-time data and exchange rate conversion information.  

[`Go to repo >>`](https://github.com/m-nanda/ETL-Pipeline)  