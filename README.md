# Portfolio
## Project 1 - Predicting F1 pit speed
### Project Background

Developed a logistic regression model to predict whether a F1 pit stop was going to be fast or slow using python. The model was build from two open F1 dataset using features like stint, tyre life, and driver demographics.

### Correlation Chart

Before starting the analysis I created a correlation chart, as seen below, to see what columns might be helpful for analysis. You can see that circuitid has the highest correlation and hopefully will be useful for analysis. 

![Correlation Chart](/images/confusion_martix.png)

### Confusion Matrix

The confusion matrix, shown below, is an easy way to see the results of the analysis. Here you can see that the model works best for predicting true negative (slow) outcomes. The false positive and false negative outcomes are higher than I wanted so more improvements, like adding more variables, should be made before being used. 

![Confusion Matrix](/images/confusion_martix1.png)

### Recommendations

As this is only my second project in python I am proud that I created a predictive model with an accuracy of 67% and a f1-score of 61%. I would like to improve both scores to over 80% so that I can be more confident in the predictive element. I believe this to be a reasonable goal as F1 is always evolving with many impacting factors.  
