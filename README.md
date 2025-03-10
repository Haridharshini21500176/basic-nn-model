# Developing a Neural Network Regression Model


## AIM
To develop a neural network regression model for the given dataset.


## THEORY
Neural networks consist of simple input/output units called neurons. These units are interconnected and each connection has a weight associated with it. Neural networks are flexible and can be used for both classification and regression. In this article, we will see how neural networks can be applied to regression problems.

Regression helps in establishing a relationship between a dependent variable and one or more independent variables. Regression models work well only when the regression equation is a good fit for the data. Although neural networks are complex and computationally expensive, they are flexible and can dynamically pick the best type of regression, and if that is not enough, hidden layers can be added to improve prediction.

Build your training and test set from the dataset, here we are making the neural network 3 hidden layer with activation layer as relu and with their nodes in them. Now we will fit our dataset and then predict the value.


## Neural Network Model
![224904957-962c297b-72c3-43f9-b361-22e9b7efb8b9](https://github.com/logeshwari2004/basic-nn-model/assets/94211349/96b14e99-21f1-45a6-b519-84677c27c181)


## DESIGN STEPS
### STEP 1:
Loading the dataset
### STEP 2:
Split the dataset into training and testing
### STEP 3:
Create MinMaxScalar objects ,fit the model and transform the data.
### STEP 4:
Build the Neural Network Model and compile the model.
### STEP 5:
Train the model with the training data.
### STEP 6:
Plot the performance plot
### STEP 7:
Evaluate the model with the testing data.
## PROGRAM
### Name:Haridharshini.S
### Register Number:212221230033
```
from google.colab import auth
import gspread
from google.auth import default
import pandas as pd
from sklearn.model_selection import train_test_split
from tensorflow.keras.models import Sequential
from tensorflow.keras.layers import Dense
from sklearn.preprocessing import MinMaxScaler
import matplotlib.pyplot as plt

auth.authenticate_user()
creds, _ = default()
gc = gspread.authorize(creds)

worksheet = gc.open('Student_Tables').sheet1
rows = worksheet.get_all_values()

df = pd.DataFrame(rows[1:], columns=rows[0])
df = df.astype({'Table':'int'})
df = df.astype({'Scores':'int'})
df.head()
x=df[['Table']].values
y=df[['Scores']].values

x_train,x_test,y_train,y_test=train_test_split(x,y,test_size=0.3,random_state=0)

scaler=MinMaxScaler()
scaler.fit(x_train)

x_t=scaler.transform(x_train)
x_t

ai=Sequential([
    Dense(8,activation='relu'),
    Dense(13,activation='relu'),
    Dense(1)
])

ai.compile(optimizer='rmsprop',loss='mse')

ai.fit(x_t,y_train,epochs=2000)

ai.fit(x_t,y_train,epochs=700)

loss_df=pd.DataFrame(ai.history.history)

loss_df.plot()

x_t2=scaler.transform(x_test)

ai.evaluate(x_t2,y_test)

err = rmse()
preds = ai.predict(x_test)
err(y_test,preds)

z=[[7]]

z_1=scaler.transform(z)

ai.predict(z_1)

```


## Dataset Information


![224903108-600c4ce3-42ef-44bd-b0e5-770bbc90a9c7](https://github.com/logeshwari2004/basic-nn-model/assets/94211349/b7874884-a671-499a-a30c-a36c999698d9)
## OUTPUT


### Training Loss Vs Iteration Plot
![224903390-501f127b-1536-4844-afe3-1dff611dae17](https://github.com/logeshwari2004/basic-nn-model/assets/94211349/6d8ac3a3-5c9b-428b-83d7-371c17ed7ac1)


### Test Data Root Mean Squared Error
![224903932-7e06c013-2f5a-4d10-97af-6a18c71b3072](https://github.com/logeshwari2004/basic-nn-model/assets/94211349/93c02d58-65d4-4e88-bc13-7a337a9608c5)


### New Sample Data Prediction
![224904405-6ec36239-184e-4c41-9d30-7e9010818ffa](https://github.com/logeshwari2004/basic-nn-model/assets/94211349/f4fa90ad-15b3-42d6-941f-cb4309a33a68)


## RESULT
Thus a neural network regression model for the given dataset is written and executed successfully.
