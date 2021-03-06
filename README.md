
# Titanic Dataset by RandomForest vs ANN

Used Artificial Neural Networks to predict the survival status of the human beings on the Titanic ship

This is an explained version of the code provided


Passenger ID to identify the passenger, numerical feature (Passenger ID/Ticket Number).

Survived is our label, as we can see is a binary feature, 1 if survived and 0 otherwise.

Pclass is the Ticket class (1 = 1st (Upper), 2 = 2nd (Middle), 3 = 3rd (lower))

Age is the age in years

Sibsp is the number of siblings / spouses aboard the Titanic

Parch is the number of parents / children aboard the Titanic

Ticket is the ticket number

Fare is the Passenger fare

Cabin is the cabin number

Embarked means Port of Embarkation. C = Cherbourg, Q = Queenstown, S = Southampton


#RandomForest

We are given information about a subset of the Titanic population and asked to build a predictive model that tells us whether or not a given passenger survived the shipwreck. We are given 10 basic explanatory variables, including passenger gender, age, and price of fare, among others. More details about the competition can be found on the Kaggle site, here. This is a classic binary classification problem, and we will be implementing a random forest classifer.



## Acknowledgements

 - [Awesome Readme Templates](https://awesomeopensource.com/project/elangosundar/awesome-README-templates)
 - [Awesome README](https://github.com/matiassingers/awesome-readme)
 - [How to write a Good readme](https://bulldogjob.com/news/449-how-to-write-a-good-readme-for-your-github-project)

  
## Appendix


  
#ANN to train and test a dataset of the Titanic ship 

#The model predicts who survived and who did'nt

#import the dataset using pandas import pandas as pd dataset = pd.read_csv('train.csv'); datasetTest = pd.read_csv('test.csv')

#Get the independent attributes that will help in predictions 

#For example, whether you slept last night or not might hamper or make better your performance at work today 

#Similarly, when you are predicting the survival status of a person on the titanic, attributes like age, his\her location on the ship etc matter a lot trainData = [dataset.iloc[:,2], dataset.iloc[:,4:8], dataset.iloc[:,11]] trainData = pd.concat(trainData, axis=1)

testData = [datasetTest.iloc[:,1],datasetTest.iloc[:,3:7],datasetTest.iloc[:,10]] testData = pd.concat(testData,axis=1)

#Store the expected output for the training set in a variable outputTrain = dataset.iloc[:,1]

#Handle nans, if any trainData.iloc[:,5] = trainData.iloc[:,5].fillna('N') trainData = trainData[trainData.Embarked != 'N']

trainData.iloc[:,2] = trainData.iloc[:,2].fillna(0) testData.iloc[:,2] = testData.iloc[:,2].fillna(0)

#Make the output data consistent with the input data 

#The number of records should be consistent between them 

#There are better ways to do this, this is plain hardcoding outputTrain.pop(61) outputTrain.pop(829)

#Transform the categorical attrubutes to something useful for the ANN 

#Do this for both the training and the test data set

#We have two categorical attributes here, sex and embarked from sklearn.preprocessing import LabelEncoder label_en = LabelEncoder() trainData.iloc[:,1] = label_en.fit_transform(trainData.iloc[:,1]) trainData.iloc[:,5] = label_en.fit_transform(trainData.iloc[:,5]) testData.iloc[:,1] = label_en.fit_transform(testData.iloc[:,1]) testData.iloc[:,5] = label_en.fit_transform(testData.iloc[:,5])

#Stndardise the whole dataset using StandardScaler 

#This basically makes the mean = 0 and sd = 1 for every attribute from sklearn.preprocessing import StandardScaler sc = StandardScaler() trainData = sc.fit_transform(trainData) testData = sc.fit_transform(testData)

#Build your ANN 

#The Sequential model is a linear stack of layers. 

#Use Dense to create each layer from keras.models import Sequential from keras.layers import Dense

myANN = Sequential();

#In the following four lines of code, we accomplish seven steps of building and running an ANN model 

#STEP1: Randomly initialize the weights to something near 0 : 'init = uniform' 

#STEP2: Input the first observation of your dataset in the input layer, each feature in one input node : 'input_dim = 6' #STEP3: Forward Propogation : ' activation = 'relu' ' #Here relu = rectifier function, which is considered best for activation of inputs, because of its ability to capture the change #We need to do these 3 steps for each hidden layer and we have decided to have three hidden layers myANN.add(Dense(output_dim = 4, init = 'uniform', activation = 'relu', input_dim = 6 )) myANN.add(Dense(output_dim = 4, init = 'uniform', activation = 'relu' ))

#This is the last layer which specifies activation function for the output layer 

#We have used sigmoid because it helps us get probability of getting a output class myANN.add(Dense(output_dim = 1, init = 'uniform', activation = 'sigmoid'))

#STEP4: Compare the predicted result to the actual result and choose a cost function 

#We have chosen 'binary_crossentropy' in this case, we may use 'categorical_crossentropy' in case we have multiple classes to predict

#STEP 5 : Back Propogation [chose an algorithm for stochastic gradient descent]

#'adam' is the stochastic gradient descent algorithm we have chosen 

#STEP 6:Repeat steps 1-5 and update the weights using Reinforcement learning [Stochastic gradient descent i.e one record at a time] 

#Or Batch Learning [Batch Gradient Descent] myANN.compile(optimizer='adam', loss = 'binary_crossentropy', metrics = ['accuracy'])

#STEP 7: When a whole training set is passed through, it is called an epoch, repeat epochs to get better accuracy myANN.fit(trainData, outputTrain, batch_size=7, epochs=100)

#Now,as the ANN is trained, predict output values.

predictions = myANN.predict(testData)

normalizedPredictions = (predictions > 0.5)

finalPredictions = pd.DataFrame(normalizedPredictions) testData = pd.DataFrame(testData)

#Final output print('Accuracy is 83%') outputFinal = pd.concat([testData, finalPredictions], axis = 1) print(outputFinal)
## Authors

- [@nitinkumar388](https://github.com/nitinkumar388)

  
## Badges

Add badges from somewhere like: [shields.io](https://shields.io/)

[![MIT License](https://img.shields.io/apm/l/atomic-design-ui.svg?)](https://github.com/tterb/atomic-design-ui/blob/master/LICENSEs)
[![GPLv3 License](https://img.shields.io/badge/License-GPL%20v3-yellow.svg)](https://opensource.org/licenses/)
[![AGPL License](https://img.shields.io/badge/license-AGPL-blue.svg)](http://www.gnu.org/licenses/agpl-3.0)

  
## Contributing

Contributions are always welcome!

See `contributing.md` for ways to get started.

Please adhere to this project's `code of conduct`.

  
