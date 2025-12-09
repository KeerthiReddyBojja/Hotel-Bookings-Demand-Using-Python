# Hotel-Bookings-Cancellation-Analysis-Using-Python

## Business Problem Statement 
Major Hotel chains 'City Hotel' and Resort Hotel' are experiencing high booking cancellation rates, leading to significant loss in revenue and inefficient room inventory management. Leadership needs actionable insights to identify areas for reducing cancellations and maximizing revenue. 

## Dataset Overview 
The analysis is based on the Hotel Booking Demand dataset, originally shared on [Kaggle.](https://www.kaggle.com/datasets/jessemostipak/hotel-booking-demand/discussion?sort=undefined). It contains 119,390 records of hotel bookings across two hotels:                                                                                                                        
    • City Hotel - A traditional urban hotel                                                                                                                                  
    • Resort Hotel - A resort-style property in a leisure destination. 

The dataset covers a duration of three years (2015-2017) and includes detailed information for each booking, such as:      
    • Booking characteristics - lead time, deposit type ("No Deposit", "Non Refund", "Refundable"), market segment, and               booking channel ("Travel Agent, "Direct").                                                                                                                         
    • Guest Profile - number of adults, children, and babies; whether the guest is a repeat visitor; and whether the booking is from a corporate entity.                                                                                                                                           
    • Stay details - length of stay (weekend and weekday nights), room type, parking requirements, and special requests.    
    • Financial data - Average Daily Rate (ADR) and cancellation status. 

## Key Columns Used
Below are the main columns used in the analysis, with definitions and their importance in understanding hotel reservation cancellations:
| SR.NO | COLUMN                   | DESCRIPTION | IMPORTANCE                           |
|----------|-------------------------------------|----------------|-------------------------------------------------------|
| 1        | is_canceled               | Binary flag: 1 if the booking was canceled, 0 if completed              |  Core target variable for cancellation analysis               |
| 2        | hotel                    | Type of hotel: "City Hotel" or "Resort Hotel"              | Helps compare cancellation behavior between city and resort properties.       |
| 3        | deposit_type             | Type of deposit made: "No Deposit", "Non Refund" or "Refundable"              | Key predictor of cancellation risk            |
| 4        | ADR (Average Daily Rate)  | Average price per day for the booking         | Used to assess lost revenue     |  

## Exploratory Data Analysis (EDA)

### Data Quality Issues & Data Cleaning

| SR.NO | ISSUE DESCRIPTION                   | RESOLUTION NOTES                           |
|----------|-------------------------------------|-------------------------------------------------------|
| 1        | Null values in 'children' column             | Imputed missing values with 0              |
| 2        | Null values in 'country' column                    | Imputed missing values with 'Unknown'       |
| 3        | Sparse 'company' column             | Dropped column; created binary flag 'is_corporate_booking'            |
| 4        | Sparse 'agent' column              | Dropped column; created binary flag 'booked_via_agent'                    |
| 5        | Incorrect data type for 'reservation_status_date            | Converted from object to datetime using pd.to_datetime()    |
| 6        | Extreme outlier in ADR  | Removed 1 outlier with ADR = $5,400    |  
| 7        | 'Non Refund' deposit anomaly | Excluded from revenue lost calculations |
| 8        | Need to calculate total stay length | Used sum of 'stays_in_weekend_nights', 'stays_in_week_nights' for revenue lost calculations |

### Key Data Interpretation & Anomalies 
• **"Non Refund" Anomaly:** The high cancellation rate (99.4%) for 'Non-refund' bookings was noted and attributed to known fraudulent/visa-support bookings (per source documentation). These were excluded from the revenue loss
calculations.

•**"ADR Interpretation:** Canceled bookings had a higher average ADR ($104.84) than confirmed bookings ($99.99), indicating that premium revenue is disproportionately lost to cancellations.

  ## Key Insights
1. Overall cancellation rate is 37%, representing $13.1M in lost revenue, excluding "Non-refund" bookings.
   
2.  "No Deposit" bookings constitute 99% of real lost revenue ($13,103,000), despite being ~88% of total bookings. It is the highest financial risk segment.                                                                                                                                             
3. Travel Agent bookings cancel at 39%, approximately 1.6x more than Direct bookings (24.7%). High-risk when combined with "No Deposit" (30.6% cancellation).                                                                                                                      
4. Corporate guests are low-risk (17.5% cancellation vs. 38.2% for individuals) and cancel 5x less, which is ideal for stable occupancy.                                                                                                                                                                                  
5. High-risk + No Deposit - "Travel Agent + No Deposit" cancels at 30.6% and represents significant lost revenue.               
6. Long Lead Time Bookings show an elevated cancellation rate.

  ## Actionable Recommendations
1. The hotel is losing its highest-value potential revenue to cancellations. Risk mitigation efforts must be put on bookings that exceed the average ADR.
2. Implement a mandatory, non-refundable partial deposit for bookings that fall into these long-term, high-risk segments to secure commitment early.
3. Offer a 5% discount to guests to switch from "No Deposit" to "Refundable".
4. Create a corporate loyalty program with perks. Negotiate long-term contracts with companies.
5. When a high-ADR booking cancels, the front desk should be immediately notified to prioitize re-selling that room, as the loss is financially significant.

## Tech Stack & Tools
• **Programming Language:** Python

• **Data Manipulation & Cleaning:** Pandas, NumPy

• **Data Visualization:** Matplotlib, Seaborn

• **Environment:** Jupyter Notebook
