# Shallow Algorthims

## Naive Bayse

ex. Spam Mail Detector

## Gradient Descent

ex. Getting down from Mount. Height from ground. Goal is to get down easiest way. (Height is the error in Data Mining algorithms)

## Regression Linear

ex. Predict House prize based on other houses properties and prize -> Draw random line -> try minimize error using Gradient Descent (least square).

## Logistic Regression

ex. Divide two classes by a line -> random line til reduce sum of error with gradient descent (log lost method!)

## SVM (Support vector machine)

Like LR find the best divider. The line with maximum distance from the classes. -> Find maximum distance with Gradient Descent or other algothims!

## Kernel Method

Like LR when can't divide it in 2D. Add Z param so we can divide them with Surface in 3D.

```py
[A(0,3),B(1,2),B(2,1),A(3,0)] -> add Z=xy -> (x,y,xy)
Or in 2D divide with curve y=1/x
```

## K-Means Clustering

ex. Know numbers of clusters = K. find K centers for K groups

## Hierarchical Clustering

ex. Like K-Means instead of K numbers of clusters, group objects with maximum distance that we defind, so we have unknown numbers clusters.

## K-Nearest Classification

- PYTHON Predict > `n = Knearest(); n.fit(x,y); n.predict(X)`
- PYTHON Validate > `n.score(xtest,ytest)*100`
- K is a hyper-parameter.

## Linear Regression

```py
from sklearn import linear_model
xtr,ytr=split_data(df)

lr=LinearRegression()
lr.fit(xtr,ytr)
ypre=lr.predict(xte)
```

Logistic Regression

```py
from sklearn.linear_model import LogisticReg
model=LogisticRegression()
model.fit(xtr,ytr)
accuracyTrain=model.score(xtr,ytr)
ypre=model.predict(xtest)
accuracy=metrics.accuracy_score(yte,ypre)
```

train_test_split

```py
xtr,ytr,xte,yte=train_test_split(x,target,test_size=0.3)
```

KNeighborsClassifier

```py
from sklearn.neighbors import KNeighborsClassifier
knn=KNeighborsCliassifier(n_neighbors)
knn.fit(xtr,ytr)
ypre=knn.predict(xtrain)
metrics.accuracy_score(ytr,ypre) #(TrainAcc going to be ==1)
metrics.accuracy_score(ytest,ypre) #(TestAcc is RIGHT)
```
