---
title: "Machine Learning Basics"
layout: post
date: 2019-05-05
tags: blog
comments: true
---

This is the first in a series of posts describing the basics of Machine Learning and application of machine learning to datasets. In subsequent posts, I will discuss more advanced analysis of data.

We will use the Iris dataset for our analysis. This can be found on the [UCI Machine Learning Repository](https://archive.ics.uci.edu/ml/datasets/iris). It includes three iris species with 50 samples each as well as some properties about each flower. One flower species is linearly separable from the other two, but the other two are not linearly separable from each other.
The columns in this dataset are:Id, SepalLengthCm, SepalWidthCm, PetalLengthCm, PetalWidthCm, and 
Species. Click [here](/assets/Python/Iris.csv) to download the csv format of the Iris dataset. 

Lets begin...

#### Import python packages
```python
import numpy as np
import pandas as pd
import seaborn as sns
import matplotlib.pyplot as plt
```

#### Load the Iris dataset
```python
iris = pd.read_csv("Iris.csv")
```

#### Information about the dataset
```python
iris.head() #show the first 5 rows from the dataset
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
      <th>Id</th>
      <th>SL: Cm</th>
      <th>SW: Cm</th>
      <th>PL: Cm</th>
      <th>PW: Cm</th>
      <th>Species</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>5.1</td>
      <td>3.5</td>
      <td>1.4</td>
      <td>0.2</td>
      <td>Iris-setosa</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>4.9</td>
      <td>3.0</td>
      <td>1.4</td>
      <td>0.2</td>
      <td>Iris-setosa</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>4.7</td>
      <td>3.2</td>
      <td>1.3</td>
      <td>0.2</td>
      <td>Iris-setosa</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>4.6</td>
      <td>3.1</td>
      <td>1.5</td>
      <td>0.2</td>
      <td>Iris-setosa</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>5.0</td>
      <td>3.6</td>
      <td>1.4</td>
      <td>0.2</td>
      <td>Iris-setosa</td>
    </tr>
  </tbody>
</table>
</div>
(SL: SepalLength, SW: SepalWidth, PL: PetalLength, PW: PetalWidth)



```python
#Inconsistency check: if no null values, then the data can be processed
iris.info() 
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 150 entries, 0 to 149
    Data columns (total 6 columns):
    Id               150 non-null int64
    SepalLengthCm    150 non-null float64
    SepalWidthCm     150 non-null float64
    PetalLengthCm    150 non-null float64
    PetalWidthCm     150 non-null float64
    Species          150 non-null object
    dtypes: float64(4), int64(1), object(1)
    memory usage: 7.1+ KB



#### Removing the unneeded columns


```python
# Drop Id column, axis=1: column wise, inplace =1: changes should be reflected into the dataframe
iris.drop('Id',axis=1,inplace=True) 
```

### Exploratory Data Analysis With Iris

#### Relationship between the sepal length and sepal width:

```python
fig = iris[iris.Species=='Iris-setosa'].plot(kind='scatter',x='SepalLengthCm',y='SepalWidthCm',color='orange', label='Setosa')
iris[iris.Species=='Iris-versicolor'].plot(kind='scatter',x='SepalLengthCm',y='SepalWidthCm',color='blue', label='versicolor',ax=fig)
iris[iris.Species=='Iris-virginica'].plot(kind='scatter',x='SepalLengthCm',y='SepalWidthCm',color='green', label='virginica', ax=fig)
fig.set_xlabel("Sepal Length")
fig.set_ylabel("Sepal Width")
fig.set_title("Sepal Length VS Width")
fig=plt.gcf()
fig.set_size_inches(10,6)
plt.show()
```
![png](/assets/images/output_7_0.png)


#### Relationship between the petal length and petal width:
```python
fig = iris[iris.Species=='Iris-setosa'].plot.scatter(x='PetalLengthCm',y='PetalWidthCm',color='orange', label='Setosa')
iris[iris.Species=='Iris-versicolor'].plot.scatter(x='PetalLengthCm',y='PetalWidthCm',color='blue', label='versicolor',ax=fig)
iris[iris.Species=='Iris-virginica'].plot.scatter(x='PetalLengthCm',y='PetalWidthCm',color='green', label='virginica', ax=fig)
fig.set_xlabel("Petal Length")
fig.set_ylabel("Petal Width")
fig.set_title(" Petal Length VS Width")
fig=plt.gcf()
fig.set_size_inches(10,6)
plt.show()
```
![png](/assets/images/output_9_0.png)


**Observation:**
* Petal Features are giving a better cluster division compared to the Sepal features.

#### Distribution of the length and width:

```python
iris.hist(edgecolor='black', linewidth=1.2)
fig=plt.gcf()
fig.set_size_inches(12,6)
plt.show()
```
![png](/assets/images/output_12_0.png)


#### Variation of length and width w.r.t. the species:

For this we make use of the violinplot, which shows density of the length and width in the species. 
1. Thinner part: less density
2. Fatter part: higher density

```python
plt.figure(figsize=(15,10))
plt.subplot(2,2,1)
sns.violinplot(x='Species',y='PetalLengthCm',data=iris)
plt.subplot(2,2,2)
sns.violinplot(x='Species',y='PetalWidthCm',data=iris)
plt.subplot(2,2,3)
sns.violinplot(x='Species',y='SepalLengthCm',data=iris)
plt.subplot(2,2,4)
sns.violinplot(x='Species',y='SepalWidthCm',data=iris)
plt.show()
```
![png](/assets/images/output_14_2.png)



### Task

The given problem is a classification problem, where the samples belong to two or more classes and we want to learn from already labeled data how to predict the class of unlabeled data.
We will use the classification algorithms to build a model.

ML notations:
1. _Attributes/Features_: a property of an instance that may be used to determine its classification. E.g. the petal and sepal length and width.
2. _Target Variable_: the variable that is or should be the output.E.g. the 3 flower species.

N.B. if the desired output consists of one or more continuous variables, then the task is called regression. An example of a regression problem would be the prediction of the length of a salmon as a function of its age and weight.

#### Import python packages for the classification algorithms
```python
from sklearn.linear_model import LogisticRegression  # Logistic Regression algorithm
from sklearn.cross_validation import train_test_split # Split the dataset for training and testing
from sklearn.neighbors import KNeighborsClassifier  # K nearest neighbours
from sklearn import svm  # Support Vector Machine (SVM) Algorithm
from sklearn import metrics # Check the model accuracy
from sklearn.tree import DecisionTreeClassifier # Decision Tree Algoithm
```


#### Correlation between features
When we train any algorithm, the number of features and their correlation plays an important role. If there are features and many of the features are highly correlated, then training an algorithm with all the featues will reduce the accuracy. Thus features selection should be done carefully.

```python
iris.shape #get the shape of the dataset
```
    (150, 5)

This dataset has less featues but still we will see the correlation.


```python
plt.figure(figsize=(7,4)) 
# Draw a heatmap with input as the correlation matrix calculted by(iris.corr())
sns.heatmap(iris.corr(),annot=True,cmap='cubehelix_r')
plt.show()
```
![png](/assets/images/output_21_0.png)

**Observation:**
* The Sepal Width and Length are not correlated
+ The Petal Width and Length are highly correlated

#### Steps To Be followed When Applying an Algorithm

 1. Split the dataset into training and testing dataset. The testing dataset is generally smaller than training one as it will help in training the model better.
 2. Select any algorithm based on the problem (classification or regression) whatever you feel may be good.
 3. Then pass the training dataset to the algorithm to train it. We use the **.fit()** method
 4. Then pass the testing data to the trained algorithm to predict the outcome. We use the **.predict()** method.
 5. We then check the accuracy by **passing the predicted outcome and the actual output** to the model.

### Using All Features

We will first use all the features for training the algorithm and check the accuracy.
Then we will use 1 Petal Feature and 1 Sepal Feature to check the accuracy of the algorithm as we are using only 2 features that are not correlated. Thus we can have a variance in the dataset which may help in better accuracy.

#### Splitting The Data into Training And Testing Dataset

```python
# Split the data: train=70% and test=30%
train, test = train_test_split(iris, test_size = 0.3)
print(train.shape)
print(test.shape)
```
    (105, 5)
    (45, 5)



```python
# taking the training data features
train_X = train[['SepalLengthCm','SepalWidthCm','PetalLengthCm','PetalWidthCm']]

# output value of training data
train_y=train.Species

# taking the test data features
test_X= test[['SepalLengthCm','SepalWidthCm','PetalLengthCm','PetalWidthCm']] 

# output value of test data
test_y =test.Species
```

```python
train_X.head(2)
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
      <th>SepalLengthCm</th>
      <th>SepalWidthCm</th>
      <th>PetalLengthCm</th>
      <th>PetalWidthCm</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>133</th>
      <td>6.3</td>
      <td>2.8</td>
      <td>5.1</td>
      <td>1.5</td>
    </tr>
    <tr>
      <th>30</th>
      <td>4.8</td>
      <td>3.1</td>
      <td>1.6</td>
      <td>0.2</td>
    </tr>
  </tbody>
</table>
</div>




```python
test_X.head(2)
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
      <th>SepalLengthCm</th>
      <th>SepalWidthCm</th>
      <th>PetalLengthCm</th>
      <th>PetalWidthCm</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>24</th>
      <td>4.8</td>
      <td>3.4</td>
      <td>1.9</td>
      <td>0.2</td>
    </tr>
    <tr>
      <th>52</th>
      <td>6.9</td>
      <td>3.1</td>
      <td>4.9</td>
      <td>1.5</td>
    </tr>
  </tbody>
</table>
</div>




```python
train_y.head()  ##output of the training data
```




    133     Iris-virginica
    30         Iris-setosa
    23         Iris-setosa
    7          Iris-setosa
    64     Iris-versicolor
    Name: Species, dtype: object



#### Support Vector Machine (SVM)


```python
model = svm.SVC() #select the algorithm
model.fit(train_X,train_y) # we train the algorithm with the training data and the training output
prediction=model.predict(test_X) #now we pass the testing data to the trained algorithm
print('The accuracy of the SVM is:',metrics.accuracy_score(prediction,test_y))#now we check the accuracy of the algorithm. 
#we pass the predicted output by the model and the actual output
```

    ('The accuracy of the SVM is:', 1.0)


SVM is giving very good accuracy . We will continue to check the accuracy for different models.

Now we will follow the same steps as above for training various machine learning algorithms.

#### Logistic Regression


```python
model = LogisticRegression()
model.fit(train_X,train_y)
prediction=model.predict(test_X)
print('The accuracy of the Logistic Regression is',metrics.accuracy_score(prediction,test_y))
```

    ('The accuracy of the Logistic Regression is', 0.9777777777777777)


#### Decision Tree


```python
model=DecisionTreeClassifier()
model.fit(train_X,train_y)
prediction=model.predict(test_X)
print('The accuracy of the Decision Tree is',metrics.accuracy_score(prediction,test_y))
```

    ('The accuracy of the Decision Tree is', 0.9333333333333333)


#### K-Nearest Neighbours


```python
model=KNeighborsClassifier(n_neighbors=3) #this examines 3 neighbours for putting the new data into a class
model.fit(train_X,train_y)
prediction=model.predict(test_X)
print('The accuracy of the KNN is',metrics.accuracy_score(prediction,test_y))
```

    ('The accuracy of the KNN is', 0.9777777777777777)


#### Let's check the accuracy for various values of n for K-Nearest nerighbours


```python
a_index=list(range(1,11))
a=pd.Series()
x=[1,2,3,4,5,6,7,8,9,10]
for i in list(range(1,11)):
    model=KNeighborsClassifier(n_neighbors=i) 
    model.fit(train_X,train_y)
    prediction=model.predict(test_X)
    a=a.append(pd.Series(metrics.accuracy_score(prediction,test_y)))
plt.plot(a_index, a)
plt.xticks(x)
```




    ([<matplotlib.axis.XTick at 0x1a2006ad50>,
      <matplotlib.axis.XTick at 0x1a2006a890>,
      <matplotlib.axis.XTick at 0x1a2006a1d0>,
      <matplotlib.axis.XTick at 0x1a20091ad0>,
      <matplotlib.axis.XTick at 0x1a200fb090>,
      <matplotlib.axis.XTick at 0x1a200fb610>,
      <matplotlib.axis.XTick at 0x1a200fbb90>,
      <matplotlib.axis.XTick at 0x1a20106150>,
      <matplotlib.axis.XTick at 0x1a201066d0>,
      <matplotlib.axis.XTick at 0x1a200fb810>],
     <a list of 10 Text xticklabel objects>)




![png](/assets/images/output_41_1.png)


Above is the graph showing the accuracy for the KNN models using different values of n. 

### Use Petals and Sepals Seperately

#### Creating Petals And Sepals Training Data 


```python
petal=iris[['PetalLengthCm','PetalWidthCm','Species']]
sepal=iris[['SepalLengthCm','SepalWidthCm','Species']]
```


```python
train_p,test_p=train_test_split(petal,test_size=0.3,random_state=0)  #petals
train_x_p=train_p[['PetalWidthCm','PetalLengthCm']]
train_y_p=train_p.Species
test_x_p=test_p[['PetalWidthCm','PetalLengthCm']]
test_y_p=test_p.Species


train_s,test_s=train_test_split(sepal,test_size=0.3,random_state=0)  #Sepal
train_x_s=train_s[['SepalWidthCm','SepalLengthCm']]
train_y_s=train_s.Species
test_x_s=test_s[['SepalWidthCm','SepalLengthCm']]
test_y_s=test_s.Species
```

#### SVM


```python
model=svm.SVC()
model.fit(train_x_p,train_y_p) 
prediction=model.predict(test_x_p) 
print('The accuracy of the SVM using Petals is:',metrics.accuracy_score(prediction,test_y_p))

model=svm.SVC()
model.fit(train_x_s,train_y_s) 
prediction=model.predict(test_x_s) 
print('The accuracy of the SVM using Sepal is:',metrics.accuracy_score(prediction,test_y_s))
```

    ('The accuracy of the SVM using Petals is:', 0.9777777777777777)
    ('The accuracy of the SVM using Sepal is:', 0.8)


#### Logistic Regression


```python
model = LogisticRegression()
model.fit(train_x_p,train_y_p) 
prediction=model.predict(test_x_p) 
print('The accuracy of the Logistic Regression using Petals is:',metrics.accuracy_score(prediction,test_y_p))

model.fit(train_x_s,train_y_s) 
prediction=model.predict(test_x_s) 
print('The accuracy of the Logistic Regression using Sepals is:',metrics.accuracy_score(prediction,test_y_s))
```

    ('The accuracy of the Logistic Regression using Petals is:', 0.6888888888888889)
    ('The accuracy of the Logistic Regression using Sepals is:', 0.6444444444444445)


#### Decision Tree


```python
model=DecisionTreeClassifier()
model.fit(train_x_p,train_y_p) 
prediction=model.predict(test_x_p) 
print('The accuracy of the Decision Tree using Petals is:',metrics.accuracy_score(prediction,test_y_p))

model.fit(train_x_s,train_y_s) 
prediction=model.predict(test_x_s) 
print('The accuracy of the Decision Tree using Sepals is:',metrics.accuracy_score(prediction,test_y_s))
```

    ('The accuracy of the Decision Tree using Petals is:', 0.9555555555555556)
    ('The accuracy of the Decision Tree using Sepals is:', 0.6444444444444445)


#### K-Nearest Neighbours


```python
model=KNeighborsClassifier(n_neighbors=3) 
model.fit(train_x_p,train_y_p) 
prediction=model.predict(test_x_p) 
print('The accuracy of the KNN using Petals is:',metrics.accuracy_score(prediction,test_y_p))

model.fit(train_x_s,train_y_s) 
prediction=model.predict(test_x_s) 
print('The accuracy of the KNN using Sepals is:',metrics.accuracy_score(prediction,test_y_s))
```

    ('The accuracy of the KNN using Petals is:', 0.9777777777777777)
    ('The accuracy of the KNN using Sepals is:', 0.7333333333333333)


### Observations:

 - Using Petals over Sepal for training the data gives a much better accuracy.
 - This was expected as we saw in the heatmap above that the correlation between the Sepal Width and Length was very low whereas the correlation between Petal Width and Length was very high. 
