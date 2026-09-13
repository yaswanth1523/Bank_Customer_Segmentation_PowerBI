# Bank Customer Segmentation & Transaction Intelligence Dashboard

## 📊 Project Overview

An interactive Power BI dashboard designed to transform large-scale banking transaction data into actionable insights across customer demographics, transaction behavior, RFM-based customer segmentation, customer value, and behavioral risk indicators.

The project demonstrates an end-to-end data analytics workflow covering data cleaning, data modeling, DAX calculations, customer segmentation, interactive visualization, and business insight generation.

### 📸 Dashboard Preview

![Customer Analysis Dashboard](Screenshots/customer-analysis.png)

![Transaction Analysis Dashboard](Screenshots/transaction-analysis.png)

![Customer Segmentation Dashboard](Screenshots/customer-segmentation.png)

![RFM & Segment Insights](Screenshots/rfm-segment-insights.png)

![Profitability & Risk Analysis](Screenshots/profitability-risk-1.png)

![Profitability & Risk Analysis - Page 2](Screenshots/profitability-risk-2.png)

---

## 🎯 Problem Statement

Banks generate large volumes of customer and transaction data, but raw transaction records alone do not provide a clear view of customer demographics, spending behavior, customer value, or engagement patterns.

This project transforms raw banking transaction data into an interactive Power BI dashboard that enables analysis of customer demographics, transaction behavior, RFM-based customer segmentation, and behavioral value/risk indicators.

The objective is to provide a centralized analytical view that helps identify valuable customer segments, understand transaction patterns, evaluate customer engagement, and support data-driven customer management decisions.

---

## 💼 Business Objectives

- Analyze customer demographics by age, gender, and location.
- Understand transaction volume, transaction value, account balance, and transaction activity patterns.
- Segment customers using Recency, Frequency, and Monetary (RFM) analysis.
- Identify loyal, new, lost/inactive, and other customer segments.
- Compare customer value and transaction frequency across segments.
- Develop behavioral risk and value indicators from available RFM-based data.
- Provide interactive filters for customer-level and segment-level analysis.
- Build a professional, interactive, decision-oriented Power BI dashboard.

---

## 🗂️ Dataset

The dataset contains approximately:

- **1.05M+ transaction records**
- **884K+ unique customers**
- **9K+ customer locations**

### Key Fields

| Field | Description |
|---|---|
| TransactionID | Unique transaction identifier |
| CustomerID | Customer identifier |
| CustomerDOB | Customer date of birth |
| CustGender | Customer gender |
| CustLocation | Customer location |
| CustAccountBalance | Account balance recorded with the transaction |
| TransactionDate | Transaction date |
| TransactionTime | Transaction time |
| TransactionAmount (INR) | Transaction amount in Indian Rupees |

---

## 🧹 Data Preparation

Power Query was used for:

- Data type correction
- Transaction date conversion
- Transaction time conversion
- Customer DOB cleaning
- Two-digit year correction
- Invalid/placeholder DOB handling
- Gender standardization
- Customer-level deduplication
- Creation of a customer dimension
- Creation of a dedicated date dimension
- Creation of transaction hour and time-of-day attributes
- Chronological sorting of date attributes

---

## 🏗️ Data Model

The Power BI model consists of:

### DimCustomer
Customer-level demographic information.

### bank_transactions
Transaction-level banking records.

### DimDate
Dedicated date dimension for time-based analysis.

### Relationships

```text
DimCustomer
     │
     │ 1 → *
     ▼
bank_transactions
     ▲
     │ * ← 1
     │
DimDate
