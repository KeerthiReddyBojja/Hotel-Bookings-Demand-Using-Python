# Hotel-Bookings-Cancellation-Analysis-Using-Python

## Business Problem Statement 
Major Hotel chains 'City Hotel' and Resort Hotel' are experiencing high booking cancellation rates, leading to significant loss in revenue and inefficient room inventory management. Leadership needs actionable insights to identify areas for reducing cancellations and maximizing revenue. 

## Dataset Overview 
The analysis is based on the Hotel Booking Demand dataset, originally shared on [Kaggle.](https://www.kaggle.com/datasets/jessemostipak/hotel-booking-demand/discussion?sort=undefined). It contains 119,390 records of hotel bookings across two hotels:
    • City Hotel - A traditional urban hotel
    • Resort Hotel - A resort-style property in a leisure destination. 

The dataset covers a duration of three years (2015-2017) and includes detailed information for each booking, such as:
    • Booking characteristics - lead time, deposit type ("No Deposit", "Non Refund", "Refundable"), market segment, and               booking channel ("Travel Agent, "Direct").
    • Guest Profile - number of adults, children, and babies; whether the guest is a repeat visitor; and whether the booking is        from a corporate entity. 
    • Stay details - length of stay (weekend and weekday nights), room type, parking requirements, and special requests.
    • Financial data - Average Daily Rate (ADR) and cancellation status. 

## Key Columns Used
Below are the main columns used in the analysis, with definitions and their importance in understanding hotel reservation cancellations:
| SR.NO | COLUMN                   | DESCRIPTION | IMPORTANCE                           |
|----------|-------------------------------------|----------------|-------------------------------------------------------|
| 1        | is_canceled               | Binary flag: 1 if the booking was canceled, 0 if completed              |  Core target variable for cancellation analysis               |
| 2        | hotel                    | Type of hotel: "City Hotel" or "Resort Hotel"              | Helps compare cancellation behavior between city and resort properties.       |
| 3        | deposit_type             | Type of deposit made: "No Deposit", "Non Refund" or "Refundable"              | Key predictor of cancellation risk            |
| 4        | market_segment             | Booking channel category (e.g., "Online TA", "Direct", "Corporate"              | Shows which customer segments cancel most frequently.                     |
| 5        | booked_via_agent             | Binary flag: 1 if the booking was made by a corporate entity, 0 for individual guests              | Highlights differences in reliability    |
| 6        | ADR (Average Daily Rate)  | Average price per day for the booking         | Used to assess lost revenue     |  

## Exploratory Data Analysis (EDA)

### Data Quality Issues & Data Cleaning
**1.Missing Values**

        • children: 4 missing values → Imputed as 0 (most bookings have no children).
        
        • country: 488 missing values → Imputed as "Unknown" to preserve row count and avoid data loss.
        
        • agent and company → Large number of missing values 
                › agent = NaN → Direct booking
                › company = NaN → Individual Guest
          New flags "booked_via_agent" and "is_corporate_booking" were created. 
          
**2.Outlier Handling**

        • One extreme ADR outlier ($5,400) was removed to prevent skewing the data (I believe the number was mistaken, instead of $540, because stays_in_week_nights was '2' and there were only 2 adults. $5,400 seems too high). 
        
**3."Non Refund" Cancellation Anomaly**

        • 99.4% of 'Non Refund' bookings are canceled seems wrong but documented in the original research paper by the author.
        • These are largely fraudulent or visa-support bookings (made with invalid payment details).
        
**4.ADR Interpretation**

        • Canceled bookings have higher average ADR ($104.84 VS. $99.99), indicating hotels are losing potential revenue to cancellations.
        
**5.Lead Time Bins** 

          • Lead time was binned into intervals (<2 months, 2-6 months, etc.), to find how lead time influences cancellations.

  ## Key Insights
  • Overall cancellation rate is 37%, representing $13.1M in lost revenue, excluding "Non refund" bookings.
  • "No Deposit" bookings constitute 99% of real lost revenue ($13,103,000), despite being ~88% of total bookings. It is the highest financial risk segment.
  • Travel Agent bookings cancel at 39%, approximately 1.6x more than Direct bookings (24.7%). High-risk when combined with "No Deposit" (30.6% cancellation).
  • Corporate guests are low-risk (17.5% cancellation vs. 38.2% for individuals) and cancel 5x less, which is ideal for stable occupancy.
  • High-risk + No Deposit - "Travel Agent + No Deposit" cancels at 30.6% and represents significant lost revenue. 
  • Long Lead Time Bookings show an elevated cancellation rate.

  ## Actionable Recommendations
  1. The hotel is losing its highest-value potential revenue to cancellations. Risk mitigation efforts must be put on bookings that exceed the average ADR.
  2. Implement a mandatory, non-refundable partial deposit for bookings that fall into these long-term, high-risk segments to secure commitment early.
  3. Offer a 5% discount to guests to switch from "No Deposit" to "Refundable".
  4. Create a corporate loyalty program with perks. Negotiate long-term contracts with companies.
  5. When a high-ADR booking cancels, the front desk should be immediately notified to prioitize re-selling that room, as the loss is financially significant. 

## Issue Tracking Table
