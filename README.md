# Big-Data-CaseStudy
Click Stream Web Analytics Using Hadoop, Hive and PySpark


# Purpose:

Generate various analytics for web users through click stream web data. On a web site, click stream analysis is the process of collecting, analysing, and reporting aggregate data about which pages visitors visit (navigation data from login to logout)

# Inputs:

The input would be the click stream data generated by java tool in the JSON format. Number of records should be at least 1 Lakh.

# Steps:

· The data can be generated through a Java program that generates data in JSON format in a file.

· The above raw data would be stored in Hive and partitioned and bucketed on appropriate data fields.

· Hive should use MySQL Meta store.

· Perform analysis on the data stored in Hive tables, the analysis jobs should have at least one hive, one MR job and one spark job.

· Schedule the process of data generation, archiving older data and running analysis jobs, through any appropriate mechanism (Cron job, Oozie work flow, Spring batch etc.).

· Store the results of analysis jobs in Hive tables.

· Visualise the analytical results (read from Hive and show data in excel or any other visulization tool)

# Analytics:

· Generate following analytics/reports using above data:

· Most active users.

· Location wise traffic analysis

· Day wise traffic analysis

# Ecommerce Analytics

· User item visit analysis.

· Users purchase/shopping cart analysis.

· Perform other appropriate ecommerce analytics base on the data.

# Deliverables

· Design document with architecture and table details:

· Case study presentation:

· Code Artifacts:

· Output report:

# Schema

The data generation schema

· userID – Unique id of the user

· url -- to keep track of user activity

· action (optional)-- to keep track of action performed while performing the cart activity

Can be covered as part of url or

Possible actions : view , addtocart , removefromcart , purchase etc location – to keep track of the location of the user

· logTime – to keep track of the time when the user logged in

· payment_method – to keep track of the payment method opted by user

· logDate – to keep track of the date when the user logged in

· sessionId – Session id of user

For e.g.
```json
{

"userID":"Marvin Eriksen Sr.",

"location":"Virginia",

"sessionId":"Session_clickShop15970860614820",

"url":"http://www.shop.com/purchased/item?Small Bronze Chair",

"logTime":"2020-08-11 00:31:01.485",

"payment_method":"Credit Card",

"logDate":"2020-08-11"

} 
```
# Solution

Required Setup
Install Java, Hadoop and Integrated with Hive, Spark and Zeppelin (Visualization Tool Same As Jupiter Notebook) 

# Step 1: Create Java Program To Generate JSON Data
i have created [<b>"Generate_Ecommerce_JsonData_Proj"</b>](https://github.com/kiranugalmugale15/Big-Data-CaseStudy/tree/main/Generate_Ecommerce_JsonData_Proj) java maven project

it is generating data using [<b>"GeneratorEcommerceData"</b>](https://github.com/kiranugalmugale15/Big-Data-CaseStudy/blob/main/Generate_Ecommerce_JsonData_Proj/src/main/java/GeneratorEcommerceData.java) class 

which is using external jar dependancy added in [<b>"pom.xml"</b>](https://github.com/kiranugalmugale15/Big-Data-CaseStudy/blob/main/Generate_Ecommerce_JsonData_Proj/pom.xml)
1. <b>"JavaFaker"</b> class to generate random names,address,city,app name for me
2. <b>"Gson"</b> for converting my ecommerce object data into json

also i have created jar [<b>"TestProject-0.0.1-SNAPSHOT-jar-with-dependencies.jar"</b>](https://github.com/kiranugalmugale15/Big-Data-CaseStudy/tree/main/Generate_Ecommerce_JsonData_Proj/target)

# Step 2: Create Map-Reduce Java Program To Count No. Of User
i have created [<b>"UserCount_MapReduce_Proj"</b>]([https://github.com/kiranugalmugale15/Big-Data-CaseStudy/tree/main/Generate_Ecommerce_JsonData_Proj](https://github.com/kiranugalmugale15/Big-Data-CaseStudy/tree/main/UserCount_MapReduce_Proj)) simple java project

which has three class 
1. [<b>"RecordCountDriver.java"</b>](https://github.com/kiranugalmugale15/Big-Data-CaseStudy/blob/main/UserCount_MapReduce_Proj/RecordCountDriver.java) Responsible For Running Mapreduce Program
2. [<b>"RecordCountMapper.java"</b>](https://github.com/kiranugalmugale15/Big-Data-CaseStudy/blob/main/UserCount_MapReduce_Proj/RecordCountMapper.java) Mapping Each Record With One Value
3. [<b>"RecordCountReducer.java"</b>](https://github.com/kiranugalmugale15/Big-Data-CaseStudy/blob/main/UserCount_MapReduce_Proj/RecordCountReducer.java) Counting All Records

also i have created jar [<b>"activeUserCountMR.jar"</b>](https://github.com/kiranugalmugale15/Big-Data-CaseStudy/tree/main/UserCount_MapReduce_Proj)

# Step 3: Doing Analysis On Input JSON File Using Zeppelin
1. [<b>"HiveAnalysisZeppelin.zpln"</b>](https://github.com/kiranugalmugale15/Big-Data-CaseStudy/blob/main/ZeppelinNotBooks/HiveAnalysisZeppelin.zpln) Responsible For Hive Analysis
2. [<b>"SparkAnalysisZeppelin.zpln"</b>](https://github.com/kiranugalmugale15/Big-Data-CaseStudy/blob/main/ZeppelinNotBooks/SparkAnalysisZeppelin.zpln) For Spark Analysis

# Step 4: Create CronJob If You Want To do Run all this Step Automatically
please have look at [<b>"schedule_analysis_script.sh"</b>](https://github.com/kiranugalmugale15/Big-Data-CaseStudy/edit/main/CronJob%20Script/schedule_analysis_script.sh)

