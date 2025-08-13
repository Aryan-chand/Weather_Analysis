<H1> </a><img src="https://upload.wikimedia.org/wikipedia/commons/thumb/c/cf/New_Power_BI_Logo.svg/600px-New_Power_BI_Logo.svg.png?20210102182532" alt="Microsoft Power BI" width="30" height="30"> Customer Retention Analysis 

## 🌦 Real-Time Weather Analysis Dashboard
<br>


# Table of contents
- [Problem Statement](https://github.com/Aryan-chand/Customer-Retention-Analysis?tab=readme-ov-file#problem-statement)
- [Data Source](https://github.com/Aryan-chand/Customer-Retention-Analysis?tab=readme-ov-file#data-sourcing)
- [Data Preparation](https://github.com/Aryan-chand/Customer-Retention-Analysis?tab=readme-ov-file#data-preparation)
- [Data Visualization](https://github.com/Aryan-chand/Customer-Retention-Analysis?tab=readme-ov-file#data-visualization)
- [Analysis and Insights](https://github.com/Aryan-chand/Customer-Retention-Analysis?tab=readme-ov-file#analysis-and-insights)
- [Shareable Link](https://github.com/Aryan-chand/Customer-Retention-Analysis?tab=readme-ov-file#link-shareable-link)


# Problem Statement

- **Problem:** Churning customers using PhoneNow services were got in touch after they terminated the contract, and the Customer Retention manager wants to understand their customer profile and insights with a focus on retaining customers as well as approaching in advance who is at risk.
- **Objectives:** The purpose of this analysis is to create a Customer Retention Dashboard in Power BI for the Customer Retention Manager that reflects all relevant Key Performance Indicators (KPIs) and metrics to:
    - Self-exploratory the customer demographics and insights (churning & retaining).
    - Actively approach who is at risk with the risk level of specific customer
    - Contain many metrics and plots related to a single area of business for discussing with higher managers and generating further analysis.
    - Allows for minimal interaction.
    - Based on finding recommend improving customer retention.
# Data Sourcing

The Dataset used for this analysis was provided by :link:[Pwc Switzerland](https://cdn.theforage.com/vinternships/companyassets/4sLyCPgmsy8DA6Dh3/02%20Churn-Dataset.xlsx)

# Data Preparation

The dataset was loaded into Microsoft Power BI Desktop for modeling after transformation in Power Query.

The tabulation below shows the metadata of `Churn` dataset:

| File name | 02 Churn-Dataset  |
| --- | --- |
| Format | .xlsx |
| Size | 772KB |
| Fields | 23 |
| Entities | 7043 |

The tabulation below shows the `Churn` table with its field's names and their description:

| Field Name | Description | Data Type |
| --- | --- | --- |
| customerID | Represents the unique number of the customer in the dataset | Text  |
| gender | Describes the gender of the customer | Text |
| SeniorCitizen | Describes if the customer is a senior citizen | Text |
| Partner | Describes if the customer has a partner | Text |
| Dependents | Describes if the customer has a dependent | Text |
| tenure | Describes how long as a customer | Whole number |
| PhoneService | Describes if the customer has registered a phone service | Text |
| MultipleLines | Describes if the customer has registered multiple lines | Text |
| InternetService | Describes if the customer has registered for Internet service | Text |
| OnlineSecurity | Describes if the customer has registered for online security | Text |
| OnlineBackup | Describes if the customer has registered for online backup | Text |
| DeviceProtection | Describes if the customer has registered for device protection | Text |
| TechSupport | Describes if the customer has registered for tech support | Text |
| StreamingTV | Describes if the customer has registered to stream tv | Text |
| StreamingMovies | Describes if the customer has registered to stream movies | Text |
| Contract | Describes the length of the contract of the customer | Text |
| PaperlessBilling | Describes if the customer has registered for paperless billing | Text |
| PaymentMethod | Describes the payment method of the customer | Text |
| MonthlyCharges | Represents the monthly charge incurred by the customer | Decimal number |
| TotalCharges | Represents the total charge incurred by the customer | Decimal number |
| numAdminTickets | Represents the number of admin tickets opened by the customer | Whole number |
| numTechTickets | Represents the number of tech tickets opened by the customer | Whole number |
| Churn | Describes if the customer is at risk of churn | Text |
- **Relevant information about the** `Churn` **dataset:**
    - Customers who left within the last month
    - Services each customer has signed up for phone, multiple lines, internet, online security, online backup, device protection, tech support, and streaming TV and movies
    - Customer account information: how long as a customer, contract, payment method, paperless billing, monthly charges, total charges and number of tickets opened in the categories administrative and technical
    - Demographic info about customers – gender, age range, and if they have partners and dependents

### Data Cleaning

Data Cleaning for the dataset was done in Power Query as follows:

- Each of the columns in the table was validated to have the correct data type
- There are 11 `N/A` values in `TotalCharges` column. Those missing values were filled with the `MonthlyCharges` value of each row because those customers are new and their tenure is just 1. `Table.AddColumn(#"Changed Type", "Custom", each if [TotalCharges] = null then [MonthlyCharges] else [TotalCharges])`

### Data Transformation

A new table named `Churn unpivot` was created by duplicating the `Churn dataset` table and unpivoting some columns to support a clear overview look. In the new table, I conducted transformation using M-formula, you can refer at below:

- Attribute of demographic info: `Table.Unpivot(#"Replaced Value1", {"SeniorCitizen", "Partner", "Dependents"}, "Attribute", "Value")`
- Attribute of services:
    - `Table.ReplaceValue(#"Renamed Columns","No internet service","No",Replacer.ReplaceText,{"OnlineSecurity", "OnlineBackup", "DeviceProtection", "TechSupport", "StreamingTV", "StreamingMovies"})`
    - `Table.Unpivot(#"Reordered Columns", {"PhoneService", "MultipleLines", "Internet", "OnlineSecurity", "OnlineBackup", "DeviceProtection", "TechSupport", "StreamingTV", "StreamingMovies"}, "Attribute", "Value.1")`

# Data Visualization

Data visualization for the datasets was done in Microsoft Power BI Desktop, the dashboard includes 3 main dashboards and 5 tooltip pages

![dashboard github](https://github.com/Aryan-chand/Customer-Retention-Analysis/blob/main/customer%20retention_pg1.png)
![dashboard github](https://github.com/Aryan-chand/Customer-Retention-Analysis/blob/main/customer%20retention_pg2.png)

### Key Performance Indicators and Metrics:

**About Customer Profile:**

- Number of retained and churned customers
- Retention & Churn Rate
- Total Admin & Tech ticket
- Total and monthly charge
- Demographic, Account and Service info

**About EDA Churn Profile:**

- Churn by each service
- Churn by tenure
- Churn by Contract type
- Total Admin & Tech tickets of churn customers

**About Churn Predictive Model Comparison:**

- Churn Predictive Model Evaluation
- Most important model features
- Risk level
  
### Measures

The measure used in visualization are:

- **Calculated measures**
    - Rate of customer = `IF(ISFILTERED('Churn dataset'[Churn]),DIVIDE(CALCULATE(COUNT('Churn dataset'[Churn]), 'Churn dataset'[Churn] = SELECTEDVALUE('Churn dataset'[Churn])),CALCULATE(COUNT('Churn dataset'[customerID]),ALL('Churn dataset'[Churn])),0),DIVIDE(COUNT('Churn dataset'[customerID]),CALCULATE(COUNT('Churn dataset'[customerID]),ALL('Churn dataset'))))`
    - %churn = `DIVIDE(CALCULATE(COUNT('Churn dataset'[Churn]), 'Churn dataset'[Churn] = "Yes"),CALCULATE(COUNT('Churn dataset'[Churn]), ALL('Churn dataset'[Churn])))`
    - %male = `DIVIDE(CALCULATE(COUNTA('Churn dataset'[gender]),'Churn dataset'[gender] = "Male"),COUNTA('Churn dataset'[gender]))`
    - %female = `DIVIDE(CALCULATE(COUNTA('Churn dataset'[gender]),'Churn dataset'[gender] = "Female"),COUNTA('Churn dataset'[gender]))`
    - subcription = `SWITCH(TRUE(),'Churn unpivot'[tenure]<=12,"< 1 year",'Churn unpivot'[tenure]<=24,"< 2 years",'Churn unpivot'[tenure]<=36,"< 3 years",'Churn unpivot'[tenure]<=48,"< 4 years", 'Churn unpivot'[tenure]<=60,"< 5 years",'Churn unpivot'[tenure]<=72,"< 6 years")`
    - #use admin ticket = `CALCULATE(COUNTA('Churn dataset'[numAdminTickets]),'Churn dataset'[numAdminTickets] > 0)`
    - #use tech ticket = `CALCULATE(COUNTA('Churn dataset'[numTechTickets]),'Churn dataset'[numTechTickets] > 0)`
- **Format measures**
    - customer text = `SWITCH(
        TRUE(),
        SELECTEDVALUE('Churn dataset'[Churn]) = "Yes", "Total Churn Customers",
        SELECTEDVALUE('Churn dataset'[Churn]) = "No", "Total Retained Customers",
         "Total Customers")`
    - dashboard name =`SWITCH(
        TRUE(),
        SELECTEDVALUE('Churn dataset'[Churn]) = "Yes","Churn Dashboard",
        SELECTEDVALUE('Churn dataset'[Churn]) = "No", "Retention Dashboard",
         "Dashboard")`
    - rate text =`SWITCH(
        TRUE(),
        SELECTEDVALUE('Churn dataset'[Churn]) = "Yes","Churn Rate",
        SELECTEDVALUE('Churn dataset'[Churn]) = "No", "Retention Rate",
         "Total Rate")`
    - Welcome text = `VAR Hour = HOUR(NOW())
    VAR Greeting = 
    SWITCH(
        TRUE(),
        Hour >= 0 && Hour < 5, "Good Night",
        Hour >= 5 && Hour < 12, "Good Morning",
        Hour >= 12 && Hour < 18, "Good Afternoon",
        Hour >= 18 && Hour < 24, "Good Evening"
    )
    RETURN
    Greeting & " " & "Manager!"`

# Analysis and Insights
The purpose of this dashboard is to serve as self-exploratory for managers, but I still note some highlighted points that I recognize below:

- Month-to-Month contracts, lack of online security and tech support, and issues with Fiber Optic service are some of the reasons for customer churn.
- Only 16% of the customers are senior citizens, with almost double the churn rate compared to younger customers.
- The customers have varying contract lengths, with a lot of them only staying for a month and some for up to 72 months.
- Customers taking longer contracts tend to be more loyal and stay with the company for a longer period of time.
- Customers are more likely to churn when the monthly charges are high, and there is a higher chance of churn when the total charges are lower.
- 
# :link: Shareable Link 
You can interact and have fun with the dashboard here:

[Microsoft PowerBI](https://app.powerbi.com/groups/me/reports/67c6a7b3-7a00-4474-8d5e-64b531ab0ae1/ReportSection515eb6e3c03bdcc7c490?experience=power-bi)
