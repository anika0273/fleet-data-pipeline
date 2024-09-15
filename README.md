# Fleet Data Pipeline Project 🚗🔧

## Overview
This project demonstrates my ability to build and manage a data pipeline using PySpark and PostgreSQL, focusing on the analysis of simulated vehicle fleet data. The goal of this project is to showcase my ability to handle large datasets, build scalable data processing systems, and integrate various technologies that are key for modern data engineering tasks.

Even though this project uses a generated dataset, it mirrors real-world scenarios in data processing and highlights my capacity to quickly learn and apply new tools and technologies.

> 🚧 **This project is a work in progress.** I am continually adding features and scaling the pipeline as I learn new technologies like Apache Kafka, Airflow, and more.

## Table of Contents
- [Project Motivation](#project-motivation)
- [Technologies Used](#technologies-used)
- [Project Architecture](#project-architecture)
- [Steps Implemented](#steps-implemented)
- [Next Steps and Future Plans](#next-steps-and-future-plans)
- [How to Run This Project](#how-to-run-this-project)
- [Conclusion](#conclusion)

## Project Motivation
The purpose of this project is to simulate a scenario where we need to process, store, and analyze large amounts of vehicle fleet data in a scalable way. This involves:
- Efficiently processing large datasets.
- Storing processed data in a relational database (PostgreSQL).
- Performing data analysis using PySpark.
- Preparing the pipeline for future scaling and automation.

While the data used here is simulated, the architecture and workflow are designed to mirror real-world data engineering challenges, such as those encountered in companies like Tesla's Self-Driving Data and Analytics team.

## Technologies Used
- **PySpark**: For data processing, filtering, and transformations on large datasets.
- **PostgreSQL**: To store filtered and processed data in a relational database.
- **Psycopg2**: For connecting to PostgreSQL and managing the database using Python.
- **Jupyter Notebook**: For development, code execution, and visualization.
- **Docker**: To manage the environment for PySpark and PostgreSQL.
- **Python**: For data extraction, loading, and general scripting.

## Project Architecture
The architecture for this project consists of the following components:

1. **Data Ingestion**: Simulated fleet data is generated in CSV format and loaded into PySpark for processing.
2. **Data Processing**: PySpark is used to clean, filter, and transform the data.
3. **Data Storage**: The processed data is stored in a PostgreSQL database.
4. **Data Analysis and Visualization**: Analyzed the data using PySpark, focusing on fleet events (e.g., braking, speed, location).
5. **Scaling (Next Steps)**: Future improvements will add automation, scaling, and real-time data processing capabilities.

## Steps Implemented

### 1. Data Ingestion
- **Simulated Dataset**: I used a generated dataset representing vehicle fleet data, containing columns such as `vehicle_id`, `timestamp`, `speed`, `event_type`, etc.
- **Loading into PySpark**: The dataset was loaded into PySpark DataFrame for further processing.

```python
# Loading the dataset into PySpark
fleet_data_spark = spark.read.csv("path/to/fleet_data.csv", header=True, inferSchema=True)
```

### 2. Data Processing
- **Data Cleaning and Filtering**: I filtered the dataset to remove incomplete rows and focused on key events such as braking, collisions, and lane changes.
- **Transformations**: The data was transformed to make it easier for analysis, e.g., converting timestamps and grouping by vehicle events.

```python
# Filtering data for key events
filtered_data_spark = fleet_data_spark.filter(fleet_data_spark["event_type"].isNotNull())
```

### 3. Data Storage
- **PostgreSQL Integration**: The cleaned and filtered data was then written to a PostgreSQL database using the JDBC connector in PySpark.

```python
# Writing the filtered data to PostgreSQL
filtered_data_spark.write \
    .format("jdbc") \
    .option("url", db_url) \
    .option("dbtable", "filtered_fleet_data") \
    .option("user", db_properties['user']) \
    .option("password", db_properties['password']) \
    .option("driver", db_properties['driver']) \
    .save()
```

### 4. Data Analysis and Visualization
- **Exploratory Analysis**: I used PySpark to perform exploratory analysis on the filtered fleet data, such as counting events by vehicle and analyzing speed distributions.
- **Visualization**: For visualizing the results, I am in the process of converting the data into pandas DataFrames and using Python libraries such as `matplotlib` and `seaborn`.

```python
# Analyzing the event types
event_type_counts = filtered_data_spark.groupBy("event_type").count()
event_type_counts.show()
```

## Next Steps and Future Plans

### 1. **Automation and Scaling**
   - **Automation with Apache Airflow**: I plan to automate the entire pipeline by setting up scheduled jobs with Airflow. This will allow the pipeline to run on a daily or weekly basis, ensuring continuous data processing and analysis.
   - **Handling Larger Datasets**: To make the pipeline scalable, I will implement optimizations such as partitioning and bucketing the data, as well as handling larger datasets in a distributed manner with Spark.

### 2. **Real-Time Streaming**
   - **Apache Kafka**: In the future, I plan to incorporate real-time data streaming by integrating Apache Kafka. This would allow the system to process real-time fleet data, a feature critical to industries like autonomous driving and fleet management.

### 3. **Improved Analysis and Visualizations**
   - **Data Visualization**: More advanced visualizations will be implemented using Python’s visualization libraries like `plotly` and `seaborn`.
   - **Machine Learning**: I am planning to add predictive analytics by training a machine learning model to predict vehicle failures or risky events based on the collected data.

## How to Run This Project

### 1. Clone the Repository
```bash
git clone https://github.com/yourusername/fleet-data-pipeline.git
cd fleet-data-pipeline
```

### 2. Set up Docker for PySpark and PostgreSQL
You’ll need Docker to create an environment for PySpark and PostgreSQL.

```bash
docker-compose up -d
```

### 3. Run the PySpark Job
Once Docker is up, you can run the PySpark job to process the data and load it into PostgreSQL.

```bash
spark-submit --jars /path/to/postgresql-jdbc.jar your_script.py
```

### 4. Query PostgreSQL
You can now query the processed data in PostgreSQL using any SQL client or via Python with `psycopg2`.

## Conclusion

This project demonstrates my ability to build a full data pipeline using PySpark, PostgreSQL, and Docker. It mirrors real-world data engineering scenarios and showcases my ability to adapt to new technologies.

> **Note**: This project is part of my ongoing learning process. As I continue to grow my skills in data engineering, I will update this project with new features such as real-time streaming and automation. Stay tuned for updates!