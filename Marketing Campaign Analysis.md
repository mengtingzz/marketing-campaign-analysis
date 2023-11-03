# Marketing Campaign Analysis

## Scenario
As a data analyst working for an advertising agency, Client A, a cosmetic company, has been implementing digital advertising across various channels such as search, display, and social media. They seek your expertise in understanding the **seasonality** and devising **effective marketing campaign strategies** for peak seasons to optimize sales. What approach would you recommend taking in this scenario?

## Step 1: Identify Key Metrics

In this step, we define key metrics that form the foundation of our analysis.

### Seasonality Metrics:
1. **Sales Volume:** Reflects revenue patterns over time, helping identify seasonal sales trends.
2. **Keyword Search Volume:** Indicates customer demand for products during specific seasons.
3. **Web Traffic (Sessions):** Measures user engagement, revealing peak website visitation periods.

### Campaign Performance Metrics:
1. **Attributed Sales:** Measures revenue directly attributed to advertising efforts.
2. **Conversion Rate (CR):** CR = (Number of Conversions / Number of Impressions) * 100. Gauges campaign efficiency in converting users into customers.
3. **Return on Advertising Spend (ROAS):** ROAS = (Attributed Sales / Advertising Spend). Evaluates advertising profitability.

**Answer:**

<img width="465" alt="Screen Shot 2023-11-02 at 8 17 43 PM" src="https://github.com/mengtingzz/marketing-campaign-analysis/assets/123043791/53903cfa-d42a-421c-8fc6-9bab673e7cff">

## Step 2: Analyze Seasonality with SQL and Visualizations

In this step, we explore seasonality trends using SQL queries and visualizations.

### Sales Volume & Website Traffic Trends
The SQL query groups sales and sessions by month to examine changes over time.
```sql
-- SQL query for Sales volume & website traffic trends
SELECT month(date) as month
, sum(sales) as sales
, sum(sessions) as sessions
FROM site_data 
WHERE client = 'A' 
GROUP BY 1 
```
**Answer:**

<img width="632" alt="salestrends" src="https://github.com/mengtingzz/marketing-campaign-analysis/assets/123043791/6883be71-d84e-46bf-a14f-d6e47b3e728d">

### Keywords Search Volume\
We identify when consumers are most actively searching for our products.\
```sql\
-- SQL query for Keywords Search Volume\
select\
date\
, sum(search_volume) as searches from keyword_data\
where\
lower(keyword) in ('a', 'eyeliner',\
'lipstick', 'lipgloss', 'eyeshadow', 'foundation', 'highlighter', 'eyebrow', 'lotion', 'facewash', 'serum')\
group by 1\
```\
\
**Insight:**\
The analysis reveals that the highest points of sales, website traffic, and keyword searches coincide with specific seasonal events such as New Year's, Valentine\'92s Day, summer, and holiday seasons. This suggests an opportunity to tailor marketing strategies to maximize sales during these peak periods.\
\
## Step 3: Analyze Campaign Effectiveness by Channel with SQL\
\
In this section, we evaluate the effectiveness of marketing campaigns across different channels using revenue, conversion rate, ROAS, and net profit.\
\
```sql\
-- SQL query for Campaign Effectiveness by Channel\
select channel\
,sum(attributed_sales) as revenue ,sum(conversions)/sum(impressions) as conv_rate ,sum(attributed_sales)/sum(spend) as ROAS ,sum(attributed_sales)-sum(spend) as net_profit \
from campaign_performance where client = 'A' \
and date between '2022-01-01' and '2022-12-31' group by 1 \
```\

**Insight:**\
Allocate a larger budget to the highly effective search and social campaigns, while also incorporating display advertising to enhance awareness and acquire new users.\
\
## Step 4: Optimize Marketing Campaigns\
\
In this step, we focus on optimizing marketing campaigns with a two-pronged approach: campaign targeting based on demographics and behavioral targeting.\
\
### Demographics Targeting:\
Through an in-depth analysis of demographic data, we have identified a key segment of Client A's customer base:\
- **Customer Profile:** Our analysis reveals that the majority of Client A's customers are women aged 35-39 residing in New York.\
\
### Behavioral Targeting:\
To further refine our targeting strategies, we delve into the purchase behavior of this specific customer segment.\
- **Most Purchased Categories:** We analyze the product categories that resonate most with this demographic group.\
```sql\
-- SQL query for Most Purchased Categories\
select\
category,\
sum(sales) as sales from user_level_sales\
where\
age_group = '35-39'\
and region = 'NY'\
and gender = 'F'\
and brand = 'A'\
and date between '2022-01-01'\
and '2022-12-31' group by 1\
```\
\
### Average Purchase Frequency:\
We calculate the average number of transactions per customer within this period:\
```sql\
-- SQL query for Average Purchase Frequency\
select\
count (distinct order_id)/count(distinct\
customer_id) as frequency from user_level_sales where\
date between '2022-01-01' and '2022-12-31' and age_group = '35-39'\
and region = 'NY'\
}
