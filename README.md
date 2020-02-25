# Using Random Forest and Boosting methods to study the relations between biomechanical attributes with developing vertebral column diseases
Investigated the relations between biomechanical attributes as predictors with developing vertebral column diseases like Disc hernia or Spondylolisthesis

During the last decade, modern numerical methods and machine learning techniques like gradient boosting, bagging, random forest, trees, Support Vector Machines and Neural Networks have been applied vastly in many medical fields like cardiology, oncology, radiology, pathology, neurology genetic, biochemistry and etc. These methods by providing a reliable prediction models, can be helpful improving the disease diagnosis. Many studies have investigated different learning models and compared their efficiency and robustness in application.

The aim of this study is investigating and comparing the relations between biomechanical attributes as predictors with developing vertebral column diseases like Disc hernia or Spondylolisthesis, using statistical teqniques Random Forest and Boosting (AdaBoostM1). Then the performance and model fit of these methods will be compared to assess which one could be more successful explaining the data with less error.

####Data exploration


The summary statistics of data were provided. Shapiro-Wilk normality test were used and QQ-plots provided for assessing and testing the normality of variables. Correlations between variables were calculated using spearman correlation coefficient.  Chisq.out.test function available in {outliers} package were used investigating any possible outliers in data set. Regarding the histogram plot and the correlation matrix of predictors and coplot it seems that there are significant correlations especially between some of the variables like PelvicIncidence and SacralSlope. 

<img src="https://user-images.githubusercontent.com/57342758/73783659-ec8b7000-4748-11ea-8881-0eb9d034879d.png" width="400" height="400">

<img src="https://user-images.githubusercontent.com/57342758/73783665-f01ef700-4748-11ea-9430-696418936881.png" width="400" height="400">

<img src="https://user-images.githubusercontent.com/57342758/73783685-f44b1480-4748-11ea-82de-b0710b18ea25.png" width="400" height="400">


These two variables at different levels of outcome variable are highly correlated. Implementing Shapiro-Wilk normality test resulted p-value < 2.2e-16, so the null hypothesis is rejected. Also some outliers were recognized for each predictor variable having values out of the specified range (Table 1).  


<img src="https://user-images.githubusercontent.com/57342758/73783767-16449700-4749-11ea-83b8-418f7381160e.png" width="400" height="200">

#######Random Forest

Decision trees are one of most popular learning methods that are commonly used for data exploration. Decision tree is made by recursive partitioning that divides feature space into sets of disjoint rectangular regions based on splitting rules and stopping criteria. Decision trees generally have limitations like Low prediction accuracy and high variance. In the other hand, Random forest (or random forests) is an ensemble classifier that consists of many decision trees and outputs the class which is the mode of the classes resulted by individual trees. Random forest, in addition to provide more stable results it is also useful in the cases having outliers, complex interactions and nonlinear relations between predictors and outcome variable [7, 9]. In this study random forest technique was implemented using randomForest function available in {randomForest} package. Also tuneRF function available in {randomForest} package and train function in {caret} package were used to estimate best mtry which results respectively minimum OOB error and larger accuracy and kappa statistics values. The important variables resulted from RF method were identified and finally using varSelRF function in {varSelRF} package, and minimal depth variable selection, three most informative variables were selected.

Using tuneRF function and train function was resulted respectively minimum OBB error measure: 0.152103 and higher Accuracy and Kappa tuning parameter estimates (0.832 0.727) for mtry equal with 2.  The mtry then set to be 2 and Random Forest technique was implemented with ntreeTry=500. The important variables were identified. Regarding MeanDecreaseAccuracy; SacralSlope, PelvicRadius and DegreeSpondylolisthesis and PelvicTilt are the most important variables that their loses can decrease the accuracy considerably. Regarding the MeanDecreaseGini; SacralSlope, PelvicRadius, LumbarLordosisAngle and PelvicIncidence are the most important variables. 

<img src="https://user-images.githubusercontent.com/57342758/73784213-e77af080-4749-11ea-9b5c-44a20f4f1a48.png" width="400" height="400">

The Random Forest method was robust and could act better and have higher performance in compare to nominal regression method. The most important variables using varSelRF function and minimal depth variable selection also identified to be: SacralSlope, PelvicRadius and DegreeSpondylolisthesis[11, 13].

<img src="https://user-images.githubusercontent.com/57342758/73784295-11ccae00-474a-11ea-8bd3-cdf68f30bd27.png" width="400" height="400">



#######Boosting

Most boosting algorithms consist of iteratively learning weak classifiers and adding them to a final strong classifier. Dependent to the weak learner's accuracy, they will be weighted and after a weak learner is added, the data is reweighted. AdaBoost as one of the famous boosting algorithms is a machine learning technique for constructing a strong classiﬁer as linear Combination of simple weak classiﬁers. In the case of dealing with multi class (more than two classes) outcome there is a generalization to AdaBoost called Adaboost.M1. Adaboost.M1 algorithm which was proposed by Freund and Schapire in 1996 uses classification trees as single classifiers [8]. The function boosting available in {adabag} package provides weights as a vector of weight of trees of all iterations and vote matrix describing the number of trees that assigned each observation to each class. This method also outputs the importance of each variables based on the number of times that each of them are selected to split. The AdaBoost.M1 algorithm was implemented and also 5-fold cross validation was used and average error regarding the confusion matrix returned [9].  

The AdaBoost.M1 algorithm was implemented and weights and votes for classes were measured. Among the six variables SacralSlope, PelvicRadius, DegreeSpondylolisthesis and PelvicTilt with respectively coefficient: 16.00, 19.01754, 20.63158 and 16.35088 are more important. Implementing 5-fold cross validation resulted average error of the model = 0.1585761. Also providing a new data set (n=200) by sampling from main data with replacement and measuring the prediction error it was equal= 0. The AdaBossting algorithm is also robust and provides accurate results in the case of having outliers or collinearity and potential interactions [10]. 




