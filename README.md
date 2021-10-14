# X12-ARIMA-ICEEMDAN-FCM-FTS

Introduction
=======
This is a python implementation of a hybrid model X12-ARIMA-ICEEMDAN-FCM-FTS, which consists of dual decomposition and an improved fuzzy time series method.

Methods
=======
The main methods involved and the overall framework of the developed hybrid forecasting model are X12-ARIMA (a popular seasonal adjustment method developed by the United States Census Bureau), ICEEMDAN (an improved complete ensemble empirical mode decomposition with adaptive noise ), FCM(the fuzzy C-means algorithm) and FTS( the fuzzy time series algorithm).

Installation
=======
1.EVIEWS 
---
A software software for implementing X12-ARIMA. Of course, you can also implement X12-ARIMA with other software.
Download link: http://www.eviews.com/home.html

2.PyEMD
---
A package contains many EMD variations.
GitHub repo: https://github.com/laszukdawid/PyEMD

3.pyFTS 
---
A package of the Fuzzy Time Series methods.
GitHub repo: https://github.com/PYFTS/pyFTS

Example
======
Take “ENG17.csv” as an example, the data of the preceding 11 years (132 observations) are used as training set, while the following year (12 observations) as testing set.

1.X12-ARIMA
----
Considering the seasonal characteristics of the tourist arrivals data, first the original time series (the "volume" column) is decomposed by X12-ARIMA method implemented by EVIEWS , extracting the seasonal component  (the "sea" column) and obtaining the seasonally adjusted series (the "seares" column).

2.ICEEMDAN
----
ICEEMDAN is then used to decompose the seasonally adjusted series (the "seares" column) into n-1 intrinsic mode functions ( the "CIMF1" column, the "CIMF2" column ,...,  the "CIMFn-1" column) with different time scale features and one smooth residual series (the "CIMFn" column), in order to reduce the data complexity.
(Refer to "ICEEMDAN.ipynb" for details)

3.Prediction of the seasonal factors series
----
The seasonal component  (the "sea" column)  can be split into data in the form of separate months （the "M1" column, the "M2" column, …, the "M12" column）.For example, the "M1" column consists of the seasonal component for January of each year, the "M2" column consists of the seasonal component for February of each year, and so on. Then we can use the seasonal component of the preceding 11 years to forecast the seasonal component of the following year by FCM-FTS method.
(Refer to "FCM-FTS.ipynb" for details)

4.Prediction of n-1 IMFs component series and the residual series 
----
The FCM-FTS method is used to model and predict the n-1 IMFs component series( the "CIMF1" column, the "CIMF2" column ,...,  the "CIMFn-1" column), and the residual series(the "CIMFn" column), respectively.
(Refer to "FCM-FTS.ipynb" for details)

5.Getting the final prediction results
----
Finally, the predicted values for all the components are linearly summed up to get the final prediction results.
(Refer to "FCM-FTS.ipynb" for details)


