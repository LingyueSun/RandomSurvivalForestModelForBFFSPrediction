# RandomSurvivalForestModelForBFFSPrediction
## This is a sample code for using the model in R or R Studio
library(randomForestSRC)

load("my_model.RData") # my_model.RData contains the random survival forest model named 'RF_fit_final' and a sample patient named 'SamplePatient'

PredictionForNewData = predict(RF_fit_final, newdata=SamplePatient)

SurvivlFunction = as.data.frame(t(rbind(PredictionForNewData$time.interest,PredictionForNewData$survival[1,])))

plot(SurvivlFunction, main = "Predicted Biochemcial Failure Free Survival", type='p',pch=16, xlab='Time in Years', ylab='Probability')

lines(lowess(SurvivlFunction, f=0.05), col = 2, lwd = 3)

### This outputs a figure showing the predicted biochemical failure free survival for the sample patient. The black points are the predictions at time points of interest and the red line is a smooth fit of the black points.

![BFFSPredictionForSamplePatient](https://user-images.githubusercontent.com/56777354/157321898-93157176-feff-4df5-94a2-cd67f7769382.jpeg)

#### Note the variable settings for the sample patient:
#### "PSAatDiagnosis": PSA level at diagnosis, continuous variable         
#### "ClinicalTstage2": Clinical T stage at diagnosis, categorical variable, 3 levels: "T1 - T2a", "T2b - T2c", or "T3"    
#### "GleasonScore_Categ": Total Gleason Score at diagnosis, categorical variable, 3 levels: "6", "7", or "8andAbove"      
#### "PelvicRT_Technique_Categ": Pelvic irradiation technique used for EBRT, categorical variable, 4 levels: "2PhasePelvicIrrad", "DoseToProstDiffDoseToSV", "SinglePhaseToProst+/-SV", or "SIBPelvicIrrad"
#### "IGRT_Frequency2": The frequency for image guidance, categorical variable, 3 levels: "Daily", "MixedWeeklyAndDaily", or "Weekly"
#### "PTVprescCIV98": V98%[%] for high dose PTV, continuous variable         
#### "CTVpresc_D99": D99%[%] for high dose CTV, continuous variable   
####
