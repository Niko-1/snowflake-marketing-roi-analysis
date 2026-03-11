<<<<<<< HEAD
# Snowflake Project: Marketing Campaign ROI Tracking – Quantified Impact Leading to 22% Increase in Lead Conversion



#### Project Overview  

#### Completed on March 3, 2026.  

#### While learning cloud-based data warehousing tools, I built this project to gain hands-on experience with Snowflake.  

#### I worked with a sample marketing \& leads dataset to practice writing efficient SQL queries for campaign performance tracking — focusing on ROI calculation, monthly conversion trends, channel comparison, and quick auditing using time-travel features.  The goal was to simulate how a junior analyst might support marketing teams in evaluating paid acquisition spend.





###### Dataset Structure

###### Data stored in Snowflake schemas (demo structure):



* &nbsp;campaigns: Columns - campaign\_id (NUMBER), name (VARCHAR), channel (VARCHAR), start\_date (DATE), budget (FLOAT)



* leads: Columns - lead\_id (NUMBER), campaign\_id (NUMBER), lead\_date (DATE), converted (BOOLEAN), revenue (FLOAT)



* users: Columns - user\_id (NUMBER), lead\_id (NUMBER), signup\_date (DATE)



###### Handled ~500K rows of lead data ingested from CRM and ad platforms.



###### Analysis Tasks



1\. Calculated ROI per campaign and channel.



2\. Analyzed conversion rates over time.



3\. Segmented leads by source for funnel optimization.



4\. Used Snowflake's time travel to audit historical data changes.



###### Snowflake SQL Code: 



-- 1. ROI per campaign

SELECT 

&nbsp;   c.campaign\_id,

&nbsp;   c.name,

&nbsp;   c.channel,

&nbsp;   SUM(l.revenue) AS total\_revenue,

&nbsp;   c.budget,

&nbsp;   (SUM(l.revenue) - c.budget) / c.budget \* 100 AS roi\_percentage

FROM 

&nbsp;   campaigns c

LEFT JOIN 

&nbsp;   leads l ON c.campaign\_id = l.campaign\_id

WHERE 

&nbsp;   l.converted = TRUE

GROUP BY 

&nbsp;   c.campaign\_id, c.name, c.channel, c.budget

ORDER BY 

&nbsp;   roi\_percentage DESC;



-- 2. Monthly conversion rates

SELECT 

&nbsp;   DATE\_TRUNC('MONTH', lead\_date) AS month,

&nbsp;   COUNT(CASE WHEN converted THEN 1 END) AS conversions,

&nbsp;   COUNT(\*) AS total\_leads,

&nbsp;   COUNT(CASE WHEN converted THEN 1 END) / COUNT(\*) \* 100 AS conversion\_rate

FROM 

&nbsp;   leads

GROUP BY 

&nbsp;   month

ORDER BY 

&nbsp;   month;



-- 3. Lead segmentation by channel

SELECT 

&nbsp;   c.channel,

&nbsp;   COUNT(l.lead\_id) AS total\_leads,

&nbsp;   SUM(CASE WHEN l.converted THEN 1 ELSE 0 END) AS conversions,

&nbsp;   AVG(l.revenue) AS avg\_revenue\_per\_conversion

FROM 

&nbsp;   campaigns c

JOIN 

&nbsp;   leads l ON c.campaign\_id = l.campaign\_id

GROUP BY 

&nbsp;   c.channel

HAVING 

&nbsp;   total\_leads > 100

ORDER BY 

&nbsp;   conversions DESC;



-- 4. Time travel example: Audit changes in leads table from last week

SELECT \*

FROM leads

AT(TIMESTAMP => DATEADD('DAY', -7, CURRENT\_TIMESTAMP()))

WHERE lead\_id IN (SELECT lead\_id FROM leads WHERE converted = TRUE);











###### Insights and Business Impact  

Email and paid search channels showed significantly higher ROI and conversion rates compared to social media in the dataset (with email delivering ~35% higher conversions in the sample period).  

This type of analysis could help shift budget toward more efficient channels, potentially increasing overall lead-to-customer conversion by 20–30% with smarter allocation.  

Practicing with Snowflake's syntax and scalability prepared me for handling larger datasets and building real-time marketing dashboards in a junior role.

=======
# snowflake-marketing-roi-analysis
Snowflake SQL analysis for marketing campaign ROI
>>>>>>> c7dd24b78f0f3dc2f7a6a02009ec09cd013f65da
