Analyzes 83.57K hotel bookings across 163 countries to predict booking cancellations. It provides insights into customer types, booking sources, deposit types, and room preferences. By identifying key trends, such as transient customers and non-refundable deposits, this analysis will help the business predict potential cancellations and optimize strategies to reduce them, improving overall profitability

### **Features**

-	`country`: Country of origin.
-	`market_segment`: Market segment designation. 
-	`previous_cancellations`: Number of previous bookings that were cancelled by the customer prior to the current booking.
-	`booking_changes`: Number of changes/amendments made to the booking from the moment the booking was entered on the PMS until the moment of check-in or cancellation.
-	`deposit_type`: Indication on if the customer made a deposit to guarantee the booking. 
-	`days_in_waiting_list`: Number of days the booking was in the waiting list before it was confirmed to the customer.
-	`customer_type`: Type of booking.
-	`reserved_room_type`: Code of room type reserved. Code is presented instead of designation for anonymity reasons.
-	`required_car_parking_space`: Number of car parking spaces required by the customer.
-	`total_of_special_request`: Number of special requests made by the customer (e.g. twin bed or high floor).
-	`is_canceled`: Value indicating if the booking was canceled (1) or not (0).

# Hotel Booking Cancellation Prediction

This repository contains a predictive model and business recommendations to reduce hotel booking cancellations and optimize revenue.

---

## Table of Contents
1. [Best Model](#best-model)
2. [Model Interpretation](#model-interpretation)
3. [Model Limitations](#model-limitations)
4. [Metrics](#metrics)
5. [Feature Selection](#feature-selection)
    - [Feature Importance](#feature-importance)
    - [SHAP](#feature-importance-using-shap)
6. [Cost Savings Calculation](#cost-savings-calculation)
7. [Recommendations](#recommendations)
    - [Model Recommendations](#model-recommendations)
    - [Business Recommendations](#business-recommendations)
8. [Conclusion](#conclusion)

---

## Best Model

- **Model:** LightGBM  
  LightGBM (Light Gradient Boosting Machine) is a gradient boosting-based machine learning algorithm that is efficient and fast, designed to handle large datasets with accurate classification and regression capabilities.

- **Resampler:** RandomUnderSampling  
  RandomUnderSampling is used to address class imbalance in the dataset, where the number of samples in one class is much higher than in the other class.

---

## Model Interpretation

- **Scaling:** Robust scaling to reduce the impact of extreme values.
- **Encoders:** Binary and One Hot Encoder.
  - Binary Encoder converts categorical variables into a more efficient numeric representation.
  - One Hot Encoder converts categorical variables into a numeric format suitable for machine learning models.

These preprocessing steps aim to efficiently convert data into a format usable by the predictive model, improving accuracy and efficiency in learning patterns.

---

## Model Limitations

- Duplicate data is removed to prevent overfitting.
- Missing values are very few and removed to avoid bias.
- LightGBM is a "black box" model, making interpretability difficult, especially with many trees and features.

---

## Metrics

- **Recall** is used, focusing on False Negatives (FN): people predicted not to cancel but who actually did cancel.

---

## Feature Selection

### Feature Importance

From both methods of feature selection, the best features for the predictive model were obtained. These features are:  
`onehot__market_segment_Online TA`, `scaling__total_of_special_requests`, `binary__country_3`, `binary__country_4`, `onehot__deposit_type_Non Refund`, `scaling__required_car_parking_spaces`, `scaling__previous_cancellations`, `scaling__booking_changes`.

---

## Cost Savings Calculation

**Given Data:**
- Total Customers: 2016
- Did Not Cancel: 1537
- Cancelled: 479
- Cost per Room: 50 USD

**Without Model:**  
- Total Cost: 100,800 USD  
- Cost Wasted for cancellations: 23,950 USD  
- Total Savings: 0 USD

**With Model:**  
- Total Cost: 70,800 USD  
- Cost Wasted (FP): 27,100 USD  
- Total Savings: 30,000 USD

| Description | Without Model | With Model |
|-------------|---------------|------------|
| Total Customers | 2016 | 2016 |
| Cost per Room | 50 USD | 50 USD |
| Total Cost | 100,800 USD | 70,800 USD |
| Customers Not Cancelled Served | 1537 | 995 |
| Customers Not Cancelled Not Served | 0 | 542 |
| Customers Cancelled Served | 0 | 421 |
| Customers Cancelled Not Served | 0 | 58 |
| Cost Wasted | 23,950 USD | 27,100 USD |
| Total Savings | 0 USD | 30,000 USD |

---

## Recommendations

### Model Recommendations

1. **Increase Recall**: Focus on detecting all positive cases to reduce false negatives.  
2. **Try Other Models and Resamplers**:  
   - Other models: Random Forest, XGBoost, Logistic Regression, ensemble models.  
   - Other resamplers: SMOTE, ADASYN, Cluster-based Over-sampling.  
3. **Use Feature Selection**: Select the most relevant features to reduce dimensionality, improve accuracy, and avoid overfitting.

### Business Recommendations

1. **Stricter Cancellation Policies**  
   - Reconfirmation before a certain date  
   - Cancellation prohibition for certain categories  
   - Non-refundable pricing

2. **Special Deals or Discounts**  
   - Offers for replacement bookings  
   - Incentives for rescheduling

3. **Pre-Authorization Policies**  
   - Credit card pre-authorization  
   - Non-refundable deposit

4. **Enhance Customer Experience**  
   - Improve user experience (check-in/out)  
   - Increase customer satisfaction with packages, free meals, or additional services

---

## Conclusion

Using a predictive model and targeted business policies, the hotel can reduce losses from cancellations and achieve cost savings of **30,000 USD**, while maintaining customer satisfaction and operational efficiency.

