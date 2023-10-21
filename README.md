# 📈**Cohort Analysis with Power BI**

<img src="https://github.com/hamzaugursumer/CohortAnalysis-PowerBI/assets/127680099/51ee8a67-9d5a-4d0c-82f8-abfa7fddb3a1)" width="1700" height="600">

* **You can access the dataset by [clicking here](https://archive.ics.uci.edu/dataset/502/online+retail+ii).**
* **You can access the visualization PDFs of the cohort study with Power BI [here](https://github.com/hamzaugursumer/CohortAnalysis-PowerBI/blob/main/Cohort%20pdf.pdf).**
* **You can [click here](https://github.com/hamzaugursumer/CohortAnalysis-PowerBI/blob/main/Cohort%20Analysis%20Power%20BI.pbix) to download the Power BI File of the cohort study.**


## **📌What is Cohort Analysis and Why Is It Done?**

* Cohort analysis is a data analysis method used to group customers, users, or any set of individuals based on a specific characteristic or behavior, and to track and analyze their performance over time.
* Cohorts are created by bringing together individuals or objects with similar attributes, typically representing those who had a similar experience during a certain period.
* Cohort analysis is widely utilized in fields such as marketing, customer management, user experience optimization, and business strategy development.
  * The primary reasons for conducting cohort analysis are as follows:
  * **Monitoring Customer Behavior:** Understanding which customer groups engaged with a business during a specific period and assessing the outcomes helps a business gain insights into customer behavior.
  * **Loyalty Analysis:** Examining the likelihood of customers remaining loyal to a business over a certain period and assessing their loyalty levels.
  * **Product Development:** Identifying which products are preferred by specific cohorts, guiding the development of new products.
  * **Optimizing Marketing Strategies:** Understanding which marketing campaigns are more effective for specific cohorts can help in optimizing marketing strategies.
 
 ## **📌To perform cohort analysis, you can follow the fundamental steps:**

* **Cohort Definition:** The first step is to define the cohorts you want to analyze. These cohorts are typically composed of users with similar sign-up dates or a specific behavior.
* **Data Collection:** Collect the relevant data and organize it based on the defined cohorts. Data sources may vary depending on your business goals and the topic you want to analyze.
* **Tracking Cohort Performance:** Determine specific metrics or KPIs to track the performance of each cohort over time. These metrics might include revenue, conversion rates, or retention rates.
* **Analysis of Results:** Compare the performance of cohorts and try to understand which groups are more successful or which factors influence performance.
* **Strategy Development:** Based on the analysis results, take actions to improve or optimize your business strategies. For instance, you may focus more on successful cohorts or target specific cohorts more effectively.

## **📌Steps applied from the power query phase**

* The 'Invoice' and 'StockCode' columns were converted to text, and canceled invoices, which are the ones starting with the letter "C," were not included in the process.
````
= Table.SelectRows(#"Filtered Rows", each not Text.StartsWith([Invoice], "C"))
````
* The 'InvoiceDate' column was converted to the Date data type.
* The 'Quantity' and 'Price' columns were multiplied, resulting in a new column named 'SalesAmount'.
````
= Table.AddColumn(#"Changed Type1", "SalesAmonunt", each [Quantity] * [Price], Currency.Type)
````
* There are 0 values in the 'SalesAmount' column. We are not including these values in the analysis as they have no relevance or represent any discounts or other specific circumstances.
* We are selecting the columns to continue our operations using the 'Choose Column' menu tool.
  * (Quantity,InvoiceDate,Price,CustomerID,Country,SalesAmount)
* The dataset contains two sheets for the years 2009-2010 and 2010-2011, but we have combined these sheets and conducted an analysis.

## **📌DAX Functions I Used in Power BI**

````
Active Customers = DISTINCTCOUNT(FactSales[CleanedData.Customer ID])
````
````
New Customers = 
    CALCULATE(
        [Active Customers],
        FactSales[Month Since First Transaction] = 0
    )
````
````
Retention Rate = 
    DIVIDE([Cohort Performance],[New Customers])  
````
````
Cohort Performance =
VAR MinDate = MIN(DimDate[Start of Month])
VAR MaxDate = MAX(DimDate[Start of Month])
Return
    CALCULATE(
            [Active Customers],
            REMOVEFILTERS(DimDate[Start of Month]),
            RELATEDTABLE(DimCustomer),
            DimCustomer[First Transaction Month]>=MinDate 
                && DimCustomer[First Transaction Month]<=MaxDate
    )
````
## **📌How to read a cohort analysis chart?**

* This dataset belongs to a UK-based company with wholesale customers. It spans over three years, and cohorts have been examined on a monthly basis.
* When we look at the row with the months, the month marked as 0 represents the first-time customers for the company.
* When we examine the 0 column, we observe the count of new customers acquired in consecutive months.
* For example, in December 2009, the company gained 955 new customers.
    - ![image](https://github.com/hamzaugursumer/CohortAnalysis-PowerBI/assets/127680099/540dadb9-6a79-406a-ba11-b70b01dfda7d)
* When we look at this consecutively, we are tracking a declining trend in acquiring new customers.
* Therefore, the company should take actions to improve customer acquisition.
    - **So what should we do if we can't get new customers?**
    - **We should Define the Customer Profile:** By examining our current customers and our best customers, we should identify the ideal customer profile.
    - **We should Conduct Market Research:** We need to understand the needs and demands of our potential customers. We should determine which products or services are in higher demand.
    - **We should Improve Our Marketing Strategies:** To attract new customers, we should review our marketing strategies. We should focus on better targeting, more attractive offers, and creating attention-grabbing advertising campaigns.
    - **We should Enhance Our Website and Online Presence:** Strengthening our online presence is essential. We should improve the user experience on our website, carry out SEO efforts, and effectively use social media platforms.
    - **We should Create Loyalty Programs:** To retain our existing customers, we should establish loyalty programs. By offering incentives like reward programs or discounts, we can increase customer loyalty.
    - **We should Evaluate Customer Feedback:** It's important to carefully assess customer feedback and use it as a basis for improving our products or services.
* When we want to look at the cohort chart at a row level, we see how many of the new customers have continued to make purchases from us in the following months and have remained engaged.
    - ![image](https://github.com/hamzaugursumer/CohortAnalysis-PowerBI/assets/127680099/4510c8a9-bdb1-45f2-a6f6-96ef254cfafc)
    - For example, when we look at April 2010, we acquired 294 new customers. However, in the following month, only 57 of them have continued to engage with us and made purchases. When looking at the overall chart, it's evident that new customers acquired are gradually lost as the months progress.

## **📌The most important points in cohort analysis**

* ![image](https://github.com/hamzaugursumer/CohortAnalysis-PowerBI/assets/127680099/200a70d0-d94c-442a-b501-cf3cff5b5b48)
   - When we look at December 2010, we can consider it as the date with the highest customer churn rate within the cohort analysis. Only 9% of the new customers we acquired have continued.
   - In our cohort table, I believe the standout months are the 3rd and 4th months. I consider these months critical for retaining customers because we've observed consecutive declines during that period. Equipped with this information, the e-commerce business can now start addressing the reasons behind this trend and take new measures to halt it. For example, they can develop a three-month loyalty campaign to re-engage customers and prevent the trend of declining interest.
