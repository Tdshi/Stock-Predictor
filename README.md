### Abstract 

 In this project, I aim to build a predictive model to forecast the future price of the NYSE stock index based on historical price data and returns. By using a decision tree as the primary predictive model, I will capture non-linear relationships and interactions between the predictors. Specifically, I will apply a regression tree to model the complex fluctuations in stock prices and assess the accuracy of the predictions. To evaluate the model's performance, I will use Mean Squared Error (MSE) and R-squared to compare the results to those of more traditional linear models. The goal is to identify the key variables that influence the price of the NYSE and refine the model to produce precise and accurate results. 

 

### Introduction 

 Understanding the market and the various factors that influence it is essential for any Economics student. Gaining knowledge of how markets are shaped by different predictors provides valuable insights into market analysis and enhances confidence when navigating markets and consumer behavior in real-life situations. In our age of online banking and trading, it is crucial to understand the fluctuations of stock prices. Predicting stock prices and market prices are central to effective financial planning and decision making, enabling economists, investors, and policymakers to make wise, informed decisions. I will use a regression tree to predict the future price of the NYSE based on lagged returns, past prices, and price change data over time. Using a decision tree is an ideal way to capture non-linear relationships in financial data, furthering our understanding of market fluctuations. By gaining accurate NYSE price predictions, this project aims to precisely predict future market movements, which can help financial decision making and risk management. The following sections will discuss the methodology, review similar projects, and present and explore the results.  

 

### Methodology 

 The data used in this model is a sample of 691 NYSE price observations sourced from the Wooldridge data sets, specifically focusing on daily stock prices and returns. The sample data is sourced from a period of multiple years with key predictor variables that includes: 

Price – The daily stock price index of the NYSE. 

1 Day Staggered Price – The stock price from the previous day. 

2 Day Staggered Price – The stock price from 2 days ago. 

Return – The change in % for stock price from one day to the next. 

Staggered Return – The return from the previous day. 

These predictor variables will serve in the decision tree as the determinants for the price predictor. The key outcome variable will be the future stock price of the NYSE. 

For this model, a regression tree is the most effective method for capturing the non-linear relationship between the predictor variable and the outcome variable. This is especially important when attempting to predict future stock prices as relationships in stock market data are often not linear. Unlike a traditional regression model, a regression tree does not require assumptions about the form of the relationship between the predictor variables and the dependent variables. Regression trees continuously separate data to best reduce the variance of the outcome variable, making it an ideal choice when predicting a complex variable such as future NYSE stock price. Unlike a linear regression model, the regression tree does not assume linearity providing greater flexibility in modeling the interactions between the different variables.  

Before we start to build our model, it is important to clean and filter our data to ensure that data is not skewed or misleading in any way. To do this, we must set up criteria to omit data. We will omit data that has any missing or incomplete variables to ensure our outcome variable is not biased. Further, we must scale numerical data to be in the same range to increase the performance of the decision tree algorithm.  

The decision tree also requires training to allow it to learn and test the accuracy of the test. To do this, as we do not have infinite data, we must split the data to ensure we have enough data to train the model, while also reserving data for testing. For this, I will use a 70-30 split, with 70% of the data being used to train the decision tree mode, while the other 30% is used to test the model. Having a split that is majority training is important to have as much data as possible used to increase the model’s predictive power, while maintaining enough data to ensure that the tests are still unbiased and are reliable. The training data teaches the model the relationships between the predictor variables and the outcome variable with the test data being used to determine how well the model can evaluate ‘unseen’ data. 

The main component of the methodology is training the model. A regression tree works by splitting data into subsets based on the values of the predictor variables. With each split of data, the model attempts to minimize the variance of the outcome variable in each subset. This process is continuously repeated until the data reaches a pre-determined maximum depth (number of splits) or if the data can no longer be split effectively. To ensure the data does not overfit the model, we must set up certain parameters: 

Maximum depth – a predetermined number of layers or splits of data. A higher maximum depth allows for more precise predictions however can overfit the model. To calculate this, I will test various values from 5-10 and choose the value with the most balanced low error and generalization. 

Minimum samples per node – This is the minimum number of sample values required to form a node. This ensures that data does not split into nodes that are too small. We will find this value by testing the minimum samples per node before the data overfits the model. I will test values from 10-20. 

With these parameters, it ensures that the model can make consistent and accurate predictions. 

To ensure validity and accuracy of the model, we must set up tests. For a regression tree, commonly two different metrics are used to test accuracy: 

Mean Squared Error (MSE) - The MSE measures the average squared difference between the actual and predicted values of the outcome variables. A lower MSE is a sign of higher accuracy, showing that values are closer to the actual values. 

R-Squared Value (R^2) - This value measures the proportion of variance in the outcome variable explained by the model, with a R-squared value closer to 1 being a sign of a more accurate model, and a R-squared value closer to 0 indicates a poor fit and less accurate model. 

In addition to the regression tree model, I will also build a linear regression model to test against. A linear regression model assumes a linear relationship between the predictor variables and the outcome variable, which in theory, should be less accurate than the regression tree model. By comparing the linear regression model to the regression tree model, we can assess whether the added complexity of the regression tree model yields more accurate results. 

In conclusion, using the test measures and the parameters discussed, the regression tree model should prove to be a reliable and efficient predictor of future NYSE stock prices by capturing the relationship between predictor variables and the outcome variable. 

 

### Results 

 Using the methodology outlined above, after importing the library and cleaning the data by replacing the nan values. I renamed the columns to ensure that my code is easily recognizable and readable, identifying the outcome variable as ‘price’. The goal of the regression tree was to predict the price of NYSE stock using a set of predictor variables and determine if the predictor was accurate.  

First, I set up the model to get a prediction of the price based on the predictor variables. To do this, I set up the 70-30 split with 483 samples going towards training the model and 207 samples going towards testing the model. This ensured that the model would not give biased results when testing and the model had enough results to train to give accurate predictions. 

To ensure the regression tree would predict accurately and the model would fit, the first step was to set up the model parameter. As outlined in the methodology, the parameters to ensure that the model would fit were to test the maximum depth and the minimum samples per leaf. To find the optimal value for both, we must find the value that balances low error and generalization. To calculate this, we can use the gridsearch tool from the sklearn library. The best model configuration with maximum depth was 20 layers, and the minimum samples per leaf was 1 sample. This means that the data was allowed to split 20 times before the data would overfit the model and each node required 1 sample to form meaning nodes smaller than one sample size could not be created. 

I then set up a linear model to test against the regression model to evaluate benefits of a regression tree over a standard linear model. As the linear model assumes a linear relationship between the predictors and the outcome variable, parameters did not need to be set, and I could set up the performance analysis of both models on the test set. The outlined test statistics in the methodology were identified as MSE and R-squared. As stated in the methodology, an R-squared value closer to 1 is more accurate. The regression model reported an R-squared value of 0.997 which shows that the regression tree is very accurate as it is very close to 1. The regression tree also reported an MSE value of 5.929. However, the linear regression model had a 0.9996 R-squared value but only a 0.595 MSE value. The R-squared value explains 99.7% of the variance in price in the regression tree. The linear model’s R-squared value shows that 99.9% of the variance in price is explained by the linearity of the relationship with the predictor variables. The linear model also has a lower MSE value which means the linear model variable made fewer errors and captured the majority of the underlying trends affecting price. The next comparison carried out between the linear regression can be seen in the residuals. Below are the results of the residuals for both models. 
We can see that the regression tree better shows homoscedasticity, a sign of more accurate and less biased results.  

More analysis was done to test the reliability and accuracy of the regression tree, I compared the expected values of the model to the prediction data created by the model. Most of the values run across the line, showing the regression tree model predicting almost every single value as we would expect it to. Further, as seen in the feature importance graph, price_1 makes up almost all of the variance of outcome variable, with price_2 also having a negligible amount of influence over the variance over the outcome variable. 

In conclusion, if interpretability and simplicity are more important, the linear model is a better model. It captures most of the variance of price and is easier to understand, it also makes less mistakes because of the lower MSE and the R-squared value is closer to 1. However, the regression is also very accurate, and if the predictors had a more even distribution of effect of variance on the outcome variable, would be more accurate than the linear model. The relationship between the predictors and outcome variable was linear, being different to the hypothesis that the regression tree would be more accurate due to the high complexity of the outcome variable. In future models, some improvement could be made. Firstly, the accuracy of a model increases with sample size, with a relatively small sample size, there is a higher chance that anomalies or trends occur that the model cannot predict. Further parameter tuning may also increase the number of layers in data and provide a clearer and more accurate picture in the future. In the future, if revisiting the same model, using predictors that have larger effects on the outcome variable would provide more desired results. 