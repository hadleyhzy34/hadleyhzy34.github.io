---
layout: post
title: Logistic Regression
key: 20200913
tags:
  - pytorch
  - machine learning
  - python
---

## Logistic Regression
___

### Introduction to logistic Regression
___
This article discusses the basics of Logistic Regression and its implementation in Python. Logistic regression is basically a supervised classification algorithm. In a classification problem, the target variable(or output), y, can take only discrete values for given set of features(or inputs), X.

Contrary to popular belief, logistic regression IS a regression model. The model builds a regression model to predict the probability that a given data entry belongs to the category numbered as “1”. Just like Linear regression assumes that the data follows a linear function, Logistic regression models the data using the sigmoid function.
<!--more-->
### Logistic Regression Model
___
![sigmoid](https://raw.githubusercontent.com/hadleyhzy34/pytorch/master/resources/sigmoid.png)

### Logistic Regression Math
___
#### Datasets
___
* The datasets has p feature variables and n observations
* The feature matrix is represented as:

<img src="http://www.sciweavers.org/tex2img.php?eq=x%3D%20%5Cbegin%7Bbmatrix%7D1%20%26%20%20x_%7B11%7D%20%20%26%20...%20%26%20x_%7B1p%7D%5C%5C1%20%26%20%20x_%7B21%7D%20%20%26%20...%20%26%20x_%7B2p%7D%5C%5C...%20%26%20%20...%20%20%26%20...%20%26%20...%7D%5C%5C1%20%26%20%20x_%7Bn1%7D%20%20%26%20...%20%26%20x_%7Bnp%7D%20%5Cend%7Bbmatrix%7D%20&bc=White&fc=Black&im=jpg&fs=12&ff=arev&edit=0" align="center" border="0" alt="x= \begin{bmatrix}1 &  x_{11}  & ... & x_{1p}\\1 &  x_{21}  & ... & x_{2p}\\... &  ...  & ... & ...}\\1 &  x_{n1}  & ... & x_{np} \end{bmatrix} " width="192" height="86" />

Here, <img src="https://latex.codecogs.com/svg.latex?x_{ij}" title="x_{ij}" />
denotes the values of jth feature for ith observation.
 <img src="https://latex.codecogs.com/svg.latex?x_{ij}" title="x_{ij}" />
represents the predicted response for ith observation, where ith observation can be represented as follows:
<img src="http://www.sciweavers.org/tex2img.php?eq=%20%5Coverrightarrow%7Bx_%7Bi%7D%20%7D%20%3D%5Cbegin%7Bbmatrix%7D%20x_%7Bi1%7D%20%5C%5C%20x_%7Bi2%7D%20%5C%5C%20x_%7Bi3%7D%20%5C%5C.%20%5C%5C.%20%5C%5C.%20%5C%5C%20x_%7Bip%7D%5Cend%7Bbmatrix%7D&bc=White&fc=Black&im=jpg&fs=12&ff=arev&edit=0" align="center" border="0" alt=" \overrightarrow{x_{i} } =\begin{bmatrix} x_{i1} \\ x_{i2} \\ x_{i3} \\. \\. \\. \\ x_{ip}\end{bmatrix}" width="93" height="140" />   
<img src="https://latex.codecogs.com/svg.latex?h(  \overrightarrow{x_{i}})" title="x_{ij}" /> represents predicted response for ith response, the formula we use for calculating <img src="https://latex.codecogs.com/svg.latex?h(  \overrightarrow{x_{i}})" title="x_{ij}" /> is called hypothesis.   

#### Hypothesis for classificaiton
___
In linear regression, the hypothesis we used for prediction was:
<img src="http://www.sciweavers.org/tex2img.php?eq=h%28%20%20%5Coverrightarrow%7Bx_%7Bi%7D%7D%20%20%29%20%3D%20%20%20%5Cbeta%20_%7B0%7D%20%2B%20%5Cbeta%20_%7B1%7D%20x_%7Bi1%7D%20%2B%20%5Cbeta%20_%7B2%7D%20x_%7Bi2%7D%2B...%2B%20%5Cbeta%20_%7Bp%7D%20x_%7Bip%7D&bc=White&fc=Black&im=jpg&fs=12&ff=arev&edit=0" align="center" border="0" alt="h(  \overrightarrow{x_{i}}  ) =   \beta _{0} + \beta _{1} x_{i1} + \beta _{2} x_{i2}+...+ \beta _{p} x_{ip}" width="317" height="28" />

#### Modification on Linear Regression
some modifications are made to the hypothesis for classification:  
<img src="http://www.sciweavers.org/tex2img.php?eq=h%28%20%5Coverrightarrow%7B%20x_%7Bi%7D%20%7D%29%3D%20%5Cfrac%7B1%7D%7B1%2B%20e%5E%7B-%20%20%5Cbeta%20%5E%7BT%7D%20%5Coverrightarrow%7B%20x_%7Bi%7D%20%7D%7D%7D&bc=White&fc=Black&im=jpg&fs=12&ff=arev&edit=0" align="center" border="0" alt="h( \overrightarrow{ x_{i} })= \frac{1}{1+ e^{-  \beta ^{T} \overrightarrow{ x_{i} }}}" width="154" height="46" />

where regression coefficient vector be:
<img src="http://www.sciweavers.org/tex2img.php?eq=%5Coverrightarrow%7B%5Cbeta%7D%20%20%20%3D%20%5Cbegin%7Bbmatrix%7D%20%20%5Cbeta%20_%7B0%7D%20%20%5C%5C%20%5Cbeta%20_%7B1%7D%5C%5C%20%5Cbeta%20_%7B2%7D%5C%5C%20.%5C%5C%20.%5C%5C%20.%5C%5C%20%5Cbeta%20_%7Bp%7D%5Cend%7Bbmatrix%7D&bc=White&fc=Black&im=jpg&fs=12&ff=arev&edit=0" align="center" border="0" alt="\overrightarrow{\beta}   = \begin{bmatrix}  \beta _{0}  \\ \beta _{1}\\ \beta _{2}\\ .\\ .\\ .\\ \beta _{p}\end{bmatrix}" width="89" height="140" />

Note that 
 <img src="https://latex.codecogs.com/svg.latex?\beta _{0}" title="x_{ij}" />
 represents bias of linear regression hypothesis.

#### Conditional Probabilities based ith observations:
___
<img src="http://www.sciweavers.org/tex2img.php?eq=%20p%28y_%7Bi%7D%3D1%20%7C%20%20%5Coverrightarrow%7B%20x_%7Bi%7D%20%7D%2C%20%20%5Coverrightarrow%7B%20%5Cbeta%20%7D%20%29%20%20%3D%20h%28%20%5Coverrightarrow%7B%20x_%7Bi%7D%20%7D%20%29&bc=White&fc=Black&im=jpg&fs=12&ff=arev&edit=0" align="center" border="0" alt=" p(y_{i}=1 |  \overrightarrow{ x_{i} },  \overrightarrow{ \beta } )  = h( \overrightarrow{ x_{i} } )" width="194" height="29" />

<img src="http://www.sciweavers.org/tex2img.php?eq=%20p%28y_%7Bi%7D%3D0%20%7C%20%20%5Coverrightarrow%7B%20x_%7Bi%7D%20%7D%2C%20%20%5Coverrightarrow%7B%20%5Cbeta%20%7D%20%29%20%20%3D%201-h%28%20%5Coverrightarrow%7B%20x_%7Bi%7D%20%7D%20%29&bc=White&fc=Black&im=jpg&fs=12&ff=arev&edit=0" align="center" border="0" alt=" p(y_{i}=0 |  \overrightarrow{ x_{i} },  \overrightarrow{ \beta } )  = 1-h( \overrightarrow{ x_{i} } )" width="225" height="29" />

#### Compact form
___
<img src="http://www.sciweavers.org/tex2img.php?eq=p%28y_%7Bi%7D%20%7C%20%20%5Coverrightarrow%7B%20x_%7Bi%7D%20%7D%2C%20%20%5Coverrightarrow%7B%20%5Cbeta%20%7D%20%29%20%20%3D%20h%28%20%5Coverrightarrow%7B%20x_%7Bi%7D%20%7D%20%29%20%5E%7B%20y_%7Bi%7D%20%7D%20%281-h%28%20%5Coverrightarrow%7B%20x_%7Bi%7D%20%7D%20%29%29%20%5E%7B1-%20y_%7Bi%7D%20%7D&bc=White&fc=Black&im=jpg&fs=12&ff=arev&edit=0" align="center" border="0" alt="p(y_{i} |  \overrightarrow{ x_{i} },  \overrightarrow{ \beta } )  = h( \overrightarrow{ x_{i} } ) ^{ y_{i} } (1-h( \overrightarrow{ x_{i} } )) ^{1- y_{i} }" width="294" height="29" />

Note that yi represents the ith observation categorical target. Image ith observation categorical target is 1, then we need to maximize ith prediciton reponse as large as 1. While if ith observation categorical target is 0, we need to maximize <img src="https://latex.codecogs.com/svg.latex?1-h( \overrightarrow{ x_{i} } )" title="x_{ij}" />. In general, maximize <img src="https://latex.codecogs.com/svg.latex?p(y_{i} |  \overrightarrow{ x_{i} },  \overrightarrow{ \beta } )" title="x_{ij}" /> will fit more our model and obtain better result. Since x and y are observation values, we estimat the parameter <img src="https://latex.codecogs.com/svg.latex?\overrightarrow{ \beta } " title="x_{ij}" /> to maximizing this likelihood function:
<img src="http://www.sciweavers.org/tex2img.php?eq=L%28%20%5Coverrightarrow%7B%20%5Cbeta%20%7D%20%29%20%3D%20%5Cprod_i%5En%20h%28%20%5Coverrightarrow%7Bx_%7Bi%7D%7D%20%29%20%5E%7B%20y_%7Bi%7D%20%7D%20%281-h%28%20%5Coverrightarrow%7Bx_%7Bi%7D%7D%20%29%20%29%5E%7B%281-y_%7Bi%7D%29%7D&bc=White&fc=Black&im=jpg&fs=12&ff=arev&edit=0" align="center" border="0" alt="L( \overrightarrow{ \beta } ) = \prod_i^n h( \overrightarrow{x_{i}} ) ^{ y_{i} } (1-h( \overrightarrow{x_{i}} ) )^{(1-y_{i})}" width="281" height="50" />

Take log likelihood and obtain cost function:
<img src="http://www.sciweavers.org/tex2img.php?eq=J%28%20%5Coverrightarrow%7B%20%5Cbeta%20%7D%20%29%20%3D%20%20%5Csum_i%5En%20-%20y_%7Bi%7D%20h%28%20%5Coverrightarrow%7Bx_%7Bi%7D%7D%20%29%20-%20%281-y_%7Bi%7D%29%281-h%28%20%5Coverrightarrow%7Bx_%7Bi%7D%7D%20%29%29&bc=White&fc=Black&im=jpg&fs=12&ff=arev&edit=0" align="center" border="0" alt="J( \overrightarrow{ \beta } ) =  \sum_i^n - y_{i} h( \overrightarrow{x_{i}} ) - (1-y_{i})(1-h( \overrightarrow{x_{i}} ))" width="332" height="50" />


#### Using Gradient descent algorithm
___
<img src="http://www.sciweavers.org/tex2img.php?eq=%20%5Cfrac%7B%5Cpartial%20J%28%20%5Coverrightarrow%7B%20%5Cbeta%20%7D%20%29%7D%7B%5Cpartial%20%20%20%5Cbeta%20_%7Bj%7D%20%7D%20%3D%20%20%5Csum_i%5En%20%20x_%7Bij%7D%20%20h%28%20%5Coverrightarrow%7Bx_%7Bi%7D%7D%20%29%20-%20x_%7Bij%7D%20%20%5Cwidehat%7B%20y_%7Bi%7D%20%7D%20%3D%20%28h%28%20%5Coverrightarrow%7Bx%7D%20%29%20-%20%5Cwidehat%7B%20y%20%7D%29%20%5Cbullet%20%20%5Coverrightarrow%7B%20x_%7Bi%7D%20%7D%20&bc=White&fc=Black&im=jpg&fs=12&ff=arev&edit=0" align="center" border="0" alt=" \frac{\partial J( \overrightarrow{ \beta } )}{\partial   \beta _{j} } =  \sum_i^n  x_{ij}  h( \overrightarrow{x_{i}} ) - x_{ij}  \widehat{ y_{i} } = (h( \overrightarrow{x} ) - \widehat{ y }) \bullet  \overrightarrow{ x_{i} } " width="362" height="60" />

## Logistic Regression using python from scratch
___
### import modules


```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
from sklearn.linear_model import LogisticRegression
from sklearn.model_selection import train_test_split
```

### Prepare Data


```python
data = pd.read_csv('/Users/hadley/Documents/pytorch/resources/heart.csv')
data.head()
print(data.shape)
```

    (303, 14)



```python
#### Creating Dummy Variables for categorical variables
dummy1 = pd.get_dummies(data['cp'], prefix = "cp")
dummy2 = pd.get_dummies(data['thal'], prefix = "thal")
dummy3 = pd.get_dummies(data['slope'], prefix = "slope")
```


```python
data = [data, dummy1, dummy2, dummy3]
print(dummy1.shape, dummy2.shape, dummy3.shape)
```

    (303, 4) (303, 4) (303, 3)


currently data is still list object, not ndarray


```python
data = pd.concat(data, axis =1)
data.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>age</th>
      <th>sex</th>
      <th>cp</th>
      <th>trestbps</th>
      <th>chol</th>
      <th>fbs</th>
      <th>restecg</th>
      <th>thalach</th>
      <th>exang</th>
      <th>oldpeak</th>
      <th>...</th>
      <th>cp_1</th>
      <th>cp_2</th>
      <th>cp_3</th>
      <th>thal_0</th>
      <th>thal_1</th>
      <th>thal_2</th>
      <th>thal_3</th>
      <th>slope_0</th>
      <th>slope_1</th>
      <th>slope_2</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>63</td>
      <td>1</td>
      <td>3</td>
      <td>145</td>
      <td>233</td>
      <td>1</td>
      <td>0</td>
      <td>150</td>
      <td>0</td>
      <td>2.3</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>37</td>
      <td>1</td>
      <td>2</td>
      <td>130</td>
      <td>250</td>
      <td>0</td>
      <td>1</td>
      <td>187</td>
      <td>0</td>
      <td>3.5</td>
      <td>...</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>41</td>
      <td>0</td>
      <td>1</td>
      <td>130</td>
      <td>204</td>
      <td>0</td>
      <td>0</td>
      <td>172</td>
      <td>0</td>
      <td>1.4</td>
      <td>...</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>3</th>
      <td>56</td>
      <td>1</td>
      <td>1</td>
      <td>120</td>
      <td>236</td>
      <td>0</td>
      <td>1</td>
      <td>178</td>
      <td>0</td>
      <td>0.8</td>
      <td>...</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>4</th>
      <td>57</td>
      <td>0</td>
      <td>0</td>
      <td>120</td>
      <td>354</td>
      <td>0</td>
      <td>1</td>
      <td>163</td>
      <td>1</td>
      <td>0.6</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 25 columns</p>
</div>



drop previous categorical columns:


```python
data = data.drop(['cp', 'thal', 'slope'], axis=1)
data.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>age</th>
      <th>sex</th>
      <th>trestbps</th>
      <th>chol</th>
      <th>fbs</th>
      <th>restecg</th>
      <th>thalach</th>
      <th>exang</th>
      <th>oldpeak</th>
      <th>ca</th>
      <th>...</th>
      <th>cp_1</th>
      <th>cp_2</th>
      <th>cp_3</th>
      <th>thal_0</th>
      <th>thal_1</th>
      <th>thal_2</th>
      <th>thal_3</th>
      <th>slope_0</th>
      <th>slope_1</th>
      <th>slope_2</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>63</td>
      <td>1</td>
      <td>145</td>
      <td>233</td>
      <td>1</td>
      <td>0</td>
      <td>150</td>
      <td>0</td>
      <td>2.3</td>
      <td>0</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>37</td>
      <td>1</td>
      <td>130</td>
      <td>250</td>
      <td>0</td>
      <td>1</td>
      <td>187</td>
      <td>0</td>
      <td>3.5</td>
      <td>0</td>
      <td>...</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>41</td>
      <td>0</td>
      <td>130</td>
      <td>204</td>
      <td>0</td>
      <td>0</td>
      <td>172</td>
      <td>0</td>
      <td>1.4</td>
      <td>0</td>
      <td>...</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>3</th>
      <td>56</td>
      <td>1</td>
      <td>120</td>
      <td>236</td>
      <td>0</td>
      <td>1</td>
      <td>178</td>
      <td>0</td>
      <td>0.8</td>
      <td>0</td>
      <td>...</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>4</th>
      <td>57</td>
      <td>0</td>
      <td>120</td>
      <td>354</td>
      <td>0</td>
      <td>1</td>
      <td>163</td>
      <td>1</td>
      <td>0.6</td>
      <td>0</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 22 columns</p>
</div>



### Creating Model for logistic regression
___
split data into input observations and output observations


```python
y = data.target.to_numpy()
print(y.shape)
```

    (303,)



```python
x = data.drop(['target'], axis = 1)
print(x.shape)
```

    (303, 21)


### Normalize Data
___
normalize input observation data and add one more 'dummy' feature column so that bias calculation included here:


```python
x = (x - np.min(x))/(np.max(x)-np.min(x)).to_numpy()
bias_column = np.ones((x.shape[0],1))
x = np.append(bias_column, x, axis = 1)
print(x.shape)
```

    (303, 22)


Split data, 80% will be train data and 20% will be test data


```python
x_train, x_test, y_train, y_test = train_test_split(x,y,test_size = 0.2,random_state=0)
print(x_train.shape, x_test.shape, y_train.shape, y_test.shape)
```

    (242, 22) (61, 22) (242,) (61,)



```python
### Weight and Bias Initialization, note that n_features+1 represent weights w already included bias
n_samples = x_train.shape[0]
n_features = x_train.shape[1]
w = np.zeros((n_features,))
print(n_samples, n_features, w.shape)
```

    242 22 (22,)



```python
#model prediction: forward pass by using sigmoid function
def forward(x):
    z = np.dot(x, w)
    return 1/(1+np.exp(-z))
```

loss function based on maximum likelihood estimation


```python
def loss(y_train, y_predicted):
    loss = -(y_train*np.log(y_predicted) + (1-y_train)*np.log(1-y_predicted))
    return np.sum(loss)/y.shape[0]
```

### gradient of weight


```python
def gradient_weight(x,y_train,y_predicted):
    dw = np.dot((y_predicted - y_train).T, x)
    return dw

## training 
learning_rate = 0.01
n_iters = 100
```

### forward predict


```python
def forward_predict(x):
    z = np.dot(x, w)
    y_prediction =  1/(1+np.exp(-z))

    for i in range(y_prediction.size):
        if y_prediction[i] <= 0.5:
            y_prediction[i] = 0
        else:
            y_prediction[i] = 1
    return y_prediction
```

### Prepare for loss curve, number of iteration as x axis and loss as y axis


```python
plt_x = []
plt_y = []
```

### Training


```python
for epoch in range(n_iters):
    #prediction = forward pass
    y_pred = forward(x_train)

    #loss
    l = loss(y_train, y_pred)

    #gradients
    dw = gradient_weight(x_train, y_train, y_pred)

    #update wrights
    w -= learning_rate * dw

    plt_x.append(epoch)
    plt_y.append(l)

    if epoch % 1 ==0:
        print(f'epoch {epoch+1}: loss = {l:.4f}')
```

    epoch 1: loss = 0.5536
    epoch 2: loss = 0.4194
    epoch 3: loss = 0.3742
    epoch 4: loss = 0.3535
    epoch 5: loss = 0.3418
    epoch 6: loss = 0.3343
    epoch 7: loss = 0.3290
    epoch 8: loss = 0.3250
    epoch 9: loss = 0.3218
    epoch 10: loss = 0.3191
    epoch 11: loss = 0.3167
    epoch 12: loss = 0.3147
    epoch 13: loss = 0.3128
    epoch 14: loss = 0.3111
    epoch 15: loss = 0.3095
    epoch 16: loss = 0.3080
    epoch 17: loss = 0.3066
    epoch 18: loss = 0.3053
    epoch 19: loss = 0.3041
    epoch 20: loss = 0.3029
    epoch 21: loss = 0.3018
    epoch 22: loss = 0.3008
    epoch 23: loss = 0.2998
    epoch 24: loss = 0.2989
    epoch 25: loss = 0.2979
    epoch 26: loss = 0.2971
    epoch 27: loss = 0.2963
    epoch 28: loss = 0.2955
    epoch 29: loss = 0.2947
    epoch 30: loss = 0.2940
    epoch 31: loss = 0.2933
    epoch 32: loss = 0.2926
    epoch 33: loss = 0.2920
    epoch 34: loss = 0.2913
    epoch 35: loss = 0.2907
    epoch 36: loss = 0.2902
    epoch 37: loss = 0.2896
    epoch 38: loss = 0.2891
    epoch 39: loss = 0.2886
    epoch 40: loss = 0.2881
    epoch 41: loss = 0.2876
    epoch 42: loss = 0.2871
    epoch 43: loss = 0.2867
    epoch 44: loss = 0.2862
    epoch 45: loss = 0.2858
    epoch 46: loss = 0.2854
    epoch 47: loss = 0.2850
    epoch 48: loss = 0.2846
    epoch 49: loss = 0.2843
    epoch 50: loss = 0.2839
    epoch 51: loss = 0.2836
    epoch 52: loss = 0.2832
    epoch 53: loss = 0.2829
    epoch 54: loss = 0.2826
    epoch 55: loss = 0.2823
    epoch 56: loss = 0.2820
    epoch 57: loss = 0.2817
    epoch 58: loss = 0.2814
    epoch 59: loss = 0.2812
    epoch 60: loss = 0.2809
    epoch 61: loss = 0.2806
    epoch 62: loss = 0.2804
    epoch 63: loss = 0.2801
    epoch 64: loss = 0.2799
    epoch 65: loss = 0.2797
    epoch 66: loss = 0.2795
    epoch 67: loss = 0.2792
    epoch 68: loss = 0.2790
    epoch 69: loss = 0.2788
    epoch 70: loss = 0.2786
    epoch 71: loss = 0.2784
    epoch 72: loss = 0.2782
    epoch 73: loss = 0.2780
    epoch 74: loss = 0.2779
    epoch 75: loss = 0.2777
    epoch 76: loss = 0.2775
    epoch 77: loss = 0.2773
    epoch 78: loss = 0.2772
    epoch 79: loss = 0.2770
    epoch 80: loss = 0.2769
    epoch 81: loss = 0.2767
    epoch 82: loss = 0.2766
    epoch 83: loss = 0.2764
    epoch 84: loss = 0.2763
    epoch 85: loss = 0.2761
    epoch 86: loss = 0.2760
    epoch 87: loss = 0.2759
    epoch 88: loss = 0.2757
    epoch 89: loss = 0.2756
    epoch 90: loss = 0.2755
    epoch 91: loss = 0.2753
    epoch 92: loss = 0.2752
    epoch 93: loss = 0.2751
    epoch 94: loss = 0.2750
    epoch 95: loss = 0.2749
    epoch 96: loss = 0.2748
    epoch 97: loss = 0.2747
    epoch 98: loss = 0.2746
    epoch 99: loss = 0.2745
    epoch 100: loss = 0.2744


loss curve, loss function returned value with respect to number of iterations


```python
plt.plot(plt_x, plt_y, 'b')
plt.xlabel("number of epochs", fontsize=15)
plt.ylabel("MLE cost function", fontsize=15)
plt.rcParams["figure.figsize"] = (12,7)
plt.show()
```


    
![svg](https://raw.githubusercontent.com/hadleyhzy34/pytorch/master/resources/loss_curve_logistic_regression.png)
    


### manually calculate accuracy


```python
y_test_pred = forward_predict(x_test)
print("Manuel Test Accuracy: {:.2f}%".format((100 - np.mean(np.abs(y_test_pred - y_test))*100)))
```

    Manuel Test Accuracy: 85.25%


Final plot to check distance between predicted value and observation with repect to each feature


```python
x_linear = np.dot(x_test, w)
def sigmoid(x):
     return 1/(1+np.exp(-x))
print(x_linear)

t1 = np.arange(-5.0, 5.0, 0.1)
plt.plot(t1, sigmoid(t1), 'r')
plt.plot(x_linear, y_test_pred, 'bo')
plt.xlabel("number of epochs", fontsize=15)
plt.ylabel("MLE cost function", fontsize=15)
plt.rcParams["figure.figsize"] = (12,7)
plt.show()
```

    [-2.29420457 -0.06308867  0.04797952 -3.46814858 -2.0499066  -1.12642636
     -2.5685351  -2.41063596 -3.50555731 -4.49125426  0.60393739  2.5569347
     -3.00098277  2.30837334  3.2512419   1.25612815 -2.71948701  1.44747319
     -4.28088693  1.39343452  1.46533894 -1.24259217 -1.81542927 -1.63853973
      2.4237399   0.25793775 -1.76087883 -0.68070708  3.49235634  1.37801868
      1.25534473 -4.33003805  3.67578518  0.98659795  2.67926752  0.57409612
     -2.1883085   2.22040851 -1.85645047 -0.36110886 -0.50539455  1.48557235
      0.04146691 -1.75997446  0.44119235  1.63330185  1.78237282 -0.07312052
     -2.78411445  1.1278409   2.39580181  1.31927031  3.61757349  0.59014531
      4.81296128 -2.13979847  2.71081302  2.07815489  2.19097508  3.4580257
      1.06761226]



    
![svg](https://raw.githubusercontent.com/hadleyhzy34/pytorch/master/resources/sigmoid_result.png)