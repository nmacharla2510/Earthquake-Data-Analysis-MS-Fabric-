# 🌍 Earthquake – Data Engineering Project
### 1. Project Overview
This project was developed to explore data engineering and analytics pipelines using Microsoft Fabric tools, including Data Factory, Data Engineering, and Power BI.
### 2. Dataset Summary
The data is sourced from the USGS Earthquake API, which provides global earthquake data.
Sample API Query:
https://earthquake.usgs.gov/fdsnws/event/1/query?format=geojson&starttime={start_date}&endtime={end_date}

The response is in GeoJSON format.
### 3. Tools and Technologies Used
•	Python
•	PySpark
•	Microsoft Fabric
•	Data Engineering
•	Data Factory
•	Power BI
### 4. Methodology
The project follows the Medallion Architecture:

![image alt](https://github.com/nmacharla2510/Earthquake-Data-Analysis-MS-Fabric-/blob/main/Medallion%20Architecture.png)
 
#### 🟫 Bronze Layer
•	Fetches JSON data from the USGS API using PySpark.
•	Stores the raw file in the Lakehouse under the Files folder.
•	API parameters (start_date, end_date) are passed as pipeline variables.
#### ⚪ Silver Layer
•	Converts the JSON structure into a tabular format.
•	Extracts relevant fields and saves the DataFrame as a table:
{start_date}_earthquake_silver 
#### 🟨 Gold Layer
•	Uses the reverse_geocoder library to derive country names from latitude and longitude.
•	Saves the enriched DataFrame as:
{start_date}_earthquake_gold 
Note: A separate environment was created for reverse_geocoder.
###5. Pipeline Variables
start_date = @formatDateTime(adddays(utcNow(), -1), 'yyyy-MM-dd') end_date = @formatDateTime(utcNow(), 'yyyy-MM-dd') 
 
### 6. Output Summary
Upon successful pipeline execution:
•	✅ JSON file is saved to the Lakehouse under the Files folder.
•	✅ Two Delta tables are created:
•	earthquake_silver
•	earthquake_gold
 
 
### 7. Power BI Visualization
The Power BI dashboard was built using the Gold Layer output to visualize earthquake data by country and magnitude.
 

