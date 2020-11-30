data <- read.csv("SomervilleHappinessSurvey2015.txt")
view(data)

str(data)

library(caret)
library(adabag)
library(e1071)
library(dplyr)

sapply(data, function(x) sum(is.na(x)))


data$X1 <- as.factor(data$X1)
data$X2 <- as.factor(data$X2)
data$X3 <- as.factor(data$X3)
data$X4 <- as.factor(data$X4)
data$X5 <- as.factor(data$X5)
data$X6 <- as.factor(data$X6)
data$D <- as.factor(data$D)


str(data)

indexes=createDataPartition(data$D, p=0.9, list = F)
train <- data[indexes,]
test<-data[-indexes,]
str(train)


model<- boosting(D~., data = train, boos = T, mfinal = 100)

prediksi<-predict(model, test)
confusionMatrix(prediksi$confusion)
