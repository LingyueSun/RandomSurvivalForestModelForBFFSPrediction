# RandomSurvivalForestModelForBFFSPrediction

library(randomForestSRC)

load("my_model.RData") # my_model.RData contains the random survival forest model named 'RF_fit_final' and a sample patient named 'SamplePatient'

PredictionForNewData = predict(RF_fit_final, newdata=SamplePatient)

SurvivlFunction = as.data.frame(t(rbind(PredictionForNewData$time.interest,PredictionForNewData$survival[1,])))
plot(SurvivlFunction, main = "Predicted Biochemcial Failure Free Survival", type='p',pch=16, xlab='Time in Years', ylab='Probability')
lines(lowess(SurvivlFunction, f=0.05), col = 2, lwd = 3)

# This outputs a figure showing the predicted biochemical failure free survival for the 
