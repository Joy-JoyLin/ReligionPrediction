# Predicting Religion Based on National Flag
> Ahmed Raza, Andrea Rosell, Andre Wood, Jose Garcia, Zhuoying 'Joy' Lin, Krithi Bojja, Lokesh Ramamoorthi, Stephen Bishop

## Executive Summary

Although religion is a very controversial and sensitive matter for a country and its people, it holds an equal importance for companies that want to do business in that country. McDonalds had to redesign their menu to remove the Big Mac in order to cater for the Indian market, which consists of Hindu majority. Other companies that include solicitation through female models have to change their marketing strategy, since that strategy won't be useful for the Islamic republican countries. 

For our project, we decided to use a dataset, which was available through the UCI website, called '[Flags](http://archive.ics.uci.edu/ml/machine-learning-databases/flags/flag.data)'. The dataset has a total of 26 variables, and we used these variables to predict the religion of a country, since some countries do not declare their religion(s). The dataset consisted of other variables like landmass and population, which were unrelated to the flag features. Therefore, we eliminated those variables and formed the models based on the remaining variables. We also found that by combining Christianity and Catholicism we were able to improve our predictions. This is because these two religions are more similar than not and was throwing off our success rates.

After cleaning the dataset, and confirming that there are no 'null' variables, we decided to use several models, which include LDA, QDA, GLM, Classification and Regression Trees, Bagging, and Random Forests. LDA and QDA failed to work since these models only work on continuous variables, and the flags dataset has non-continuous variables. The rest of the models worked fine. The results of the models that were applied and ran successfully are summarized in the table on the right.

Since we had six religions to predict, plus one as 'others', we were looking for a success rate of 1 in 7, or 14 percent. Our best model, as can be seen in the table, is Random Forest with a CP of .1 and depending on the seed, this would range from 50-60%. The particular seed we used was 316 and the CER was 0.5721649.

<p align="center">
  <img src="Executive%20Summary.png">
</p>

 
## Introduction
        
Throughout the world, *religion* is one of the most important thing that decides how people live their lives and how they act. If a company can determine the religion of its new target audience, it can do a much better job deciding whether it should enter the area, or how to tailor their products. For example, beef selling and consumption is restricted to only a few regions in India, since in Hindu religion, cow is considered as a sacred animal. Based on that fact, McDonalds had to redesign its menu to offer Veggie Big Macs compared to a Big Mac made of beef. This is one of the many examples where businesses had to redesign their flagship product to cater to a certain demographic based on *religion*.

Of course, gathering census information on a population’s religion is extremely difficult given that religion is such a controversial and sensitive issue in today’s society, and therefore, census information may not be that reliable. But what if, based on certain markers, we can predict their religion, and understand our targets better? That marker is a '*countries flag*'. A country’s flag is a symbol of pride. It is what the whole world will see, and therefore it must be in adherence to the beliefs of the mass majority of the population. Because of this, we think we should be able to predict a country’s religion based on the characteristics of their flag. 

To solve this we chose a data set from the UCI Machine Learning Repository called Flags. The issue of understanding the clients is extremely important. Any information that can be generated to gain a better information about the target market, provides an edge over the competition, and could prevent a company from making a costly mistake. In this paper we will discuss how we went about acquiring the data, cleaning it, analyzing it, interpreting it, and what did we find from this process.

## Data Description

As previously mentioned, the data set we chose to use was the Flags dataset from the UCI Machine Learning Repository.  Fortunately, the data from the UCI website was tailored for the classification approach and because of that we did not need to do much cleanup of the data. One thing we did was we had to change the name of the row because the data was split into separate files, one for the actual data and the other for the headers of the column. For example the data headings were named V1, V2, to Vn. So we ran some code in R so as to change the headers to the proper names of the column. For example, V1 was replaced by religion, V2 was replaced by color, and so on. We also made the decision to combine two of the religion classifications, Christianity and Catholicism. We did this because it makes sense that our model would get these two religions confused some of the time because they are more similar than not; when we combined the religions our results improved.

The dataset also had variables that are not related to the flag. These variables include landmass, zone, area, population, and language. Therefore, we discounted these variables and only used the variables related to the flags. A summary of data characteristics is as below:

<p align="center">
  <img src="Data%20Description.png">
</p>

As we can see, the data set we chose goes nicely with our classification problem, and even has no missing values. The data set is also widely used, and we believe we can discover something that others have missed in the past, which is another reason why we have selected this dataset. One problem that we will discuss later on is that some of the predictor variables came in binary form (1 for present, 0 for absent) while others were in colors. This had an adverse effect on some of our models and forced us to scrap two of the models.

## Methodology Description

After we cleaned the data, we decided to use 6 different models in our analysis LDA, QDA, GLM, Tree, Bagging, and Random Forests. Immediately after running our code we realized that LDA and QDA would not work on our dataset because the data set is small. LDA and QDA work well with continuous data and our data is not continuous. Also in our data set, we had colors as data for some of the variables, which did not work well for LDA and QDA. Next we tried to limit our variables by doing variable reduction and ran into similar problems and due to that we did not include lasso or ridge analysis in our analysis.

With those methods eliminated we focused on the methods like GLM, Trees, Bagging, and Random Forests because these models work well with classification data. For Trees, Bagging and Random Forests, we ran with different tuning parameters to ensure as accurate tree as possible, without over fitting the data. But we found that the tuning parameter did not change the results much inside of the model. We than used a leave one out cross validation method to test each of our models. We chose this method because our data set was not very large or complex and would not require massive amounts of computing time. We then ran each of our models with a seed of 316, formed our predictions, created a table, and then created a table summarizing our result and created the CER which we used as our measure of success. Below, we discuss the models we used to create our predictions model, and we also discuss why we chose these models:

###### Generalized Linear Models (GLM):

The generalized linear model (GLM) is a flexible generalization of ordinary linear regression that allows for response variables that have error distribution models other than a normal distribution. The purpose of GLM is to give a general framework for regression. GLM makes the following assumptions regarding the data structure:
1.	Independence of each data points
2.	Correct distribution of the residuals
3.	Correct specification of the variance structure
4.	Linear relationship between the response and the linear predictor

Our data set had independent data points and also there was a linear relationship between the response and the predictor, which is the first and fourth assumption. Hence we decided to try GLM.

###### Classification and Regression Trees

Trees create a model based on yes/no questions to a set of predictor variables to predict some response variable. Trees are simple, easy to understand and robust. The main reason for choosing Regression trees is that they are resistant to outliers and also they work well with data sets having large number of variables. Our data set had 26 variables and hence we thought that Regression trees would work well with our data.

###### Bagging 

Bagging is a machine learning ensemble meta-algorithm designed to improve the stability and accuracy of machine learning algorithms used in statistical classification and regression. Bagging reduces the variance associated with prediction by splitting the data into bags and the combining it all together which improves the prediction. Since our dataset had 26 variables, we thought Bagging would help us decrease the variance and predict better.

###### Random Forests

Random forests are an ensemble learning method for classification, regression and other tasks, that operate by constructing a multitude of decision trees at training time and outputting the class that is the mode of the classes (classification) or mean prediction (regression) of the individual trees. Though Random forests are similar to trees, but Random Forests produces two additional pieces of information:
1.	a measure of the importance of the predictor variables
2.	a measure of the internal structure of the data (the proximity of different data points to one another)
 
## Predictive Performance
In our data set, we have 6 religions plus "other" which is a total of 7 categories (We combined Christianity and Catholicism). Before we began running our models we decided on a criteria that would tell us if it is worth using any of our models or a criteria to tell if they actually improved upon a random choice, our criteria was: Any success rate of more than 14% is better than random picking. The reason we used a random guess is because the purpose of this is to predict and any improvement from that means that the analysis can provide benefit. Our best model, which is the Random Forest model with a CP of .1 using a seed of 316 is predicting with a success rate of 0.5721649  and hence we can say that our model is doing a good job relative to the measure we selected to compare it to. Depending on the seed though the particular model selection based on the CP or the decision between Random Forest and Bagging might change. In overall though, Random Forest and Bagging generated the best results and sometimes alternated based on the seeds selected with Random Forest performing best in general.

## Conclusion

From our analysis, we found that Random Forests worked best for our data set. It had a success percentage of 0.5721649. Given the complexity of our problem, none of our models predicted above 60% but each of the ones we got to run each performed better than a random guess so that was encouraging. We even increased our CER percentages by combining Christianity and Catholicism. We took away some good lessons from out project. One such lesson is that not all models work for all situations even if the model is supposed to address a certain issue, for example, when LDA, QDA, Ridge, and Lasso failed to work for us. We also learned that it is important to actually understand the data. If we had not looked into the individual elements of the data we would not have been able to eliminate non- flag features and this would have adversely affected our models. Another thing we learned was that we may need to use our own judgment in formatting the given data to improve results, for example when we combined Christianity and Catholicism. We also learned, that not all prediction problems will give us a 95% prediction rate and that is okay, so long as there is a basis to judge whether the model gives an improvement over a random guess. Even though this is not an easy problem to solve, given that we couldn't get the CER to be above 60%, we still can conclude that running different model analysis can improve our ability to predict a country's religion based on their flag, which could improve a firm’s ability to compete in foreign markets.
