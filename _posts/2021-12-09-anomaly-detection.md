---
layout: post
title:  "NLP Web Application"
date:   2021-12-09
excerpt: "NLP application use case with TensorFlow framework"
project: true
tag:
- Condition Based Maintenance
- Anomaly Detection
- Data Mining
- Pattern Anomaly
- Alert
- Machine Learning
comments: true
---

# Project Description

Condition Based Maintenance (CBM) uses the sensor to collect real-time measurements (ie. pressure, temperature, and vibration). CBM data allows maintenance personnel to perform maintenance at the exact moment it is needed, prior to failure. This can be done by **Anomaly Detection** to detect machine failures. There are some types of anomaly detection [1-3]. In this project, using **Data Mining**. This approach can give patterns that are more informative and easier to understand. The patterns can be used further to trigger alerts for alerting machine failures. On the other hand, this approach is also quite light and does not require much time. So, it is considered suitable for solving anomaly detection problems in small datasets, such as the used dataset.


# Dataset Description  

The dataset is vibration sensor readings from NASA Acoustics and Vibration Database. sensor readings were taken on four bearings that were run to failure under constant load and running conditions. The vibration measurement signals are provided for the datasets over the lifetime of the bearings until failure. Failure occurred after 100 million cycles with a crack in the outer race.
![Plot Initial Data](https://github.com/m-nanda/Projects/raw/main/Anomaly%20Detection/img/Plot_Initial_Data.png "Plot Initial Data")


# Method

The idea behind this approach is adopted from the proposed framework in [4], but simpler and customizable according to the given dataset. The first step is to discretize the value of each sensor which indicates the sensor is in normal or failure condition. Then the results are clustered to find out the condition of the machine so that in the end a pattern can be obtained to give an early warning when the machine experiences signs of failure.

# Results  

## Rules  

Rules obtained for machine failures:

* Bearing 1: Failure, Bearing 2: Failure, Bearing 3: Failure, Bearing 4: Failure -> **Machine Failure Alert!**  
* Bearing 1: Normal, Bearing 2: Failure, Bearing 3: Failure, Bearing 4: Failure -> **Machine Failure Alert!**  
* Bearing 1: Normal, Bearing 2: Failure, Bearing 3: Failure, Bearing 4: Normal -> **Machine Failure Alert!**  
* Bearing 1: Failure, Bearing 2: Failure, Bearing 3: Normal, Bearing 4: Normal -> **Machine Failure Alert!**  
* Bearing 1: Normal, Bearing 2: Failure, Bearing 3: Normal, Bearing 4: Failure -> **Machine Failure Alert!**


## Bearing Status

![Plot Labeled Bearings](https://github.com/m-nanda/Projects/raw/main/Anomaly%20Detection/img/Plot_Labeled_Bearings.png "Plot Labeled Bearings")
From Bearing Status:

* It can be seen that **Bearing 1** is the first sensor that indicates failure. It doesn't, making the machine fail immediately. But, it might be considered as the root cause of machine failure.
* Machine start failure when Bearing 1 and Bearing 2 fail.


## Time Interval  

![Plot Result](https://github.com/m-nanda/Projects/raw/main/Anomaly%20Detection/img/Result.png "Plot Result")

By using the generated rules, it gives a time interval of **23 hours and 20 minutes** (since the first alert) before the machine is completely broken.


# References

[1] https://bhanushahi.medium.com/anomaly-detection-a7f28ccd5936

[2] https://medium.com/analytics-vidhya/anomaly-detection-in-python-part-1-basics-code-and-standard-algorithms-37d022cdbcff

[3] https://towardsdatascience.com/how-to-use-machine-learning-for-anomaly-detection-and-condition-monitoring-6742f82900d7

[4] Palembiya R.A., Setiawan M.N., Gultom E.O., Prayitno A.S.D., Kurniati N., Iqbal M. (2021) A Smart Predictive Maintenance Scheme for Classifying Diagnostic and Prognostic Statuses. In: Mohamed A., Yap B.W., Zain J.M., Berry M.W. (eds) Soft Computing in Data Science. SCDS 2021. Communications in Computer and Information Science, vol 1489. Springer, Singapore. https://doi.org/10.1007/978-981-16-7334-4_8  


[`Go to repo >>`](https://github.com/m-nanda/Projects/tree/main/Anomaly%20Detection)