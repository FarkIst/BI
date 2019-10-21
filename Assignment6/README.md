# Assignment 6 for Business Intellegence Course
## Basic Machine Learning

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