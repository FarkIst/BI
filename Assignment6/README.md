# Assignment 6 for Business Intellegence Course
## Basic Machine Learning

## Part 1: Predicting Hackernews Points With Linear Regression in One Variable
### 1.1- Data preprocessing

![alt text](https://github.com/grimetone/BI/blob/master/Assignment6/img/HackerNews_Plot.png "HackerNews Karma Progression Plot")

The plot confirms our hypothesis. There is a clear downtrend in the amount of karma-points in newer accounts, with the natural expection of some outliers.

### 1.2 - Model selection

We will be using the `Linear Regression` model. This model estimates sparse coefficients and can be successful when sources of data are less than 100,000 units. This linear regression is also is useful for predicting a quantity. There are only two variables so we can use this model.

### 1.3 - Model training

`
model = LinearRegression()
x_val = df1['created'].values.reshape(-1, 1)
y_val = df1['karma'].values 

#Split into training and test set. 80-20
X_train, X_test, y_train, y_test = train_test_split(x_val, y_val, test_size=0.2, random_state=0)

regressor = LinearRegression()  
#here we train the algo
regressor.fit(X_train, y_train) 

print(regressor.intercept_)
print(regressor.coef_)

y_pred = regressor.predict(X_test)`

### 1.4 - Model Validation

1.

When we print out the regression coefficient we get `-3.73534337e-05` or `-0.0000373534337` which means for every second that increases, the karma points will decrease by 0.00003%. 

2.

![alt text](https://github.com/grimetone/BI/blob/master/Assignment6/img/PredictorModel.png "Training Data")

Here we have a plot of our training data. The predictive line is centered nicely. 

![alt text](https://github.com/grimetone/BI/blob/master/Assignment6/img/FullModel.png "Full Plot")

Here we have a full plot with all of our data with just the predictive line.

3.

When we plot the equation `t_1000 = (1000 - model.intercept_) / model.coef_[0]` into the pandas we get 
`Timestamp('2016-05-22 13:10:56.026025057')` or `1463922656` unix seconds. 

When you subtract the current epox time from that(1571696765 -  1463922656)  you should get around 107,774,109 seconds  which is around 1,247 days from now.

4. 

`Actual	Predicted

0	596.0	6693.205444

1	5497.0	3002.947069

2	204.0	11897.468077

3	5503.0	559.629722

4	9.0	-150.663451

5	9924.0	8879.785133

6	14022.0	1992.969240

7	608.0	6833.189641

8	1040.0	1929.380883

9	12558.0	5574.542794

10	2599.0	7945.127925

11	1713.0	8886.303755

12	839.0	6017.491876

13	5519.0	6067.948147

14	2324.0	7644.855027

15	130.0	2871.015376

16	5643.0	6863.012211

17	1351.0	7437.489158

18	1588.0	4200.592546

19	421.0	2864.496418

20	36691.0	6873.288851

21	3973.0	7802.211410

22	985.0	1526.232146

23	26037.0	6397.153857

24	72.0	-434.718086

25	3.0	-224.841842

26	5042.0	4776.013601

27	27759.0	8456.902614

28	649.0	2332.124672

29	1815.0	10096.638007`

Here we show a sample of our machine learning testing itself on the 20% of the HackerNews JSON data not included in our training data. The models prediction seems to be quite off.

Mean Absolute Error: 4167.507217090202

Mean Squared Error: 60489353.90798358

Root Mean Squared Error: 7777.490206228715

The root mean squared error is very high, suggesting a high residual variance. More sample data is recommended. 

## 2. Predicting Hackernews Points With Multivariate Linear Regression

	Coefficient

created	-0.000007

submitted	2.709600

Here we can see the coefficients for the two variables. For every decrease in seconds the karma points decreases by 0.000007  and for every submission there is an increase in karma by ~2.7.

     Actual     Predicted

2615    596.0   1300.877731

296    5497.0   6843.389891

7443    204.0   2054.710945

2343   5503.0   8668.199300

5564      9.0   -387.965699

5314   9924.0  11395.384411

33    14022.0  12194.341306

5335    608.0   1949.318375

2103   1040.0   2105.876616

8075  12558.0   6960.099947

8627   2599.0   3821.572273

7404   1713.0   3197.309592

4617    839.0   2054.278888

1149   5519.0  10354.750028

8750   2324.0   2721.541435

390     130.0    219.022976

39     5643.0   5580.138893

7270   1351.0   2394.235825

5648   1588.0   1978.769419

6301    421.0    729.962325

31    36691.0  22140.357341

4624   3973.0   7047.331174

4706    985.0    415.576442

1065  26037.0  33513.431102

6737     72.0   -406.652311

Here we show a sample of our machine learning testing itself on the 20% of the HackerNews JSON data not included in our training data. The models prediction is a lot closer using multiple linear regression.


MEA: 1718.8780099769258

MSE: 17351701.441963457

Root Mean Squared Error: 4165.537353327114

The root mean squared error is very high, suggesting a high residual variance. However it is about half of what it was previously when we only used the creation date variable. This shows that our data more than likely doens't have a linear relationship. More sample data is recommended.


(1000 - model.intercept_ + -0.000007 * #{unix_time}) / (-2.709600)

You would need `6967.04573757315` posts if one was to register ones account on : 2016-05-22 13:10:56.026025057.


If we were to set the posts variable to 500 we can use the following formula to see how long it would take to get 1000 karma points: 
(1000 - model.intercept_ + 2.709600 * 500) / -0.000007

Which equals to `1039378362` unix seconds 
or 
`~12,029 Days`

## 3. Prediction of breast cancer malignity

### 3.1 - Looking at the data

`0	1	2	3	4	5	6	7	8	9	...	22	23	24	25	26	27	28	29	30	31

0	842302	M	17.99	10.38	122.80	1001.0	0.11840	0.27760	0.3001	0.14710	...	25.38	17.33	184.60	2019.0	0.1622	0.6656	0.7119	0.2654	0.4601	0.11890

1	842517	M	20.57	17.77	132.90	1326.0	0.08474	0.07864	0.0869	0.07017	...	24.99	23.41	158.80	1956.0	0.1238	0.1866	0.2416	0.1860	0.2750	0.08902

2	84300903	M	19.69	21.25	130.00	1203.0	0.10960	0.15990	0.1974	0.12790	...	23.57	25.53	152.50	1709.0	0.1444	0.4245	0.4504	0.2430	0.3613	0.08758

3	84348301	M	11.42	20.38	77.58	386.1	0.14250	0.28390	0.2414	0.10520	...	14.91	26.50	98.87	567.7	0.2098	0.8663	0.6869	0.2575	0.6638	0.17300

4	84358402	M	20.29	14.34	135.10	1297.0	0.10030	0.13280	0.1980	0.10430	...	22.54	16.67	152.20	1575.0	0.1374	0.2050	0.4000	0.1625	0.2364	0.07678`


There are `569 rows × 32 columns`. There are a lot of columns to consider. The column I was able to distinguish is the column on index 1 which most likely describes whether the patients' tumor is malignant(M) or benign(B).

### 3.2 - Building the model

![alt text](https://github.com/grimetone/BI/blob/master/Assignment6/img/histogram_plots.png "Plotting inputs")

These models can help us to choose a column indexes with strong correlation to the benignity or malignancy of the patient.

Going just by these models we choose indexes 16, 30 as the data is very localized indicating causation.

`Accuracy of Logistic regression classifier on training set: 0.72
Accuracy of Logistic regression classifier on test set: 0.71`

Our accuracy was quite poor choosing these two, other indexes provided much better results and choosing all of the indexes resulted in even greater predictions as seen below.

With a full set using logistical regression we were able to get very high accuracy rates: 
`Accuracy of Logistic regression classifier on training set: 0.97`
`Accuracy of Logistic regression classifier on test set: 0.96`

### 3.3 - Evaluating the model

I would argue that the data is balanced to an extent as we are presented with an fairly even number of benign and malignant data samples. I am not sure it the lack of healthy data sets will skew the data as seen below. 

![alt text](https://github.com/grimetone/BI/blob/master/Assignment6/img/cancer_count.png "Count")

ROC and Precision-Recall Curves are used for evaluating a prediction model. 
ROC curves plot the false hit rate vs the hit rate and are best used when classes are balanced., as opposed to Precision_recall Curves which are best suited for unbalanced sets. As we have come to the conclusion that the data is reasonably balanced, we reason that ROC is best used for this prediction model.