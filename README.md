
# Nottingham University Hospitals NHS Trust Overnight Bed Occupancy Rate Forecast

![download](https://user-images.githubusercontent.com/34876902/204103802-7db9a70b-07ba-4dd4-8a2c-e0e0647fe1cc.png)

### Problem Statement
This problem was created based on the data available from the NHS statistics [(link here)](https://www.england.nhs.uk/statistics/statistical-work-areas/bed-availability-and-occupancy/).
The official problem statement for this is “Can we accurately forecast the overnight bed occupancy rate for Nottingham University Hospitals?”

### Background

Bed occupancy rate has remained as the most important parameter to evaluate the utilisation of hospitals.
It is a management indicator that provides information on the hospital’s service capacity, helping to assess whether there are missing or empty beds and to know about the usability of the spaces. 

Why is it important?  Bed maintenance is an expensive process for the hospital, involving cleaning, disinfection, and maintenance costs. In this context, it is important to have accurate and quality information, to ensure that the investments involved are better utilized and reduced within the possible limits. As reference, a general ward cost per bed day £586.59, where an ICU cost per day is £1621.16 
(from https://www.ncbi.nlm.nih.gov/pmc/articles/PMC7045184/#R26).

From the data of Overnight Bed Availability and Occupancy Data available from the NHS Statistics website, we can obtain the data of the Nottingham University Hospitals NHS Trust from June 2010 to September 2022. With it, we can attempt to train machine learning models to predict the occupancy of the next quarter corresponding to December 2022, and save costs by reducing expenses.

### Goal

Accurately forecast the overnight bed occupancy rate for Quarter December 2022 via Machine Learning.
 Ultimately, we want to find ways we can use these predictions for the Trust to utilise resources better. The effectiveness of our predictions will determine what kinds of things our predictions can be used for.

### Methods

A total of 50 datapoints composed the dataset, 4 each year since 2010 and 2 of 2022.We trained an ARIMA and Prophet Models, and compared them via MAPE, RMSE and MAE as well as visually.

### Results 
The results of the validation set were:
 Model|mean_absolute_error|mean_absolute_percentage_error|root_mean_squared_error|
-----------|---------|---------|---------|
ARIMA|0.016693|1.904301|0.018286|
Prophet|0.015123|1.72885|0.020611|

The propher model seems to adjust better in the first third, understimate in the middle and overestimate at the end. On the other hand, the ARIMA model underestimates across all the points.
For the Q3 of 2022: 

-The ARIMA model predicts a decrease of bed occupancy of -0.0022 % in regards to Q2. 

-The Prophet model predicts an increase of bed occupancy of 0.0281 % in regards to Q2.

### Recommendation

The model can be improved with information such as the day-only beds reports, information of occupancy of nearing hospitals in the Midlands area (if a hospital is full patients will be fererred and transfered), seasonal epidemiologic information and others. With these complementary sources,  more complex models for multivariate-time series can be used.

If the reports of the daily, weekly or monthly occupancy were available, there would be more data points to train models and thus obtain better results. With a more robust model, it could be used by other NHS-listed Hospitals to forecast their own overnight bed occupancy.

In the future, it could incorporate routines that deal with possible NaNs, Outliers, zeros and other possible distortions in the dataset.

### Risks and Assumptions

**Note for 2020-21 data**  "Hospital capacity has had to be organised in new ways as a result of the pandemic to treat Covid and non-Covid patients separately and safely in meeting the enhanced Infection Prevention Control measures. This results in beds and staff being deployed differently from in previous years in both emergency and elective settings within the hospital. As a result, caution should be exercised in comparing overall occupancy rates between this year and previous years. In general hospitals will experience capacity pressures at lower overall occupancy rates than would previously have been the case."

With this in mind, we restrict the training and validation sets of the model to be from 2010 up to Q4 of 2019.

