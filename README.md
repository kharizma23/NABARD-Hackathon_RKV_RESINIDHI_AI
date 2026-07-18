# RKV ResiNidhi AI

Team Phoenix | NABARD Hackathon @ GFF 2026

---

## Who we are

Raina E (Team Leader, BIT Sathyamangalam)
Kharizma A (BIT Sathyamangalam)
Vassudev S (BIT Sathyamangalam)

We are a team of three students from Tamil Nadu. We have spent the last few weeks talking to local dairy farmers and retail shop owners in and around Sathyamangalam to understand how they manage their cash flow. That ground experience shaped most of this project.

---

## Why we built this

Most rural micro-enterprises do not have a formal credit history. Banks and field officers usually assess them based on past transaction records or physical visits. The problem is that by the time a field officer notices a problem—like a repayment delay or falling stock turnover—the enterprise is already in stress.

NABARD asked for a system that predicts 3 to 6 months of cash flow. But we realized early on that just showing a prediction is not helpful. If a dairy farmer is going to run out of cash in October, they need to know what to do about it in September. They do not need another red flag. They need a practical plan.

That is why our focus shifted from risk identification to risk prevention.

---

## What our platform actually does

We built RKV ResiNidhi AI as a cash flow forecasting and early intervention platform. The name stands for Resilience and Finance (Nidhi). The platform takes data from multiple sources—regular income and expense entries, UPI transaction proxies, rainfall data from IMD, and commodity prices from Agmarknet.

We combine all of this to generate a forecast for the next six months. But the core of our idea rests on three things:

First, we create a digital twin. It is essentially a simulated copy of the enterprise. We use it to test different shock scenarios. What if the price of fodder goes up by 15 percent? What if the monsoon is delayed? We run these simulations to see where the business breaks.

Second, we calculate something we call the Resilience Gap. Instead of just saying the enterprise is high risk, we calculate exactly how much money or what operational change is needed to keep the cash flow positive for the next 90 days.

Third, we use that gap to recommend specific rescue actions. The system does not approve loans automatically, but it gives the field officer a short list of options. It might say shift the EMI date, delay the next inventory purchase, provide a small bridge loan, or coordinate bulk procurement through the FPO.

---

## How we handle rural constraints

We are very aware that most of these enterprises are in areas with patchy internet. So we designed the mobile interface to work offline. Data is stored locally in the browser using IndexedDB and syncs to the backend automatically whenever a network connection is available.

We also kept language in mind. A typed English form is not practical for many entrepreneurs. So we are building voice assisted entry in Tamil and Hindi. The alerts are also generated in plain language. Instead of showing a technical risk score, the entrepreneur will see something like "October may be difficult because your expenses are rising faster than income."

For new enterprises that do not have enough historical data, we use a cohort based benchmark. We group similar businesses in the same district and sector and use that as a baseline until the enterprise has its own transaction history.

---

## End to end process

Here is the complete flow we designed:

1. An enterprise is onboarded with basic details like sector, location, and existing loan or savings information.

2. The field officer or entrepreneur enters monthly income, expenses, stock purchases, and repayment dates through the mobile interface.

3. All of this is stored locally if there is no network. It syncs to the backend when connectivity returns.

4. The system pulls external signals like rainfall, temperature, commodity prices, and seasonal demand patterns.

5. We clean the data and generate features like moving averages, repayment overlap ratios, and shock indexes.

6. The forecast model runs. We are using XGBoost quantile regression to predict income and expenses with confidence bands. We do not give a single number because that creates false confidence.

7. The digital twin simulates five specific shocks on the forecast output. These include price increases, demand drops, delayed customer payments, climate disruptions, and production losses.

8. The risk classifier flags the enterprise as Low, Moderate, or High based on when the cash deficit is likely to occur and how large it is.

9. The Resilience Gap is calculated. It tells the field officer the minimum intervention required to keep the enterprise above zero balance.

10. The Risk to Rescue engine compares different intervention options and recommends the most practical one for the specific situation.

11. Alerts are generated for both the entrepreneur and the field officer. The entrepreneur gets a simple local language warning. The field officer gets a panel showing the top three drivers for the risk and the suggested action.

12. The system also aggregates risk at the village or FPO level. If 17 out of 42 dairy units in a village show fodder cost stress, the radar triggers a cluster level recommendation for bulk procurement.

13. The field officer records what action was taken and how the enterprise responded. This feedback is used to improve the next set of predictions.

---

## Technology stack

We are planning to build this using the following tools. We chose them mostly because they are practical and we have some prior experience with them.

Frontend: React.js as a Progressive Web App. This lets us run it on mobile, tablet, and desktop with one codebase. IndexedDB handles the local offline storage.

Backend: Python with FastAPI. It is straightforward to write REST APIs and serve machine learning models. We are containerizing everything with Docker to keep deployment consistent.

Database: PostgreSQL for the main relational data like enterprise profiles and user records. We are using TimescaleDB for the time series data like daily transactions and market signals.

Machine Learning: We are using LightGBM and XGBoost for the quantile regression forecasts. Isolation Forest for detecting unusual transactions or sudden drops in income. SHAP for explaining why a particular enterprise was flagged. The shock simulations are done with Monte Carlo methods written in Python.

Visualization: Recharts and Plotly for the dashboards. We need to show forecast confidence bands, risk heatmaps, and cluster level views.

Deployment: We are planning to host it on AWS or Render. The most important part is the offline sync layer, so we are spending more time on that than on scaling.

---

## Business model

We are following an institution led B2B2C model. The mobile app for the entrepreneur will remain free. We believe that is necessary for adoption and data collection.

The revenue comes from institutional subscriptions. Banks, RRBs, MFIs, and FPO federations pay for the portfolio dashboard. It gives them the ability to monitor all their enterprises, prioritize high risk cases, and track intervention outcomes.

We also plan to charge for API integration services if a bank wants to connect this with their core lending system. Custom district level reports and sector specific risk models would be additional paid services.

We are also open to open sourcing the core profiling framework as a Digital Public Good. We think that aligns well with NABARDs mission. But the advanced analytics and dashboards will remain subscription based.

We think this is commercially viable because banks spend a lot of manual effort on field monitoring right now. Our platform reduces that effort and helps them catch repayment stress three months earlier. That directly reduces NPAs and improves their lending portfolio quality.

---

## What is in this repository right now

Since this is the first round, we are not submitting a working application. We wanted to use this repository to show our design thinking and system planning.

The docs folder contains our system architecture diagram and a preliminary database schema. We wanted to show that we have thought about how data flows from the village level to the cloud.

The sample data folder contains mock CSV files for enterprise financials, market signals, and climate data. We used these to test our feature engineering logic on paper.

The ui mockups folder has exports from our design phase. We have screens for the entrepreneur dashboard, the field officer risk list, and the alert view. We believe showing the interface early proves we are thinking about adoption and usability.

The model design folder has markdown files explaining the Resilience Gap formula and the Risk to Rescue decision matrix in plain math. That is our main differentiator.

---

## Final note

We are a student team from a small engineering college in Tamil Nadu. We do not have corporate experience or massive datasets. But we understand the ground reality of rural micro enterprises because we see it around us every day.

Our focus on prevention over identification is what we believe sets us apart. We are not trying to build just another credit scoring tool. We are trying to build something that actually helps a farmer or a small retailer take action before things go wrong.

We are looking forward to the next rounds and we are ready to prototype this for dairy and rural retail sectors.

Team Phoenix

PPT demo video explanation :
https://drive.google.com/drive/folders/1fnIYbQ0SDtjYMhio3-kiEHdS3boW7G1v?usp=sharing
