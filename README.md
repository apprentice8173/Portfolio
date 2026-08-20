# Portfolio
## Project 1 - Predicting F1 pit speed
### Project Background

Developed a logistic regression model to predict whether an F1 pit stop was going to be fast or slow using python. The model was build from two open F1 dataset using features like stint, tyre life, and driver demographics.

Before starting the analysis I created a correlation chart to see what columns might be helpful for analysis. You can see that circuitid has the highest correlation and hopefully will be useful for analysis. 

![Correlation Chart](/images/confusion_martix.png)

The confusion matrix is an easy way to see the results of the analysis. Here you can see that the model works best for predicting true negative (slow) outcomes.

![Confusion Matrix](/images/confusion_martix1.png)
