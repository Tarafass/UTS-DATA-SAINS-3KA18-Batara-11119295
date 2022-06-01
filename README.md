# UTS-DATA-SAINS-3KA18-Batara-11119295

Untuk grafik saya lebih ke polyminial dan Linear model dikarenakan lebih jelas dan lebih baik

"#Import the libraries
from sklearn.svm import SVR
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
plt.style.use('seaborn-darkgrid')" adalah style ipynb

"#Load the data
#from google.colab import files # Use to load data on Google Colab
#uploaded = files.upload() # Use to load data on Google Colab
df = pd.read_csv('GOOG.csv')
df" Adalah untuk meng upload data xls nya

"actual_price = df.tail(1)
actual_price" adalah untuk mencari harga di hari terakhir

"df = df.head(len(df)-1)
df" adalah mengurutkan semua data hanya sampai tanggal 29

"#Create the lists / X and y data set
days = list()
adj_close_prices = list()" adalah untuk membuat list harian nya

"df_days = df.loc[:, 'Date']
df_adj_close = df.loc[:, 'Adj Close']" untuk mencari tanggal yang ingin di cari

"#Create the independent data set
for day in df_days:
   days.append( [int(day.split('/')[1])] )
#Create the dependent data set
for adj_close_price in df_adj_close:
   adj_close_prices.append( float(adj_close_price) )" untuk mencari harga
   
   "print(days)" untuk print selama 1 bulan
   
   "#Create and train an SVR model using a linear kernel
lin_svr = SVR(kernel='linear', C=1000.0)
lin_svr.fit(days,adj_close_prices)#Create and train an SVR model using a polynomial kernel
poly_svr = SVR(kernel='poly', C=1000.0, degree=2)
poly_svr.fit(days, adj_close_prices)#Create and train an SVR model using a RBF kernel
rbf_svr = SVR(kernel='rbf', C=2500.0, gamma=0.20)
rbf_svr.fit(days, adj_close_prices)" pembuatan liniear nya

"#Plot the models on a graph to see which has the best fit
plt.figure(figsize=(16,8))
plt.scatter(days, adj_close_prices, color = 'black', label='Original Data')
plt.plot(days, rbf_svr.predict(days), color = 'green', label='RBF Model')
plt.plot(days, poly_svr.predict(days), color = 'orange', label='Polynomial Model')
plt.plot(days, lin_svr.predict(days), color = 'purple', label='Linear Model')
plt.xlabel('Days')
plt.ylabel('Adj Close Price')
plt.title('Support Vector Regression')
plt.legend()
plt.show()" menampilkan graph nya

"day = [[30]]
print('The RBF SVR predicted:', rbf_svr.predict(day))
print('The Linear SVR predicted:', lin_svr.predict(day))
print('The Polynomial SVR predicted:', poly_svr.predict(day))" prediksi harian nya
