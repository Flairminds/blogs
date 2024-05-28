---
title: How to Set Up Grafana Documentation A Simple Guide
date: 2024-05-27
authors: [shreeyashs]
slug: grafana_documentation_setup_guide
description: >
  Learn how to efficiently set up Grafana documentation with this step-by-step guide.
categories:
  - Grafana
tags:
  - Grafana
  - Data Visualization
  - Dashboards
  - Athena
  - Documentation
comments: true
---

# How to Set Up Grafana Documentation: A Simple Guide for You

## Introduction:
Are you looking to document your Grafana setup or share your dashboard configurations effortlessly? Grafana offers robust features for visualization and dashboard management, and with proper documentation, you can make your workflows more efficient and reproducible. This guide will walk you through the essential steps to create and manage your Grafana documentation.

<!-- more -->

## 1. Create New Visualizations in Grafana

Creating new visualizations in Grafana is straightforward and powerful. Here's how you can get started:

1. **Open Grafana and select a dashboard**: Start by opening your Grafana instance and selecting the dashboard where you want to create a new visualization.
2. **Add a new panel**: Click on the 'Add panel' button and choose 'Add new panel'.
3. **Choose a visualization type**: Select from various visualization options like Graph, Singlestat, Table, etc.
4. **Configure the panel**: Set your data source, write your queries, and customize the visualization settings to fit your needs.
5. **Save the panel**: Once you're satisfied with the configuration, click 'Apply' to save the panel to your dashboard.

## 2. Dashboard Query Explanation

Understanding and documenting your queries is crucial for maintaining and sharing your dashboards. Here's a breakdown of how to explain your dashboard queries:

1. **Describe the purpose**: Start with a brief description of what the query aims to achieve.
2. **Show the query**: Include the exact query used in the panel. Use code blocks for clarity.
3. **Explain each part**: Break down the query into parts and explain each component. This can include the metrics, filters, and functions used.
4. **Provide examples**: Where applicable, include examples of the query results and how they impact the visualization.

## 3. Create Database in Athena

Integrating Grafana with Amazon Athena allows you to query large datasets stored in S3. Here's how to set up a database in Athena:

1. **Access Athena**: Log in to the AWS Management Console and open the Athena service.
2. **Create a database**: Run the following SQL command to create a new database:
   CREATE DATABASE my_database;
3. **Define table schema**: Use the CREATE TABLE statement to define the schema for your data.
4. **Query your data**: Once the database and tables are set up, you can start querying your data using SQL.

## 4. Import and Export Grafana Dashboards

Managing dashboards involves importing and exporting them for backup or sharing. Here’s how you can do it:

### Importing a Dashboard

1. **Open dashboard settings**: Navigate to the dashboard settings and click on the 'Import' button.
2. **Upload JSON file**: Select the JSON file containing the dashboard configuration.
3. **Configure settings**: Adjust any settings if necessary, such as the data source mappings.
4. **Save the dashboard**: Click 'Import' to add the dashboard to your Grafana instance.

### Exporting a Dashboard

1. **Go to the dashboard**: Open the dashboard you want to export.
2. **Access the share menu**: Click on the share icon (usually a paper plane) and select 'Export'.
3. **Save as JSON**: Choose the 'Save as JSON' option to download the dashboard configuration file.

# Grafana Panel Editor Overview

## Adding a Panel
- **New Dashboard**: Click `+ Add visualization` in the middle of the dashboard.

[Material Metrics Picture1]:Grafana_setup/Picture1.png
![Material Metrics Picture1][Material Metrics Picture1]

- **Existing Dashboard**: Click `Add` in the dashboard header and select `Visualization` from the drop-down.

[Material Metrics Picture2]:Grafana_setup/Picture2.png
![Material Metrics Picture2][Material Metrics Picture2]

## Panel Menu
Access the panel editor by hovering over the top-right corner of any panel. Click the panel menu icon that appears and select `Edit`.

### Panel Menu Options
- **View**: View the panel in full screen.
- **Edit**: Open the panel editor to edit panel and visualization options.
- **Share**: Share the panel as a link, embed, or library panel.
- **Explore**: Open the panel in Explore mode to focus on your query.
- **Inspect**: Open the Inspect drawer to review panel data, stats, metadata, JSON, and query.
  - **Data**: Open the Inspect drawer in the Data tab.
  - **Query**: Open the Inspect drawer in the Query tab.
  - **Panel JSON**: Open the Inspect drawer in the JSON tab.
- **More**: Access other panel actions.
  - **Duplicate**: Make a copy of the panel.
  - **Copy**: Copy the panel to the clipboard.
  - **Create library panel**: Create a panel that can be imported into other dashboards.
  - **Create alert**: Open the alert rule configuration page in Alerting.
  - **Hide legend**: Hide the panel legend.
  - **Get help**: Send a snapshot or panel data to Grafana Labs Technical Support.
- **Remove**: Remove the panel from the dashboard.

[Material Metrics Picture3]:Grafana_setup/Picture3.png
![Material Metrics Picture3][Material Metrics Picture3]

## Panel Editor

### Visualization Preview
- **Table view**: Convert any visualization to a table to see the raw data.
- **Fill**: The visualization preview fills the available space.
- **Actual**: The visualization preview matches the exact size on the dashboard.
- **Time range controls**: Default is either the browser local timezone or the timezone selected at a higher level.

[Material Metrics Picture5]:Grafana_setup/Picture5.png
![Material Metrics Picture5][Material Metrics Picture5]

## Data Section
Contains tabs for entering queries, transforming data, and creating alert rules (if applicable).

- **Query tab**: Select your data source and enter queries here. 
- **Transform tab**: Apply data transformations.
- **Alert tab**: Write alert rules.

[Material Metrics Picture6]:Grafana_setup/Picture6.png
![Material Metrics Picture6][Material Metrics Picture6]

## About Queries
Grafana panels communicate with data sources via queries.

- **Region**: The geographical location of your data source.
- **Data Source**: Connection to your database service.
- **Database**: The specific database within your data source.
- **Table**: Tables within the selected database for querying.
- **Column**: Columns within the tables for data retrieval.
- **Enable**: Toggle to activate or deactivate certain features.
- **TTL (mins)**: Time-to-Live for cached data in minutes.
- **Frames**: Individual data sets returned by your queries.
- **Format as**: Specify the output format for the query results.
- **+ Add query**: Add additional queries for comparison or analysis.
- **+ Expression**: Define custom expressions or calculations on query results.

## Panel Options
- **Title**: Set a title for the panel.
- **Description**: Include a description for the panel.
- **Transparent background**: Set the background of the panel as transparent.
- **Panel links**: Link to other panels or external URLs.
- **Repeat options**: Repeat or clone certain settings or elements within the panel.

[Material Metrics Picture7]:Grafana_setup/Picture7.png
![Material Metrics Picture7][Material Metrics Picture7]

## Value Options
- **Show**: Control the visibility of certain elements.
- **Calculation**: Perform calculations on values displayed in the panel.
- **Fields**: Select specific data fields to display or calculate.

[Material Metrics Picture8]:Grafana_setup/Picture8.png
![Material Metrics Picture8][Material Metrics Picture8]

## Gauge
- **Orientation**: Set the orientation of the gauge.
- **Show threshold labels**: Display labels for threshold values.
- **Show threshold markers**: Display markers for threshold values.

[Material Metrics Picture9]:Grafana_setup/Picture9.png
![Material Metrics Picture9][Material Metrics Picture9]

## Text Size
- **Title**: Adjust the size of the title text.
- **Value**: Adjust the size of the value text.

[Material Metrics Picture10]:Grafana_setup/Picture10.png
![Material Metrics Picture10][Material Metrics Picture10]

## Standard Options
- **Unit**: Specify the unit for displayed values.
- **Min**: Set the minimum value on the scale.
- **Max**: Set the maximum value on the scale.
- **Field min/max**: Use the minimum and maximum values from the data fields.
- **Decimals**: Control the number of decimal places displayed.
- **Display name**: Set a custom display name for the panel.
- **No value**: Handle cases where there is no data or value available.

[Material Metrics Picture11]:Grafana_setup/Picture11.png
![Material Metrics Picture11][Material Metrics Picture11]

## Data Links
- **Add link**: Add links to related data or information.

[Material Metrics Picture12]:Grafana_setup/Picture12.png
![Material Metrics Picture12][Material Metrics Picture12]

## Value Mappings
- **Add value mappings**: Map specific values to custom representations or labels.

## Thresholds
- **Thresholds mode**: Set the mode for defining and handling threshold values.

## Creating a Table

[Material Metrics Picture13]:Grafana_setup/Picture13.png
![Material Metrics Picture13][Material Metrics Picture13]

- **Table Schema**: Defines the structure of the table with columns such as time, type, elb, client_ip, client_port, etc.
- **Partitioning**: Partitions the data by the day column to improve query performance.
- **SerDe**: Specifies the Serializer/Deserializer for interpreting the log data.
- **SerDe Properties**: Defines properties for the SerDe, including the serialization format and regex pattern.
- **Location**: Specifies the S3 bucket location where the log files are stored.
- **Table Properties**: Includes properties for the table, such as enabling column projections and defining the partitioning strategy.

# Grafana Dashboard Query Explanation

## Total Request
Counts the total number of requests hitting an Application Load Balancer (ALB).

**Graph:**

[Material Metrics Picture14]:Grafana_setup/Picture14.png
![Material Metrics Picture14][Material Metrics Picture14]

**Query:**

[Material Metrics Picture15]:Grafana_setup/Picture15.png
![Material Metrics Picture15][Material Metrics Picture15]

**Description:**
This Athena query retrieves the total number of requests from an Application Load Balancer (ALB) access log table named `alb_access_logs_v1`.

**Functionality:**
- Retrieves the count of all requests from ALB access logs within a specified time range.

## Total Failed Request
Counts the number of failed requests hitting an Application Load Balancer (ALB).

**Graph:**

[Material Metrics Picture16]:Grafana_setup/Picture16.png
![Material Metrics Picture16][Material Metrics Picture16]

**Query:**

[Material Metrics Picture17]:Grafana_setup/Picture17.png
![Material Metrics Picture17][Material Metrics Picture17]

**Description:**
This Athena query retrieves the total number of failed requests from an Application Load Balancer (ALB) access log table named `alb_access_logs_v1`.

**Functionality:**
- Retrieves the count of rows from ALB access logs where the ELB status code is not equal to 200, indicating failed requests.

## Average Total Processing Time
Calculates the average overall response time for successful requests hitting an Application Load Balancer (ALB).

**Graph:**

[Material Metrics Picture18]:Grafana_setup/Picture18.png
![Material Metrics Picture18][Material Metrics Picture18]

**Query:**

[Material Metrics Picture19]:Grafana_setup/Picture19.png
![Material Metrics Picture19][Material Metrics Picture19]

**Description:**
This Athena query retrieves the average overall response time for successful requests from an ALB access log table named `alb_access_logs_v1`.

**Functionality:**
- Computes the average of the sum of request processing time, target processing time, and response processing time for successful requests (ELB status code = 200) within a specified time range.

## Average Target Processing Time
Calculates the average target processing time for successful requests hitting an Application Load Balancer (ALB).

**Graph:**

[Material Metrics Picture20]:Grafana_setup/Picture20.png
![Material Metrics Picture20][Material Metrics Picture20]

**Query:**

[Material Metrics Picture21]:Grafana_setup/Picture21.png
![Material Metrics Picture21][Material Metrics Picture21]

**Description:**
This Athena query retrieves the average target processing time for successful requests from an ALB access log table named `alb_access_logs_v1`.

**Functionality:**
- Calculates the average target processing time for successful requests (ELB status code = 200) within a specified time range.

## Unique Visitor
Counts the number of unique visitors accessing an Application Load Balancer (ALB) within a specified time range.

**Graph:**

[Material Metrics Picture22]:Grafana_setup/Picture22.png
![Material Metrics Picture22][Material Metrics Picture22]

**Query:**

[Material Metrics Picture23]:Grafana_setup/Picture23.png
![Material Metrics Picture23][Material Metrics Picture23]

**Description:**
This Athena query retrieves the number of unique visitors accessing an ALB within a specified time range from an access log table named `alb_access_logs_v1`.

**Functionality:**
- Identifies unique visitors by counting the distinct client IP addresses present in the ALB access logs.

## Total Valid Requests
Counts the total number of successful requests hitting an Application Load Balancer (ALB) within a specified time range.

**Graph:**

[Material Metrics Picture24]:Grafana_setup/Picture24.png
![Material Metrics Picture24][Material Metrics Picture24]

**Query:**

[Material Metrics Picture25]:Grafana_setup/Picture25.png
![Material Metrics Picture25][Material Metrics Picture25]

**Description:**
This Athena query retrieves the total number of successful requests from an ALB access log table named `alb_access_logs_v1`.

**Functionality:**
- Determines the count of rows where the ELB status code is 200, indicating successful requests.

## Total Sent Data In MB
Calculates the total amount of data sent, in megabytes, by an Application Load Balancer (ALB) within a specified time range.

**Graph:**

[Material Metrics Picture26]:Grafana_setup/Picture26.png
![Material Metrics Picture26][Material Metrics Picture26]

**Query:**

[Material Metrics Picture27]:Grafana_setup/Picture27.png
![Material Metrics Picture27][Material Metrics Picture27]

**Description:**
This Athena query retrieves the total amount of data sent, in megabytes, by an ALB within a specified time range from an access log table named `alb_access_logs_v1`.

**Functionality:**
- Adds up the `sent_bytes` column values and converts the total to megabytes.

## Total Received Data In MB
Calculates the total amount of data received, in megabytes, by an Application Load Balancer (ALB) within a specified time range.

**Graph:**

[Material Metrics Picture28]:Grafana_setup/Picture28.png
![Material Metrics Picture28][Material Metrics Picture28]

**Query:**

[Material Metrics Picture29]:Grafana_setup/Picture29.png
![Material Metrics Picture29][Material Metrics Picture29]

**Description:**
This Athena query retrieves the total amount of data received, in megabytes, by an ALB within a specified time range from an access log table named `alb_access_logs_v1`.

**Functionality:**
- Adds up the `received_bytes` column values and converts the total to megabytes.

## Total Request Count By Hour
Counts the number of requests hitting an Application Load Balancer (ALB) per hour within a specified time range.

**Graph:**

[Material Metrics Picture30]:Grafana_setup/Picture30.png
![Material Metrics Picture30][Material Metrics Picture30]

**Query:**

[Material Metrics Picture31]:Grafana_setup/Picture31.png
![Material Metrics Picture31][Material Metrics Picture31]

**Description:**
This Athena query retrieves the total number of successful requests from an ALB within a specified time range from an access log table named `alb_access_logs_v1`.

**Functionality:**
- Groups the requests by hour and counts them, providing a breakdown of request counts for each hour.

## Hyperlink

[Material Metrics Picture32]:Grafana_setup/Picture32.png
![Material Metrics Picture32][Material Metrics Picture32]

We have added hyperlinks from Panel Option -> Panel Links.

[Material Metrics Picture33]:Grafana_setup/Picture33.png
![Material Metrics Picture33][Material Metrics Picture33]

**URL:**
[http://13.126.47.32:3000/d/ddj4et2jglywwb/prd-ptg-elb-sub?orgId=1&from=${__from}&to=${__to}&viewPanel=9](http://13.126.47.32:3000/d/ddj4et2jglywwb/prd-ptg-elb-sub?orgId=1&from=${__from}&to=${__to}&viewPanel=9)

- We've added `from` and `to` parameters to explicitly pass the `from_date` and `to_date` values to the target dashboard or visualization.
- Ensure that the variables `from` and `to` capture the correct date range from the source panel.

  [Material Metrics Picture34]:Grafana_setup/Picture34.png
  ![Material Metrics Picture34][Material Metrics Picture34]

- After opening the hyperlink, it shows the minutes graph.

## Total Failed Request Count By Hour
Counts the number of failed requests hitting an Application Load Balancer (ALB) per hour within a specified time range.

**Graph:**

[Material Metrics Picture35]:Grafana_setup/Picture35.png
![Material Metrics Picture35][Material Metrics Picture35]

**Query:**

[Material Metrics Picture36]:Grafana_setup/Picture36.png
![Material Metrics Picture36][Material Metrics Picture36]

**Description:**
This Athena query retrieves the number of failed requests from an ALB per hour within a specified time range from an access log table named `alb_access_logs_v1`.

**Functionality:**
- Groups the failed requests by hour and counts them, providing a breakdown of failed request counts for each hour.

## Hyperlink

[Material Metrics Picture37]:Grafana_setup/Picture37.png
![Material Metrics Picture37][Material Metrics Picture37]

We have added hyperlinks from Panel Option -> Panel Links.

[Material Metrics Picture38]:Grafana_setup/Picture38.png
![Material Metrics Picture38][Material Metrics Picture38]

**URL:**
[http://13.126.47.32:3000/d/ddj4et2jglywwb/prd-ptg-elb-sub?orgId=1&from=${__from}&to=${__to}&viewPanel=10](http://13.126.47.32:3000/d/ddj4et2jglywwb/prd-ptg-elb-sub?orgId=1&from=${__from}&to=${__to}&viewPanel=10)

- We've added `from` and `to` parameters to explicitly pass the `from_date` and `to_date` values to the target dashboard or visualization.
- Ensure that the variables `from` and `to` capture the correct date range from the source panel.

  [Material Metrics Picture39]:Grafana_setup/Picture39.png
  ![Material Metrics Picture39][Material Metrics Picture39]

- After opening the hyperlink, it shows the minutes graph.

## Top 5 Most Visited Client IP
Identifies the top 5 IP addresses with the highest number of requests hitting an Application Load Balancer (ALB) within a specified time range.

**Graph:**

[Material Metrics Picture40]:Grafana_setup/Picture40.png
![Material Metrics Picture40][Material Metrics Picture40]

**Queries:**

[Material Metrics Picture41]:Grafana_setup/Picture41.png
![Material Metrics Picture41][Material Metrics Picture41]

**Description:**
This Athena query retrieves the top 5 IP addresses with the highest number of requests from an ALB access log table named `alb_access_logs_v1`.

**Functionality:**
- Groups requests by client IP address, counts them, sorts the results in descending order based on the request count, and limits the output to the top 5 IP addresses.

## Top 10 Failed Request By Client IP
Provides a breakdown of request counts, 4xx errors, and 5xx errors for the top 10 client IP addresses accessing an Application Load Balancer (ALB) within a specified time range.

**Graph:**

[Material Metrics Picture42]:Grafana_setup/Picture42.png
![Material Metrics Picture42][Material Metrics Picture42]

**Queries:**

[Material Metrics Picture43]:Grafana_setup/Picture43.png
![Material Metrics Picture43][Material Metrics Picture43]

[Material Metrics Picture44]:Grafana_setup/Picture44.png
![Material Metrics Picture44][Material Metrics Picture44]

**Description:**
This Athena query retrieves the top 10 failed requests by client IP addresses accessing an ALB from an access log table named `alb_access_logs_v1`.

**Functionality:**
- Counts the total number of requests, as well as the number of requests resulting in 4xx and 5xx errors for each client IP address.
- Sorts the results by the total request count in descending order and limits the output to the top 10 IP addresses.

## Hyperlink

[Material Metrics Picture45]:Grafana_setup/Picture45.png
![Material Metrics Picture45][Material Metrics Picture45]

We have added hyperlinks from Panel Option -> Panel Links.

[Material Metrics Picture46]:Grafana_setup/Picture46.png
![Material Metrics Picture46][Material Metrics Picture46]

**URL:**
[http://13.126.47.32:3000/d/ddjkq4ktifldse/prd-ptg-elb-failed-request?orgId=1&from=${__from}&to=${__to}&viewPanel=1](http://13.126.47.32:3000/d/ddjkq4ktifldse/prd-ptg-elb-failed-request?orgId=1&from=${__from}&to=${__to}&viewPanel=1)

- We've added `from` and `to` parameters to explicitly pass the `from_date` and `to_date` values to the target dashboard or visualization.
- Ensure that the variables `from` and `to` capture the correct date range from the source panel.
- After opening the hyperlink, it shows all failed requests.

## Data Links
**After hitting the Client IP:**

[Material Metrics Picture47]:Grafana_setup/Picture47.png
![Material Metrics Picture47][Material Metrics Picture47]

 It redirects to a new tab showing details of each Client IP, such as Time, Status Code, Target Processing Time, and Requested URL.

[Material Metrics Picture48]:Grafana_setup/Picture48.png
![Material Metrics Picture48][Material Metrics Picture48]

[Material Metrics Picture49]:Grafana_setup/Picture49.png
![Material Metrics Picture49][Material Metrics Picture49]

**URL:**
[Failed Request Dashboard](http://13.126.47.32:3000/d/ddjkq4ktifldse/prd-ptg-elb-failed-request?orgId=1&from=${__from}&to=${__to}&viewPanel=2&var-client_ip=${__value.raw})

- We've added ‘from’ and ‘to’ parameters to explicitly pass the ‘from_date’ and ‘to_date’ values to the target dashboard or visualization.
- Ensure that the variables ‘from’ and ‘to’ to capture the correct date range from the source panel. Below I have attached the source panel date ranges.
- `&var-client_ip=${__value.raw}`: This passes a variable (client_ip) with the value `${__value.raw}`. Make sure that `__value.raw` contains the desired client IP value.

## All Status Code And Request Count:

Provides a breakdown of the count of different ELB status codes returned by an Application Load Balancer (ALB) within a specified time range.

**Graph:**

[Material Metrics Picture50]:Grafana_setup/Picture50.png
![Material Metrics Picture50][Material Metrics Picture50]

**Queries:**

[Material Metrics Picture51]:Grafana_setup/Picture51.png
![Material Metrics Picture51][Material Metrics Picture51]

**Description:**
This Athena query retrieves the count of different ELB status codes returned by an Application Load Balancer (ALB) access log table named `alb_access_logs_v1`.

**Functionality:**
Counts the occurrences of each ELB status code and sorts the results in descending order based on the count of occurrences.

**DataLinks:**
We have attached multiple datalinks for each status code.

[Material Metrics Picture52]:Grafana_setup/Picture52.png
![Material Metrics Picture52][Material Metrics Picture52]

**URL:**
[Failed Request Data Dashboard](http://13.126.47.32:3000/d/ddj4et2jglywwb/prd-ptg-elb-sub?orgId=1&from=1713932807560&to=1713954407561&viewPanel=1&status=${__value.raw})

- `status=${__value.raw}`: This passes a variable (status code) with the value `${__value.raw}`. Make sure that `__value.raw` contains the desired status code value.

[Material Metrics Picture53]:Grafana_setup/Picture53.png
![Material Metrics Picture53][Material Metrics Picture53]

## Failed Request API:

Provides a breakdown of request counts, 4xx errors, and 5xx errors for the top 10 request URLs accessing an Application Load Balancer (ALB) within a specified time range, excluding image requests.

**Graph:**

[Material Metrics Picture54]:Grafana_setup/Picture54.png
![Material Metrics Picture54][Material Metrics Picture54]

**Query:**

[Material Metrics Picture55]:Grafana_setup/Picture55.png
![Material Metrics Picture55][Material Metrics Picture55]

[Material Metrics Picture56]:Grafana_setup/Picture56.png
![Material Metrics Picture56][Material Metrics Picture56]

**Description:**
The Athena query provides a breakdown of request counts, 4xx errors, and 5xx errors for the top 10 request URLs accessing an Application Load Balancer (ALB) within a specified time range, excluding image requests from access log table named `alb_access_logs_v1`.

**Functionality:**
Filters out requests with ELB status codes between 400 and 600, excludes requests with image extensions or containing "images/" in the URL, then counts the occurrences of each request URL and sorts the results in descending order based on the total count.

## Target Processing Time:

Segments request counts based on different time buckets of target processing time for successful requests hitting an Application Load Balancer (ALB) within a specified time range.

**Graph:**

[Material Metrics Picture57]:Grafana_setup/Picture57.png
![Material Metrics Picture57][Material Metrics Picture57]

**Query:**

[Material Metrics Picture58]:Grafana_setup/Picture58.png
![Material Metrics Picture58][Material Metrics Picture58]

[Material Metrics Picture59]:Grafana_setup/Picture59.png
![Material Metrics Picture59][Material Metrics Picture59]

[Material Metrics Picture60]:Grafana_setup/Picture60.png
![Material Metrics Picture60][Material Metrics Picture60]

**Description:**
This Athena query request counts based on different time buckets of target processing time for successful requests hitting an Application Load Balancer (ALB) access log table named `alb_access_logs_v1`.

**Functionality:**
Categorizes target processing time into predefined buckets and counts the number of requests falling within each bucket.

## Top 10 Requested URLs:

Retrieves the top 10 most requested URLs and their respective request counts hitting an Application Load Balancer (ALB) within a specified time range.

**Graph:**

[Material Metrics Picture61]:Grafana_setup/Picture61.png
![Material Metrics Picture61][Material Metrics Picture61]

**Query:**

[Material Metrics Picture62]:Grafana_setup/Picture62.png
![Material Metrics Picture62][Material Metrics Picture62]

**Description:**
This Athena query retrieves the top 10 most requested URLs and their respective request counts hitting an Application Load Balancer (ALB) access log table named `alb_access_logs_v1`.

**Functionality:**
Groups requests by URL and counts the occurrences of each URL, then sorts the results in descending order based on the request count and limits the output to the top 10 URLs.

## Total Request Count By Minutes:

Counts the number of requests hitting an Application Load Balancer (ALB) per minute within a specified time range.

**Graph:**

[Material Metrics Picture63]:Grafana_setup/Picture63.png
![Material Metrics Picture63][Material Metrics Picture63]

**Query:**

[Material Metrics Picture64]:Grafana_setup/Picture64.png
![Material Metrics Picture64][Material Metrics Picture64]

**Description:**
This Athena query retrieves counts the number of requests hitting an Application Load Balancer (ALB) per minute within a specified time range. access log table named `alb_access_logs_v1`.

**Functionality:**
Groups requests by minute and counts them, providing a breakdown of request counts for each minute.

## Failed Request / Minute:

Counts the number of failed requests hitting an Application Load Balancer (ALB) per minute within a specified time range.

**Graph:**

[Material Metrics Picture65]:Grafana_setup/Picture65.png
![Material Metrics Picture65][Material Metrics Picture65]

**Query:**

[Material Metrics Picture66]:Grafana_setup/Picture66.png
![Material Metrics Picture66][Material Metrics Picture66]

**Description:**
The Athena query analyses the temporal distribution of failed requests hitting an Application Load Balancer (ALB) by counting their occurrences over minute intervals within a specified time range from access log table named `alb_access_logs_v1`.

**Functionality:**
Aggregating the count of failed requests within each minute interval, facilitating understanding of error occurrence trends and enabling timely troubleshooting.

## Request Count For Failed Request:

Analyzing client IP addresses for their respective total request counts and counts of various HTTP error status codes (400, 401, 403, 404, 405, 500, 502, 503, 504) they encountered.

**Graph:**

[Material Metrics Picture67]:Grafana_setup/Picture67.png
![Material Metrics Picture67][Material Metrics Picture67]

**Query:**

[Material Metrics Picture68]:Grafana_setup/Picture68.png
![Material Metrics Picture68][Material Metrics Picture68]

[Material Metrics Picture69]:Grafana_setup/Picture69.png
![Material Metrics Picture69][Material Metrics Picture69]

**Description:**
The Athena query analyzing client IP addresses for their respective total request counts and counts of various HTTP error status codes (400, 401, 403, 404, 405, 500, 502, 503, 504) they encountered from Application Load Balancer (ALB). access log table named `alb_access_logs_v1`.

**Functionality:**
Summing up the occurrences of each HTTP error status code for individual client IP addresses within the specified range, aiding in pinpointing potential issues or problematic IPs causing specific errors.

# Create Database In Athena

**Steps:**

[Material Metrics Picture70]:Grafana_setup/Picture70.png
![Material Metrics Picture70][Material Metrics Picture70]

[Material Metrics Picture71]:Grafana_setup/Picture71.png
![Material Metrics Picture71][Material Metrics Picture71]

[Material Metrics Picture72]:Grafana_setup/Picture72.png
![Material Metrics Picture72][Material Metrics Picture72]

[Material Metrics Picture73]:Grafana_setup/Picture73.png
![Material Metrics Picture73][Material Metrics Picture73]

[Material Metrics Picture74]:Grafana_setup/Picture74.png
![Material Metrics Picture74][Material Metrics Picture74]

1. **GOTO** -> Create –>
2. **S3 Bucket Data:**
   - Identify the S3 bucket containing the data you want to query with Athena.
3. **Enter Table Name:**
   - Choose a name for the table you're creating in Athena.
4. **Select Create a Database:**
   - If you're creating a new database, ensure you select this option.
5. **Select S3 Bucket Path for ALB Logs/Other Information:**
   - Specify the S3 bucket path where your ALB logs or other data are located.
6. **Enter Column Fields:**
   - Define the column fields for your table. You can refer to an example shown in a snapshot or provide your own column definitions.
7. **Create Table:**
   - Finalize the table creation process.

# Import And Export Grafana Dashboards

## Export:
- Open the Grafana web interface and navigate to the resource you want to export, such as a dashboard or alert.
- Click on the settings icon (gear icon) in the top-right corner of the resource.
- In the dropdown menu, select "Export" or a similar option. OR Choose the desired export format, such as JSON or YAML.
- Save the exported file to your local machine.

[Material Metrics Picture75]:Grafana_setup/Picture75.png
![Material Metrics Picture75][Material Metrics Picture75]

Copy Or Save Json Model

[Material Metrics Picture76]:Grafana_setup/Picture76.png
![Material Metrics Picture76][Material Metrics Picture76]

## Import:
- **Import Dashboards:**
  - We have two options:
    1. Upload dashboards JSON file.
    2. Import via dashboard JSON Model.

[Material Metrics Picture77]:Grafana_setup/Picture77.png
![Material Metrics Picture77][Material Metrics Picture77]

[Material Metrics Picture78]:Grafana_setup/Picture78.png
![Material Metrics Picture78][Material Metrics Picture78]

- Navigate to the dashboard section in the Grafana web interface.
- Choose the appropriate option and follow the prompts to import the dashboard.

# Conclusion

In this guide, we explored various aspects of working with Grafana and Amazon Athena. 

- We learned how to create new visualizations in Grafana, enabling us to represent data effectively on dashboards.
- Understanding and documenting dashboard queries ensures clarity and facilitates collaboration among team members.
- Setting up a database in Athena allows seamless integration with Grafana, empowering users to query large datasets stored in S3 efficiently.
- Lastly, managing dashboards by importing and exporting them ensures backup and easy sharing, contributing to streamlined dashboard management workflows.
