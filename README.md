README
UtilityWise — Utility Bill Management & Analysis System
A local Flask + SQLite web application for tracking utility bills, visualizing spending, converting currencies, and generating rule-based saving insights.
Features
Add utility bills
Store original currency
Dashboard with total spending
Utility category doughnut chart
Monthly spending line chart
Bill history
Delete bills
Analytics page
Currency conversion using a public exchange-rate API
Rule-based spending insights
Smart Insights page with an explainable 3-month-average spending baseline
Actionable energy and water saving checklists (without inventing emissions data)
CSV export for bill records
Responsive dashboard UI
Run on macOS
cd UtilityBillAnalyzer
python3 -m venv venv
source venv/bin/activate
pip install -r requirements.txt
python app.py
​
Open:
http://127.0.0.1:5000
Important
Currency conversion needs an internet connection. Bill storage and the main dashboard work locally with SQLite.
Presentation architecture
User → Flask routes → SQLite database → analysis + simple forecasting + rule-based recommendations → HTML templates + Chart.js
Smart Insights uses a transparent average of up to the latest three recorded monthly totals. It is a baseline estimate, not a machine-learning model. CSV export preserves original amounts and currencies. Currency conversion requires internet access; when rates fail, non-matching currencies are excluded from selected-currency estimates and a warning is shown.
For a university presentation, explain the system as:
Data collection
Data storage
Data normalization/currency conversion
Data analysis
Visualization
Recommendation generation
Local AI assistant (Ollama)
The AI assistant is available at /assistant when the Flask app is running. It uses the local Ollama API and the qwen2.5:3b model. No extra Python package is required for this integration.
Install and open Ollama.
In a terminal, run ollama pull qwen2.5:3b once.
Confirm the model exists with ollama list.
Start the Flask app with python app.py.
Open http://127.0.0.1:5000/assistant.
The browser sends messages to Flask; Flask calls http://127.0.0.1:11434/api/chat. If the assistant reports a connection error, confirm Ollama is running and that the model name matches qwen2.5:3b.
