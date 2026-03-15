📦 Logistics Intelligence Engine: Automated Stock & Inbound Tracker
🎯 Project Overview
This project was engineered to solve a critical visibility gap in warehouse operations: the disconnect between current stock levels and inbound supply chain data. ## 🧠 Core DAX Logic

1. Stock Intelligence Status (Stock_Status)
Code snippet

Stock_Status = 
VAR CurrentInventory = SUM('Cleaned_Stock'[Quantity])
VAR PlannedInbound = SUM('Wk_11'[Quantity])

RETURN
SWITCH(
    TRUE(),
    CurrentInventory > 0, "🟢 In Stock",
    CurrentInventory <= 0 && PlannedInbound > 0, "🟡 OOS - Inbound Pending",
    "🔴 Critical Shortage"
)
2. Logistics Forecasting (ETA_Week)
Code snippet

ETA_Week = 
VAR NextWeekArrival = MAX('Wk_11'[Download_Date]) + 7
RETURN
IF(
    [Dostawa_Inbound] > 0, 
    "Wk " & WEEKNUM(NextWeekArrival), 
    BLANK()
)
🛠️ Technical Stack
Data Engineering: Python (pandas, pdfplumber)

Analytics Platform: Microsoft Power BI Desktop

Language: DAX & M Query

👤 Author
Hubert Kowalski

LinkedIn Profile

Email: kowalskihubert343@gmail.com
