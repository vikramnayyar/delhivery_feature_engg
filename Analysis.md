# 1.     Dataset Overview
## 1.2  Dataset Structure
- There are 11 Numerical cols
- There are 8 object cols
- There are 4 datetime cols
- One col is Boolean
- Source Name and Destination Names are redundant (and have few NaNs), Source IDs and Destination IDs represent same information
- Therefore, Source and Destination Names have been Dropped. There are no NaNs in DataFrame now.
 
## 1.2 Trips and Source Destination
- A trip can have multiple source destination pairs.
- There are no trips that have same Source and Destination, so Dataset is consistent in this aspect.
- There are a total of 2344 Source Destination pairs

## 1.3 Route Schedules and Trips
- Each Trip has a single Route Schedule
- A Route Schedule can have multiple Trips

## 1.4 Route Schedules with Source-Destinations
- 1761 Routes (Source-destination pairs) of 2344 Routes have 1 Route Schedule.
- 360 Routes of 2344 Routes (Source-destination pairs) have 2 Route Schedule.
- 103 Routes of 2344 Routes (Source-destination pairs) have 3 Route Schedule.

## 1.5 Trip Creation Dates
- We have data for 21 days from 12th Sept to 3rd Oct 2018. 
- Since we only have about 3 Weeks of Data, data is insufficeint for Weekly and Daily (Mon-Sun) will not be sufficient for analysis

## 1.6 Trip Creation Hours
- As expected, we have Data for all 24 hours

# 2.     Delivery Speeds
## 2.1 Cart Deliveries
### 2.2.1 Distribution & Outliers
- With skewness of 0.61, The Delivery speed is slightly right skewed
- Kurtosis of 3.57, Delivery Speeds are highly peaked, so they have large number of outliers
- QQ Plot also suggests there are Outliers in Delivery Speeds, the Distribution is near to Gaussian Distribution
- Shapiro Test is not valid, as total size of dataset is very large (>5000 rows)
- After Outlier removal, QQ suggests deviation from Normal Distribution.
- So the Distribution of delivery Speeds is not Normal.

### 2.2.2 Source-Destination Delivery Speeds
- With 0.034403742642202875 and 97% confidence, Delivery Speeds are Normal Distributed
- 17% deliveries are at Slow Speeds
- 71.3% deliveries are at Medium Speeds
- 11.7% deliveries are at Fast Speed
- Mean Delivery Speed is 0.45
- Top 10 Source Destination Pairs have Delivery Speeds in range of 0.8 to 0.9
- Skewness of 0.11, suggests Distribution peak is almmost at center.
- Kurtosis of -0.36 (negative Kurtosis) suggests Delivery speeds are more uniformly distributed across Source Destination Pairs.
- Efforts for increasing Delivery Speeds are required, as Avg Delivery Speeds have negative Kurtosis and Skewness is almost Centered
- With 99% Confidence, Confidence Interval of Average Delivery Speed (0.44, 0.47)

### 2.2.3 FTL Deliveries
- 7.3% deliveries are at Slow Speeds
- 71.8% deliveries are at Medium Speeds
- 20.9% deliveries are at Fast Speed

### 2.2.3 Source Destination Pairs With Top 10 Speeds
- Mean Delivery Speed is 0.52
- Top 10 Source Destination Pairs have Delivery Speeds in range of 0.93 to 1.16
- Skewness of 0, suggests Distribution peak is at the Center.
- Kurtosis of 0.18 (slightly positive Kurtosis) suggests Delivery speeds are more uniformly distributed across Source Destination Pairs.
- Efforts for increasing Delivery Speeds are required, as Avg Delivery Speeds have Kurtosis of 0.18 and Skewness is Centered.
- With 99% Confidence, Confidence Interval of Average Delivery Speed (0.52, 0.54)

## 2.3 Carting vs FTL
- 4.375818059065075e-30 and 99% confidence suggest that FTL Delivery Speeds are faster than Cart Deliveries

# 3.     OSRM Time vs Actual Time
## 3.1 Distribution
- Delivery Times are highly right skewed, taking Median Delivery times for aggregation will be suitable.
- Median of Actual Delivery Time is 42.
- Median of OSRM time is 34.
- Skewness of Time Difference in highly Positive (12.4), most of deliveries are completing in comparatively shorter time difference percentage from OSRM time.
- Kurtosis is highly Positive (265.65), suggesting most of deliveries are concentrated at shorter time difference percentage from OSRM time.
- But, Median Difference Percentage between OSRM Time and Actual Time is 92%, so there is still a vast difference between OSRM and Actual Time.
- Only 1.96% Deliveries matched to OSRM Time.
- Better strategies to meet OSRM time are required, or OSRM time reference is not practical for gauging Delivery Times.

## 3.2  Percent Delivery Times Closer to OSRM Time
- 3.6% Deliveries completed within 110% of OSRM Time
- 6.3% Deliveries completed within 120% of OSRM Time
- 9.7% Deliveries completed within 130% of OSRM Time
- There is significant deviation from of Delivery time from OSRM Time. Deliveries are clearly not meeting OSRM Time.

## 3.3  Delivery Time Factor
- Percent values that were Outliers: 2.9%
- Mean and Median are close by, we tested for Normal Distribution
- With 2.5177207375521852e-06 and 99% confidence, Delivery Factor Factor is Not Normal Distributed
- Most Deliveries are taking 192.9% of OSRM Time

## 3.4 Hypothesis Validation
- P-value of 7.848069340149569e-204 and 99% confidence suggest that Actual Time is larger than Median OSRM Time
 
# 4.     OSRM Distance vs Actual Distance
## 4.1 Distribution
- OSRM Distance and Actual Distance are Right skewed taking Median (on aggregation at Source-Distance Pair) will be appropriate.
- Median of Actual Delivery Distance is 9.02.
- Median of OSRM distance is 9.65.
- Median Difference between Actual Distance and OSRM Distance is -17%, so most deliveries are completing in smaller distance than OSRM Distance.
- Skewness of Distance Difference Percentage in Negative (-1.2), most of deliveries are completing closer to OSRM distance.
- Kurtosis of Distance Difference Percentage is Positive (2%), suggesting most of deliveries are concentrated closer to OSRM distance.
- 100% Deliveries completed in lesser distance than OSRM Distance.
- Delhivery is performing perfectly as per OSRM Distance.
 
## 4.2  Delivery Distance Factor
- Percent values that were Outliers: 2.8156996587030716%
- Most Deliveries are routing through 83.4% of OSRM Distance
- Performing Kruskal Test, P-value of 1.1598178598208581e-29 and 99% confidence suggest that Median Actual Distance is smaller than Median OSRM Distance
 
# 5. Trips Across Top 5 Route Schedules
- Percent Variation in Delivery Time for Route 1 thanos::sroute:0007affd-fd01-4cf0-8a4f-90419df059f7 : 427.76 %
- Percent Variation in Delivery Time for Route 2 thanos::sroute:00435307-de7f-4439-bd6a-5a2a9a3cd8bf : 223.97 %
- Percent Variation in Delivery Time for Route 3 thanos::sroute:00a74fab-a3ac-44df-b83a-cbf181b4cd94 : 60.89 %
- Percent Variation in Delivery Time for Route 4 thanos::sroute:00b294b8-d2c3-4bca-a3be-684f46278bdd : 81.98 %
- Percent Variation in Delivery Time for Route 5 thanos::sroute:01164881-301e-45f8-bacd-ee21c37f1cc4 : 283.07 %
- Percent Variation in Delivery Time for Route 6 thanos::sroute:011f94ad-57cf-4005-9734-f5b8a4d9cb59 : 18400.0 %
- Considering top 5 Route Schedules as sample, time taken by constituting Trips varies extremely.
- This should be controlled and efforts to maintain them consistent will significantly improve reliability and Customer Satisfaction.
