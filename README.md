Hubert, rozumiem frustrację. Problem polega na tym, że GitHub widzi te potrójne tyldy w moim tekście i traktuje je jako polecenie, a Ty chcesz dostać czysty tekst do skopiowania, który sam w sobie te tyldy zawiera.

Zrobimy to w sposób "brutalny" – wysyłam Ci to w bloku kodu, ale UWAŻAJ: na samym początku i na samym końcu Twojego pliku README na GitHubie NIE MOŻE być żadnych tyld. Ma być tylko to, co jest w środku poniższego szarego pola.

Markdown

# 📦 Logistics Intelligence Engine: Automated Stock & Inbound Tracker

[![Python](https://img.shields.io/badge/Python-3.9+-blue.svg)](https://www.python.org/)
[![Power BI](https://img.shields.io/badge/Power_BI-Data_Modeling-yellow.svg)](https://powerbi.microsoft.com/)
[![DAX](https://img.shields.io/badge/DAX-Advanced_Analytics-orange.svg)](https://docs.microsoft.com/en-us/dax/)

## 🎯 Project Overview
This project was engineered to solve a critical visibility gap in warehouse operations: **the disconnect between current stock levels and inbound supply chain data.** By integrating fractured datasets into a unified Power BI dashboard, I built an automated "Early Warning System" for stockouts and dynamic ETA forecasting.

## 🛠️ The Challenge
* **Data Silos:** Warehouse inventory data lived in daily CSV exports, while inbound shipment details were locked in weekly PDF reports.
* **Zero Visibility:** Critical low-stock SKUs were indistinguishable from those with pending deliveries.
* **Manual Reporting:** Compiling accurate stock status required hours of manual data manipulation in Excel.

## 🚀 The Solution: A Unified Data Pipeline
1. **Python ETL:** Custom scripts using `pandas` and `pdfplumber` to extract, clean, and standardize SKU data from PDFs.
2. **Star Schema Modeling:** Engineered a resilient data model in Power BI with a central **Master_SKU1** dimension table.
3. **Advanced DAX Analytics:** Developed custom measures using `VAR` and `SWITCH` for real-time stock status flagging.

## 🧠 Core DAX Logic

### 1. Stock Intelligence Status (`Stock_Status`)
This measure dynamically prioritizes inventory risk using robust `VAR` and `SWITCH` logic.

```dax
Stock_Status = 
VAR CurrentInventory = SUM('Cleaned_Stock'[Quantity])
VAR PlannedInbound = SUM('Wk_11'[Quantity])

RETURN
SWITCH(
    TRUE(),
    CurrentInventory > 0, "🟢 In Stock",
    CurrentInventory <= 0 && PlannedInbound > 0, "🟡 OOS - Inbound Pending",
    "🔴 Critical Shortage" -- 0 Stock & 0 Inbound
)
```
2. Logistics Forecasting (ETA_Week)
An automated ETA tracker that estimates arrival weeks based on data ingestion timestamps.
```
ETA_Week = 
VAR NextWeekArrival = MAX('Wk_11'[Download_Date]) + 7
RETURN
IF(
    [Dostawa_Inbound] > 0, 
    "Wk " & WEEKNUM(NextWeekArrival), 
    BLANK()
)
```
✨ Key Business Benefits
100% Critical Shortage Visibility: Instantly isolates SKUs with zero stock and zero inbound shipments.

Data-Driven ETA: Supply chain coordinators use automated forecasting to optimize inbound logistics windows.

Efficiency: Reduces manual analysis time by 90% through automated ETL.

💻 Technical Stack
Data Engineering: Python (pandas, pdfplumber)

Analytics Platform: Microsoft Power BI Desktop

Language: DAX & M Query

👤 Author
Hubert Kowalski

www.linkedin.com/in/hubert-kowalski-081189398

Email: kowalskihubert343@gmail.com
