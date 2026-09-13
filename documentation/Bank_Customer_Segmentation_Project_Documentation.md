**Project Title:**

Bank Customer Segmentation \& Transaction Intelligence Dashboard



**Problem Statement:**

Banks generate large volumes of customer and transaction data, but raw transaction records alone do not provide a clear view of customer demographics, spending behaviour, customer value, or engagement patterns.



This project transforms raw banking transaction data into an interactive Power BI dashboard that enables analysis of customer demographics, transaction behaviour, RFM-based customer segmentation, and behavioural value/risk indicators.



The objective is to provide a centralized analytical view that helps identify valuable customer segments, understand transaction patterns, evaluate customer engagement, and support data-driven customer management decisions.



**Business Objectives:**

* Analyze the demographic profile of bank customers by age, gender, and location.
* Understand transaction volume, transaction value, account balance, and transaction activity patterns.
* Segment customers using Recency, Frequency, and Monetary (RFM) analysis.
* Identify loyal, new, lost/inactive, and other customer segments based on observed transaction behaviour.
* Compare customer value and transaction frequency across different segments.
* Develop behavioural risk and value indicators from available RFM-based data where actual credit/risk fields are unavailable.
* Provide interactive filters and visual insights to support customer-level and segment-level analysis.
* Build an interactive, professional Power BI dashboard that converts raw banking data into actionable business insights.



**Dataset \& Data Description**

The project uses a banking transaction dataset containing customer information and transaction-level records.



The dataset includes the following fields:



* TransactionID — Unique identifier for each transaction
* CustomerID — Identifier linking transactions to customers
* CustomerDOB — Customer date of birth
* CustGender — Customer gender
* CustLocation — Customer location
* CustAccountBalance — Customer account balance recorded with the transaction
* TransactionDate — Date of the transaction
* TransactionTime — Time of the transaction
* TransactionAmount (INR) — Transaction amount in Indian Rupees



The dataset contains approximately 1.05 million transaction records and more than 884,000 unique customers.



The analysis uses transaction-level data to understand customer behaviour and creates a separate customer dimension for customer-level demographic analysis.



These field definitions are directly aligned with the project brief.



**Important**

Don't add **Credit Score**, **Risk Level**, or **Value Score** to the dataset description as if they were original fields. Those are derived/proxy metrics we created later and will be documented separately under Methodology \& Limitations.





**Data Cleaning \& Preparation**

The raw banking transaction data was prepared using Power Query in Power BI before building the analytical model.



The main data preparation steps were:



* Promoted the first row as column headers.
* Corrected the data types for transaction amount and account balance.
* Converted TransactionDate into a proper date field using the appropriate locale.
* Converted the raw numeric TransactionTime into a valid time data type.
* Cleaned CustomerDOB by correcting two-digit year values and treating invalid/placeholder dates such as 01/01/1800 as missing.
* Standardized customer gender values into Male, Female, Other, and Unknown.
* Created a customer dimension (DimCustomer) containing one record per customer.
* Retained the latest observed customer record when multiple demographic records existed for the same customer.
* Created a dedicated date dimension (DimDate) for time-based analysis.
* Created supporting date attributes such as Year, Month, Day Name, and Month Year.
* Created transaction time attributes including Transaction Hour and Time of Day.
* Created appropriate sort columns to ensure chronological and logical ordering in visuals.



These preparation steps were performed to improve data consistency, enable reliable customer-level analysis, and support interactive time-based reporting.



**One important point**

We should not say that missing values were simply deleted, because your approach did not do that. You handled invalid values appropriately and retained usable records.





**Data Model \& Relationships**

A structured data model was created in Power BI to separate customer-level information, transaction-level information, and date-related information.



The model consists of three primary tables:



1\. DimCustomer



Contains one unique record for each customer and stores customer-level attributes such as:



CustomerID

CustomerDOB

Gender

Location

Age

Age Group



2\. bank\_transactions



Contains the transaction-level records and includes:



TransactionID

CustomerID

TransactionDate

TransactionTime

TransactionTime\_Clean

TransactionAmount (INR)

CustAccountBalance

Transaction Hour

Time of Day



3\. DimDate



A dedicated date dimension was created to support time-based analysis. It contains:



Date

Year

Month

Month Number

Day Name

Day Number

Month Year



**Relationships**



DimCustomer\[CustomerID] → bank\_transactions\[CustomerID]

One-to-many relationship

Single-direction filtering

DimDate\[Date] → bank\_transactions\[TransactionDate]

One-to-many relationship

Single-direction filtering



This model enables customer-level demographic analysis while maintaining transaction-level detail and consistent time-based analysis across the dashboard.



**NOTE**:

CustomerRFM is not added to this section as a primary model relationship. It is a calculated table used specifically for the RFM-based segmentation and behavioural analysis.







**Key Measures \& Calculations**



DAX measures and calculated columns were created to support the dashboard's KPI cards, charts, segmentation analysis, and behavioural indicators.



1. Customer Metrics



Total Customers — Distinct count of customers.

Male Customers — Number of customers classified as Male.

Female Customers — Number of customers classified as Female.

Male Customer % — Percentage of total customers who are Male.

Female Customer % — Percentage of total customers who are Female.

Average Customer Age — Average age calculated from the cleaned customer date of birth.

Unique Locations — Number of distinct customer locations.



2\. Transaction Metrics



Total Transactions — Distinct count of TransactionID.

Total Transaction Amount — Sum of transaction amounts.

Average Transaction Amount — Average transaction amount.

Highest Transaction Amount — Maximum individual transaction amount.

Average Account Balance — Average recorded customer account balance.

Transactions per Customer — Total transactions divided by total customers.

Average Transaction Value per Customer — Total transaction amount divided by total customers.



3\. Customer Segmentation Metrics



RFM analysis was performed using:



Recency — Number of days since the customer's last observed transaction within the dataset period.

Frequency — Number of transactions made by the customer.

Monetary — Total transaction amount associated with the customer.



Recency, Frequency, and Monetary values were converted into 1–5 scores using percentile-based thresholds. The three scores were combined to create an RFM Score ranging from 3 to 15.



Customers were then categorized into the following segments:



* Loyal
* New
* Lost
* Other



The Other segment was retained for customers who did not satisfy the defined Loyal, New, or Lost criteria.



4\. Behavioural Risk \& Credit Proxies



Because the original dataset does not contain actual credit score or risk-level fields, behavioural proxy metrics were derived from the RFM analysis:



Behavioural Risk Score — Derived inversely from the RFM Score.

Behavioural Risk Level — Categorized as Low, Medium, or High based on the Behavioural Risk Score.

Credit Score Proxy — A scaled behavioural indicator derived from the RFM Score.

Total Value Score — Sum of the Monetary Scores.



These proxy metrics are used strictly for analytical demonstration and should not be interpreted as actual banking credit-risk assessments.





**Dashboard Pages \& Analysis Covered**



The Power BI report is organized into multiple analytical pages so that the required business questions can be presented clearly without overcrowding individual pages.



1\. Customer Analysis



Focuses on customer demographics and distribution, including:



* Total customer count
* Average customer age
* Male and female customer counts
* Unique customer locations
* Gender distribution
* Customer distribution by age group
* Top customer locations
* Gender distribution across age groups
* Detailed customer information
* Interactive filtering by age group, gender, and location



2\. Transaction Analysis



Focuses on transaction behaviour and activity patterns, including:



* Total transaction volume
* Average transaction amount
* Highest transaction amount
* Average account balance
* Transaction volume trends over time
* Average transaction value by age group
* Transaction activity by day and time of day
* Daily transaction activity
* Interactive filtering by transaction date, transaction hour, and transaction amount



3\. Customer Segmentation



Uses RFM-based analysis to understand customer value and engagement, including:



* Loyal customers
* New customer revenue
* Lost/inactive customers
* Customer segment distribution
* Average revenue per customer by segment
* Revenue by customer segment
* Transaction frequency by segment
* Interactive filtering by customer segment, gender, and age group



4\. RFM \& Segment Insights



Provides deeper analysis of RFM scores and customer segment composition, including:



* RFM score distribution by customer segment
* Customer segment distribution across age groups
* Interactive filtering by customer segment, gender, and age group



5\. Profitability \& Risk Analysis — Page 1



Presents customer value and behavioural risk indicators, including:



* Total customer revenue
* Average credit score proxy
* High-risk customer count
* Total monetary value
* Average credit score proxy by segment
* Behavioural risk-level distribution
* Credit score proxy distribution by segment



6\. Profitability \& Risk Analysis — Page 2



Provides additional value and risk analysis, including:



* Account balance by risk level
* Total value score by segment
* Top 10 high-revenue, high-risk customers
* Filtering by credit score proxy, behavioural risk level, and monetary score



The report uses interactive slicers and cross-filtering to allow users to explore customer, transaction, segmentation, profitability, and behavioural risk insights from different perspectives.





**Key Business Insights**



The dashboard provides several important insights into customer demographics, transaction behaviour, customer value, and engagement.



Customer Demographics



* The dataset contains approximately 884K unique customers, providing a broad customer base for demographic analysis.
* Customer demographics can be analyzed across gender, age groups, and more than 9K locations.
* The age-group and gender analysis helps identify the customer categories contributing most to the overall customer base.
* Location analysis highlights the geographic areas with the highest concentration of customers.



Transaction Behaviour



* The dataset contains approximately 1.05 million transactions.
* The average transaction amount is approximately ₹1,574, while the median transaction amount is considerably lower, indicating that transaction values are influenced by higher-value transactions.
* Transaction activity varies across dates and times, allowing identification of periods with relatively higher transaction volumes.
* Transaction analysis also enables comparison of spending behaviour across different customer age groups.



Customer Segmentation



* Lost/Inactive customers represent the largest segment under the defined RFM rules, followed by New, Other, and Loyal customers.
* Loyal customers have the highest average revenue per customer, indicating higher monetary value among this group.
* The RFM framework helps distinguish customers based on their recent activity, transaction frequency, and monetary contribution.
* Segment analysis can therefore support differentiated customer engagement and retention strategies.



Value \& Behavioural Risk



* Customer monetary contribution can be compared across RFM segments to identify high-value customer groups.
* Behavioural risk analysis highlights customers whose RFM-based engagement patterns indicate relatively higher behavioural risk.
* The Top 10 analysis provides a focused view of customers combining high revenue contribution and high behavioural risk.
* These insights can help prioritize further investigation and customer-management activities.



**Important Interpretation**



The Lost segment represents customers who appear inactive within the observed transaction period; it should not be interpreted as confirmed permanent churn.



Similarly, the Credit Score Proxy and Behavioural Risk Level are derived from RFM behaviour because actual credit-score and risk-level fields are not present in the source dataset. They should therefore be treated as analytical indicators rather than formal banking risk measures.





**Limitations \& Assumptions**



The following limitations and assumptions should be considered when interpreting the dashboard:



* The dataset represents a limited transaction period, so customer activity and inactivity are evaluated only within the available observation window.
* The Lost segment represents customers who were inactive within the observed period and does not confirm permanent customer churn.
* Customer demographic information may contain missing or inconsistent values across transactions. A latest-observed customer record was therefore retained for customer-level analysis.
* Invalid or placeholder dates, including 01/01/1800, were treated as missing rather than being used to calculate customer age.
* Missing gender and location values were retained and handled through appropriate categories where required.
* CustAccountBalance represents the balance recorded with transaction records. The customer-level balance analysis uses the latest observed transaction date and should not necessarily be interpreted as a live current account balance.
* The original dataset does not contain actual Credit Score, Risk Level, or Value Score fields.
* The Credit Score Proxy, Behavioural Risk Score, and Behavioural Risk Level are derived from RFM-based customer behaviour and are intended for analytical demonstration only.
* These behavioural proxies must not be interpreted as actual banking credit assessments, regulatory risk classifications, or lending decisions.
* Transaction amount analysis reflects the transactions available in the dataset and may not represent a customer's complete banking relationship.
* The dashboard is designed for analytical and portfolio demonstration purposes rather than production banking decision-making.





**Tools \& Technologies**



* Power BI Desktop — Used to build the interactive dashboard, data model, DAX calculations, and visualizations.
* Power Query — Used for data cleaning, transformation, data-type correction, and preparation of customer and transaction data.
* DAX (Data Analysis Expressions) — Used to create measures, calculated columns, RFM scores, customer segments, and behavioral risk/value indicators.
* CSV — Used as the primary source format for the banking transaction dataset.



Key Power BI Concepts Applied



* Data cleaning and transformation
* Dimensional data modeling
* One-to-many relationships
* Date dimension and time intelligence
* Calculated columns and measures
* RFM customer segmentation
* Interactive slicers and cross-filtering
* KPI cards and analytical visualizations
* Behavioral proxy metrics
* Dashboard design and user-focused reporting





**Conclusion**



The Bank Customer Segmentation \& Transaction Intelligence Dashboard transforms more than one million banking transaction records into an interactive analytical solution covering customer demographics, transaction behaviour, RFM-based segmentation, customer value, and behavioural risk indicators.



The project demonstrates the complete Power BI analytics workflow, from data cleaning and transformation through data modelling, DAX calculations, segmentation, visualization, and interactive dashboard development.



The RFM analysis provides a structured approach to identifying different customer behaviour patterns, while the transaction and demographic analysis helps reveal how customer characteristics relate to banking activity and monetary contribution.



Where the source dataset did not provide actual credit-risk information, derived behavioural proxies were used and clearly identified as such. This ensures that the dashboard remains analytically useful while maintaining appropriate interpretation of the available data.



Overall, the project demonstrates the ability to convert raw business data into a professional, interactive, and decision-oriented Power BI reporting solution.





**Project Structure \& How to Use the Dashboard**



The report is organized into dedicated pages, with each page focusing on a specific analytical area:



1. Customer Analysis — Explore customer demographics, age groups, gender, and locations.
2. Transaction Analysis — Analyze transaction volume, transaction values, account balances, and transaction activity patterns.
3. Customer Segmentation — Explore RFM-based customer segments and customer value.
4. RFM \& Segment Insights — Analyze RFM score distributions and segment composition across age groups.
5. Profitability \& Risk Analysis — Page 1 — Review customer value, credit-score proxies, and behavioral risk indicators.
6. Profitability \& Risk Analysis — Page 2 — Explore account balance, value scores, and high-revenue/high-risk customers.



**Dashboard Interaction**



Users can interact with the report using the available slicers and visual cross-filtering. Selecting a value in one visual can dynamically filter related visuals on the page.



Available filters include:



* Age Group
* Gender
* Location
* Transaction Date
* Transaction Hour
* Transaction Amount
* Customer Segment
* Credit Score Proxy
* Behavioural Risk Level
* Monetary Score



This interactive structure allows users to move from a high-level overview to detailed customer, transaction, segment, and behavioural analysis.





