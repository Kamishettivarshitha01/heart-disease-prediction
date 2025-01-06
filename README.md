# -*- coding: utf-8 -*-
"""ml.ipynb

Automatically generated by Colab.

Original file is located at
    https://colab.research.google.com/drive/1sLCh058ziyW4x_JWZLqOizATgPy0uX0u
"""

import pandas as pd

df=pd.read_csv('/content/heart (1).csv')

df

df.head()

df.tail()

df.describe()

df.shape

df.columns

df.isna().sum()

df.head()

df.tail()

df.shape

df['target'].value_counts()

df.info()

df['target'].value_counts()

df['chol'].value_counts()

df['sex'].value_counts()

df=df.drop([df.columns[3],df.columns[6],df.columns[5]],axis=1)

df.head()

import matplotlib.pyplot as plt
import plotly.express as px
fig=px.histogram(df,x='age')
fig.show()

x=df.drop(['target'],axis=1)
y=df['target']
print(x.head())
print(y.head())

from sklearn.model_selection import train_test_split
train_x,test_x,train_y,test_y=train_test_split(x,y,test_size=0.2,random_state=2)

print(train_x.head())
print(train_y.head())

from sklearn.linear_model import LinearRegression
from sklearn.metrics import mean_squared_error,r2_score
model_lr=LinearRegression()
model_lr.fit(train_x,train_y)

y_pred_train_lr=model_lr.predict(train_x)
y_pred_test_lr=model_lr.predict(test_x)

y_pred_train_lr=model_lr.predict(train_x)
y_pred_test_lr=model_lr.predict(test_x)
train_mse_lr=mean_squared_error(train_y,y_pred_train_lr)
test_mse_lr=mean_squared_error(test_y,y_pred_test_lr)
train_r2_lr=r2_score(train_y,y_pred_train_lr)
test_r2_lr=r2_score(test_y,y_pred_test_lr)

print(train_mse_lr)
print(test_mse_lr)
print(train_r2_lr)
print(test_r2_lr)

from sklearn.linear_model import LogisticRegression
model_lr=LogisticRegression(max_iter=1000)
model_lr.fit(train_x,train_y)
y_pred_train=model_lr.predict(train_x)
y_pred_test=model_lr.predict(test_x)

print(y_pred_test)

print(y_pred_train)

from sklearn.metrics import accuracy_score,confusion_matrix

accuracy_train=accuracy_score(train_y,y_pred_train)
print("Accuracy of the Logistic Regression model on your train",accuracy_train)

accuracy_test=accuracy_score(test_y,y_pred_test)
print("Accuracy of the Logistic Regression model on your test dataset",accuracy_test)

confusion_matrix(test_y,y_pred_test)

tn,fp,fn,tp=confusion_matrix(test_y,y_pred_test).ravel()
print("TN:",tn)
print("FN:",fn)
print("FP:",fp)
print("TP:",tp)

accuracy=(tp+tn)/(tp+tn+fp+fn)
accuracy

confusion_matrix(train_y,y_pred_train)

Recall=tp/(tp+fn)
print("Recall of Logistic Regression is:",Recall)
Precision=tp/(tp+fp)
print("Precision of Logistic Regression is",Precision)
F1_score=(2*Recall+Precision)/(Recall+Precision)
print("F1_score of Logistic Regression is:",F1_score)

import pandas as pd
from sklearn.tree import DecisionTreeClassifier

dt=DecisionTreeClassifier(criterion='entropy')
dt.fit(train_x,train_y)
y_pred_test_dt=dt.predict(test_x)
y_pred_train_dt=dt.predict(train_x)

accuracy_train = accuracy_score(train_y,y_pred_train_dt)
print("Accuracy of the Decision tree model on your train dataset,accuracy_train")

accuracy_test = accuracy_score(test_y,y_pred_test_dt)
print("Accuracy of the Decision tree model on your test dataset,accuracy_test")

from sklearn.metrics import precision_score, recall_score, f1_score # Importing necessary functions

precision_test=precision_score(test_y,y_pred_test_dt)
print("precision of the Desion Tree on your test dataset",precision_test)
recall_test=recall_score(test_y,y_pred_test_dt)
print("recall of the Decision tree on your test dataset",recall_test)
f1_score_test=f1_score(test_y,y_pred_test_dt)
print("F1 score of the Decision Tree on your test dataset",f1_score_test)

precision_train=precision_score(train_y,y_pred_train_dt)
print("precision of the DT on your train dataset",precision_train)
recall_train=recall_score(train_y,y_pred_train_dt)
print("recall of the DT on your train dataset",recall_train)
f1_score_train=f1_score(train_y,y_pred_train_dt)
print("F1 score of the DT on your train dataset",f1_score_train)

import pandas as pd
from sklearn.neighbors import KNeighborsClassifier

import pandas as pd
from sklearn.neighbors import KNeighborsClassifier # Corrected the class name

model_knn = KNeighborsClassifier(n_neighbors=5) # Corrected the class name
model_knn.fit(train_x, train_y)
y_pred_train_knn = model_knn.predict(train_x)
y_pred_test_knn = model_knn.predict(test_x)

print(y_pred_train_knn)

print(y_pred_test_knn)

accuracy_test = accuracy_score(test_y,y_pred_test_knn)
print("Accuracy of the knn model on your test dataset,accuracy_test")
accuracy_train = accuracy_score(train_y,y_pred_train_knn)
print("Accuracy of the knn model on your train dataset,accuracy_train")
precision_test=precision_score(test_y,y_pred_test_knn)
print("precision of the knn on your test dataset",precision_test)
recall_test=recall_score(test_y,y_pred_test_knn)
print("recall of the knn on your test dataset",recall_test)
f1_score_test=f1_score(test_y,y_pred_test_knn)
print("F1 score of the knn on your test dataset",f1_score_test)

print("Accuracy of the KNN model on your train dataset,accuracy_train")
precision_train=precision_score(train_y,y_pred_train_knn)
print("precision of the knn on your train dataset",precision_train)
recall_train=recall_score(train_y,y_pred_train_knn)
print("recall of the knn on your train dataset",recall_train)
f1_score_test=f1_score(train_y,y_pred_train_knn)
print("F1 score of the knn on your train dataset",f1_score_train)

from sklearn.cluster import KMeans
k=3
model_kmeans=KMeans(n_clusters=k,random_state=42)
columns_for_cllustering=["age","chol"]
df_for_clustering=df[columns_for_cllustering]
model_kmeans.fit(df_for_clustering)
from sklearn.cluster import KMeans
k=3
model_kmeans=KMeans(n_clusters=k,random_state=42)
columns_for_cllustering=["age","chol"]
df_for_clustering=df[columns_for_cllustering]
model_kmeans.fit(df_for_clustering)
cluster_labels=model_kmeans.labels_
cluster_centers=model_kmeans.cluster_centers_
plt.figure(figsize=(8,6))
plt.scatter(df_for_clustering['age'],df_for_clustering['chol'],c=cluster_labels,cmap='viridis',alpha=0.5)
plt.scatter(cluster_centers[:,0],cluster_centers[:,1],marker='x',s=100,color='red')
plt.xlabel("Age")
plt.ylabel("Chol")
plt.title("K-means Clustering")
#plt.legend() # legend might not be necessary if not specifying specific labels for the scatter plots
plt.show()

from sklearn.cluster import KMeans
from sklearn.metrics import silhouette_score,davies_bouldin_score,calinski_harabasz_score,homogeneity_score,completeness_score,v_measure_score
import matplotlib.pyplot as plt
k=2
model_KMeans = KMeans(n_clusters=k,random_state=42)
model_KMeans.fit(x)
cluster_labels=model_KMeans.labels_
inertia=model_KMeans.inertia_
print("Inertia:",inertia)
silhouette=silhouette_score(x,cluster_labels)
print("Silhouette_Score:",silhouette)
davies_bouldin=davies_bouldin_score(x,cluster_labels)
print("Davies_Bouldin Score:",davies_bouldin)
calinski_harabasz=calinski_harabasz_score(x,cluster_labels)
print("Calinski-Harabasz Score:",calinski_harabasz)
homogeneity=homogeneity_score(y,cluster_labels)
completeness=completeness_score(y,cluster_labels)
v_measure=v_measure_score(y,cluster_labels)
print("Homogeneity Score:",homogeneity)
print("Completeness Score:",completeness)
print("v_measure:",v_measure)
plt.figure(figsize=(8,6))
colors=['navy','turquoise']
lw=2
plt.figure(figsize=(8,6))
plt.scatter(df_for_clustering['age'],df_for_clustering['chol'],c=cluster_labels,cmap='viridis',alpha=0.7)
plt.scatter(cluster_centers[:,0],cluster_centers[:,1],c='red',marker='x',s=100,label='centroid')
plt.xlabel('age')
plt.ylabel('chol')
plt.title('K-means Clustering')
plt.legend()
plt.show()

from sklearn.discriminant_analysis import LinearDiscriminantAnalysis
import matplotlib.pyplot as plt
import numpy as np
lda =LinearDiscriminantAnalysis(n_components=1)
x_lda=lda.fit_transform(x,y)
plt.figure(figsize=(8,6))
colors=['navy','turquoise']
lw=2
for color,i,target_name in zip(colors,[0,1],['No Heart Disease','Heart Disease']):
  plt.scatter(x_lda[y==1,0],np.zeros_like(x_lda[y==1,0]),color=color,alpha=.8,lw=lw,label=target_name)
plt.legend(loc="best",shadow=False,scatterpoints=1)
plt.title("LDA of Heart Disease Dataset")
plt.xlabel("LD1")
plt.show()
