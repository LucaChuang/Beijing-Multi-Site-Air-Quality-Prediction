# Beijing-Multi-Site-Air-Quality-Prediction

Author: Team 1
* 2863031 Yunan Chen
* 2863088 Shen-Wei Chuang
* 2868872 Simeng Deng
* 2854110 Zhuo Chen

## Data source: 

We merged two datasets： 

1. Beijing Multi-Site Air-Quality Data Set - Shunyi District
https://www.kaggle.com/sid321axn/beijing-multisite-airquality-data-set
2. Airport weather observations - ZBAA Beijing(in Shunyi District）
https://mesonet.agron.iastate.edu/request/download.phtml?network=CN__ASOS

## Literature Review
There are many kinds of pollution on the Earth. Among varieties of pollution, air pollution is more prominent than others because people are breathing air all the time. Nowadays, as air pollution becomes severer and severer, more and more countries start paying attention to it. During the process of development, it is easy for the country to focus on the speed but to ignore environment pollution. As a result, air pollution issues are more serious in developing countries. In fact, the most polluted cities in the world are mostly in developing countries such as India and Pakistan <sup>[1]</sup>. China is also one of them. First, according to developing countries list in 2020 <sup>[2]</sup>, China is a developing country due to its low GDP per capita. Second, previously China’s air pollution was nearly unmanageable because of fast speed of its development. With people's awareness of environmental protection, air pollution has been one of the hottest topics in China for many years.

PM 2.5 is one of the most harmful air pollutants. PM 2.5 is atmospheric particulate matter that have a diameter of less than 2.5 micrometers <sup>[3]</sup>. It is an important factor to evaluate air quality. Besides, PM 2.5 can be harmful to human health. Exposure to PM2.5 pollution is considered to be an important risk factor of cardiovascular and cerebrovascular disease, respiratory damage, and lung cancer <sup>[4]</sup>. In addition, it might cause injury from free radical peroxidation, imbalanced intracellular calcium homeostasis and inflammatory injury, in turn to cause dangerous diseases. Diseases above seem to exist widely among elder people <sup>[5]</sup>. However,  in fact, PM 2.5 can hurt the health of young children as well <sup>[6]</sup>. What is more, PM 2.5 also affects economic welfare significantly. According to woPol scenario, PM2.5 pollution would lead to 2% of GDP loss and 210 billion CNY of health expense in China in 2030. Besides,  <sup>[7]</sup>. Thus, it's really important to control the PM 2.5 pollution.

China has succeeded in governing PM 2.5 issues from 2013 when China’s government started the war against PM 2.5 <sup>[8]</sup>. However, the policy is unlikely to result in further reductions in PM 2.5 and more ambitious policies are required <sup>[9]</sup>. To make contributions to this issue, this paper made models for prediction of PM 2.5 to forecast the concentration of PM 2.5 in next 24 hours, making it possible for government to remind people of harmful air quality and suggest wearing masks in outdoors. This could help reduce the overall exposure to PM 2.5.

According to previous analysis, PM 2.5 are strongly linked to weather variables such as temperature, relative humidity, wind conditions and air quality data such as SO2, NO2, etc. <sup>[10]</sup>. Hence, we collect weather data to build our models based on RNN for time series to predict real time concentration of PM 2.5.

In conclusion, as a result of future analysis needed for solving PM 2.5 issues in China, we collect weather and air quality data, and make models based on RNN to predict PM 2.5 concentration in next 24 hours.


## Data Dictionary
The **ASOS network whether data** is collected in Beijing Capital International Airport(ZBAA) which located at Shunyi district, so we enrich this dataset with **Beijing Municipal Environmental Monitoring Center data** for Shunyi district. 


**Target variable**:
*   The Concentration of PM 2.5: Fine inhalable particles, with diameters that are generally 2.5 micrometers and smaller.

**Shunyi Air-quality observation**:

*   PM10:  Inhalable particles, with diameters that are generally 10 micrometers and smaller
*   SO2: SO2 concentration (ug/m^3)
*   NO2: NO2 concentration (ug/m^3)
*   CO: CO concentration (ug/m^3)
*   O3: Ozone concentration (ug/m^3)
*   TEMP: temperature (degree Celsius)
*   PRES: pressure (hPa)
*   DEWP: dew point temperature (degree Celsius).
*   RAIN:precipitation (mm)
*   WD: wind direction
*   WSPM: wind speed (m/s)

**ASOS Network whether observation:**

*   relh: Relative Humidity in %
*   p01i: One hour precipitation for the period from the observation time to the time of the previous hourly precipitation reset. 
*   vsby: Visibility in miles


## Results and Model Comparasion

Below is the table showing general performance(mae) of each model: 

|Model|Discription| Train_mae |Test_mae|1st hour-Pred_mae|12nd hour - Pred_mae|24th hour-Pred_mae|
|:----:|:----:|:----:| :----: |:----:|:----:|:----:|
|1|baseline|59.76|59.76|-|-|-|
|2|Model1|35.91|40.50|20.83|41.46|53.06|
|3|Model2|45.99|45.40|46.36|45.98|55.20|
|3|Model3|40.29|41.94|34.72|41.61|54.67|


*   Our objective is to predict the PM2.5 concentration in the next 24 
hours more accurately. 
*   model1,model2 and model3 all perform better than the baseline model, but model1 have many negative prediction results, which are impossible in reality.
*   Compared with model1, model2 and model3 predict mostly postive results but the overall mae for test data increase by 4.9 in model2 and by 1.44 in model3.
*   All the models perform better when predicting PM 2.5 in the near hours. As shown in the table, 1st hour prediction is better than 12nd hour prediction. 12nd hour prediction is better than 24th hour prediction.
*   Considering the overall accuracy and reality restriction, we choose model3 as our final model. The government could apply this model to do a PM 2.5 real-time forecast for the next 24 hours and guide citizens in advance to avoid exposure to PM 2.5 pollution. 


## Conclusion

*   Data Gathering: We found our original data from kaggle, then use the data from ASOS to enrich our original data.
*   Preprocessing: Merge data base on time value, then clean data. Since we want to use 24 hours data to predict next 24 hours concentration of PM2.5, we shift our tar back ward 1 postion to let the model predict the right value.
*   Feature Engineering: Split our X and Y data, used the define function to process our data. In this case, we can use 24 hours data to predict next 24 hour.
*   Modeling: build a simple LSTM and a complex stacked LSTM model with convd and maxpooling layer. Comparing the performance of those 2 model.
*   Business problem: By forcasting the concentration of PM2.5, we can understand the air quality of the next 24 hour. In this case, people can stay indoor or wear mask when concentration of PM2.5 is high to prevent from potential air pollution inhaled.


## Reference

[1] Most polluted cities in the world.

https://www.iqair.com/us/world-most-polluted-cities

[2] Developing countries list in 2020.

https://worldpopulationreview.com/country-rankings/developing-countries

[3] Definition of PM 2.5

https://blissair.com/what-is-pm-2-5.htm#:~:text=Thank%20you.-,PM2.,be%20seen%20with%20a%20microscope.

[4] Yang Guan, Lei Kang, Yi Wang, Nan-Nan Zhang, Mei-Ting Ju, Health loss attributed to PM2.5 pollution in China's cities: Economic impact, annual change and reduction potential, Journal of Cleaner Production, Volume 217, 2019, Pages 284-294, ISSN 0959-6526, https://doi.org/10.1016/j.jclepro.2019.01.284.

[5] Xing, Y. F., Xu, Y. H., Shi, M. H., & Lian, Y. X. (2016). The impact of PM2.5 on the human respiratory system. Journal of thoracic disease, 8(1), E69–E74. https://doi.org/10.3978/j.issn.2072-1439.2016.01.19.

[6] Holst Gitte J, Pedersen Carsten B, Thygesen Malene, Brandt Jørgen, Geels Camilla, Bønløkke Jakob H et al. (2020) “Air pollution and family related determinants of asthma onset and persistent wheezing in children: nationwide case-control study” BMJ 370:m2791 doi: 10.1136/bmj.m2791

[7] Yang Xie, Hancheng Dai, Yanxu Zhang, Yazhen Wu, Tatsuya Hanaoka, Toshihiko Masui, Comparison of health and economic impacts of PM2.5 and ozone pollution in China, Environment International, Volume 130, 2019, 104881, ISSN 0160-4120, https://doi.org/10.1016/j.envint.2019.05.075.

[8] China’s success in dealing with PM 2.5 issues.

https://www.hindustantimes.com/delhi-news/how-china-managed-to-consistently-reduce-pm-2-5-concentrations-in-recent-years/story-dtWOaWt6JyMrHyJgCCxA4L.html

[9] Yue, H., He, C., Huang, Q. et al. Stronger policy required to substantially reduce deaths from PM2.5 pollution in China. Nat Commun 11, 1462 (2020), https://doi.org/10.1038/s41467-020-15319-4.

[10] Weeberb J. Requia, Iny Jhun, Brent A. Coull, Petros Koutrakis, Climate impact on ambient PM2.5 elemental concentration in the United States: A trend analysis over the last 30 years, Environment International, Volume 131, 2019, 104888, ISSN 0160-4120, https://doi.org/10.1016/j.envint.2019.05.082.

