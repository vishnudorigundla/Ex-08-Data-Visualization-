# Ex-08-Data-Visualization-
# AIM
To Perform Data Visualization on a complex dataset and save the data to a file.

# Explanation
Data visualization is the graphical representation of information and data. By using visual elements like charts, graphs, and maps, data visualization tools provide an accessible way to see and understand trends, outliers, and patterns in data.

# ALGORITHM
STEP 1
Read the given Data

STEP 2
Clean the Data Set using Data Cleaning Process

STEP 3
Apply Feature generation and selection techniques to all the features of the data set

STEP 4
Apply data visualization techniques to identify the patterns of the data.

```
Developed by: D.vishnu vardhan reddy
Register no: 212221230023
```
# CODE :
```
#loading the dataset
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
df=pd.read_csv("Superstore.csv")
df
```
```
#removing unnecessary data variables
df.drop('Row ID',axis=1,inplace=True)
df.drop('Order ID',axis=1,inplace=True)
df.drop('Customer ID',axis=1,inplace=True)
df.drop('Customer Name',axis=1,inplace=True)
df.drop('Country',axis=1,inplace=True)
df.drop('Postal Code',axis=1,inplace=True)
df.drop('Product ID',axis=1,inplace=True)
df.drop('Product Name',axis=1,inplace=True)
df.drop('Order Date',axis=1,inplace=True)
df.drop('Ship Date',axis=1,inplace=True)
print("Updated dataset")
df

df.isnull().sum()
```
```
#detecting and removing outliers in current numeric data
plt.figure(figsize=(12,10))
plt.title("Data with outliers")
df.boxplot()
plt.show()

plt.figure(figsize=(12,10))
cols = ['Sales','Quantity','Discount','Profit']
Q1 = df[cols].quantile(0.25)
Q3 = df[cols].quantile(0.75)
IQR = Q3 - Q1
df = df[~((df[cols] < (Q1 - 1.5 * IQR)) |(df[cols] > (Q3 + 1.5 * IQR))).any(axis=1)]
plt.title("Dataset after removing outliers")
df.boxplot()
plt.show()
```
```
#data visualization
#line plots
import seaborn as sns
sns.lineplot(x="Sub-Category",y="Sales",data=df,marker='o')
plt.title("Sub Categories vs Sales")
plt.xticks(rotation = 90)
plt.show()

sns.lineplot(x="Category",y="Profit",data=df,marker='o')
plt.xticks(rotation = 90)
plt.title("Categories vs Profit")
plt.show()

sns.lineplot(x="Region",y="Sales",data=df,marker='o')
plt.xticks(rotation = 90)
plt.title("Region area vs Sales")
plt.show()

sns.lineplot(x="Category",y="Discount",data=df,marker='o')
plt.title("Categories vs Discount")
plt.show()

sns.lineplot(x="Sub-Category",y="Quantity",data=df,marker='o')
plt.xticks(rotation = 90)
plt.title("Sub Categories vs Quantity")
plt.show()
```
```
#bar plots
sns.barplot(x="Sub-Category",y="Sales",data=df)
plt.title("Sub Categories vs Sales")
plt.xticks(rotation = 90)
plt.show()

sns.barplot(x="Category",y="Profit",data=df)
plt.title("Categories vs Profit")
plt.show()

sns.barplot(x="Sub-Category",y="Quantity",data=df)
plt.title("Sub Categories vs Quantity")
plt.xticks(rotation = 90)
plt.show()

sns.barplot(x="Category",y="Discount",data=df)
plt.title("Categories vs Discount")
plt.show()

plt.figure(figsize=(12,7))
sns.barplot(x="State",y="Sales",data=df)
plt.title("States vs Sales")
plt.xticks(rotation = 90)
plt.show()

plt.figure(figsize=(25,8))
sns.barplot(x="State",y="Sales",hue="Region",data=df)
plt.title("State vs Sales based on Region")
plt.xticks(rotation = 90)
plt.show()
```
```
#Histogram
sns.histplot(data = df,x = 'Region',hue='Ship Mode')
sns.histplot(data = df,x = 'Category',hue='Quantity')
sns.histplot(data = df,x = 'Sub-Category',hue='Category')
plt.xticks(rotation = 90)
plt.show()
sns.histplot(data = df,x = 'Quantity',hue='Segment')
plt.hist(data = df,x = 'Profit')
plt.show()
```
```
#count plot
plt.figure(figsize=(10,7))
sns.countplot(x ='Segment', data = df,hue = 'Sub-Category')
sns.countplot(x ='Region', data = df,hue = 'Segment')
sns.countplot(x ='Category', data = df,hue='Discount')
sns.countplot(x ='Ship Mode', data = df,hue = 'Quantity')
```
```
#Barplot 
sns.boxplot(x="Sub-Category",y="Discount",data=df)
plt.xticks(rotation = 90)
plt.show()
sns.boxplot( x="Profit", y="Category",data=df)
plt.xticks(rotation = 90)
plt.show()
plt.figure(figsize=(10,7))
sns.boxplot(x="Sub-Category",y="Sales",data=df)
plt.xticks(rotation = 90)
plt.show()
sns.boxplot(x="Category",y="Profit",data=df)
sns.boxplot(x="Region",y="Sales",data=df)
plt.figure(figsize=(10,7))
sns.boxplot(x="Sub-Category",y="Quantity",data=df)
plt.xticks(rotation = 90)
plt.show()
sns.boxplot(x="Category",y="Discount",data=df)
plt.figure(figsize=(15,7))
sns.boxplot(x="State",y="Sales",data=df)
plt.xticks(rotation = 90)
plt.show()
```
```
#KDE plot
sns.kdeplot(x="Profit", data = df,hue='Category')
sns.kdeplot(x="Sales", data = df,hue='Region')
sns.kdeplot(x="Quantity", data = df,hue='Segment')
sns.kdeplot(x="Discount", data = df,hue='Segment')
```
```
#violin plot
sns.violinplot(x="Profit",data=df)
sns.violinplot(x="Discount",y="Ship Mode",data=df)
sns.violinplot(x="Quantity",y="Ship Mode",data=df)
```
```
#point plot
sns.pointplot(x=df["Quantity"],y=df["Discount"])
sns.pointplot(x=df["Quantity"],y=df["Category"])
sns.pointplot(x=df["Sales"],y=df["Sub-Category"])
```
```
#Pie Chart
df.groupby(['Category']).sum().plot(kind='pie', y='Discount',figsize=(6,10),pctdistance=1.7,labeldistance=1.2)
df.groupby(['Sub-Category']).sum().plot(kind='pie', y='Sales',figsize=(10,10),pctdistance=1.7,labeldistance=1.2)
df.groupby(['Region']).sum().plot(kind='pie', y='Profit',figsize=(6,9),pctdistance=1.7,labeldistance=1.2)
df.groupby(['Ship Mode']).sum().plot(kind='pie', y='Quantity',figsize=(8,11),pctdistance=1.7,labeldistance=1.2)

df1=df.groupby(by=["Category"]).sum()
labels=[]
for i in df1.index:
    labels.append(i)  
plt.figure(figsize=(8,8))
colors = sns.color_palette('pastel')
plt.pie(df1["Profit"],colors = colors,labels=labels, autopct = '%0.0f%%')
plt.show()

df1=df.groupby(by=["Ship Mode"]).sum()
labels=[]
for i in df1.index:
    labels.append(i)
colors=sns.color_palette("bright")
plt.pie(df1["Sales"],labels=labels,autopct="%0.0f%%")
plt.show()
```
```
#HeatMap
df4=df.copy()

#encoding
from sklearn.preprocessing import LabelEncoder,OrdinalEncoder,OneHotEncoder
le=LabelEncoder()
ohe=OneHotEncoder
oe=OrdinalEncoder()

df4["Ship Mode"]=oe.fit_transform(df[["Ship Mode"]])
df4["Segment"]=oe.fit_transform(df[["Segment"]])
df4["City"]=le.fit_transform(df[["City"]])
df4["State"]=le.fit_transform(df[["State"]])
df4['Region'] = oe.fit_transform(df[['Region']])
df4["Category"]=oe.fit_transform(df[["Category"]])
df4["Sub-Category"]=le.fit_transform(df[["Sub-Category"]])

#scaling
from sklearn.preprocessing import RobustScaler
sc=RobustScaler()
df5=pd.DataFrame(sc.fit_transform(df4),columns=['Ship Mode', 'Segment', 'City', 'State','Region',
'Category','Sub-Category','Sales','Quantity','Discount','Profit'])

#Heatmap
plt.subplots(figsize=(12,7))
sns.heatmap(df5.corr(),cmap="PuBu",annot=True)
plt.show()
```
# OUTPUT :
OUPUT
Initial Dataset:

![image](https://user-images.githubusercontent.com/94175324/172290769-a17f9810-ba58-47a0-8bb4-9046cc70f484.png)


Cleaned Dataset:
![image](https://user-images.githubusercontent.com/94175324/172291136-eb6515e2-2309-4fc5-9f06-c63d85c23e05.png)
![image](https://user-images.githubusercontent.com/94175324/172291166-4fb08340-07c3-4f50-a27a-12c29f373d61.png)




Removing Outliers:

![image](https://user-images.githubusercontent.com/94175324/172291189-e0393a0d-19cc-4059-af23-50fccd1e425d.png)
![image](https://user-images.githubusercontent.com/94175324/172291230-c37fc8c0-451d-49e1-bc41-0c763edf3cea.png)



Line PLot:
![image](https://user-images.githubusercontent.com/94175324/172291273-5fdf1bcb-fa26-4b65-9f6f-623d90ba6ff4.png)
![image](https://user-images.githubusercontent.com/94175324/172291320-979dacaa-8ec3-47b7-9142-2b5110592330.png)
![image](https://user-images.githubusercontent.com/94175324/172291336-864d03d1-d571-466c-b8f5-08f727df0d25.png)
![image](https://user-images.githubusercontent.com/94175324/172291350-343f69d4-1720-490b-a490-ee8920a62dc3.png)
![image](https://user-images.githubusercontent.com/94175324/172291583-20d07c56-1a70-427d-89f4-d3223155cc9b.png)















Bar Plots:
![image](https://user-images.githubusercontent.com/94175324/172291607-2ae6afd5-d55d-494c-9e59-9ce1c2cb707c.png)
![image](https://user-images.githubusercontent.com/94175324/172291625-c0edf028-f7b6-4850-b898-8cfd649b8377.png)
![image](https://user-images.githubusercontent.com/94175324/172291642-8478c264-3e3e-4929-a0c5-694873e474db.png)
![image](https://user-images.githubusercontent.com/94175324/172291654-4b37765e-dae4-4fab-956e-95963e3fed08.png)
![image](https://user-images.githubusercontent.com/94175324/172291688-00703f6d-0eaa-4c03-8c6b-1f3adecbca6c.png)












Histograms:

![image](https://user-images.githubusercontent.com/94175324/172291708-f6afb9b8-a276-41ef-9c1f-3bc5072524b3.png)
![image](https://user-images.githubusercontent.com/94175324/172291752-8acb96bf-222a-44a4-b44b-61c4e877df18.png)
![image](https://user-images.githubusercontent.com/94175324/172291834-1623fcfd-7aed-4a59-8eb6-25bb701b5273.png)
![image](https://user-images.githubusercontent.com/94175324/172291869-332d8f2b-eec1-4e9d-9249-ae14a01fc081.png)









Count plots:


![image](https://user-images.githubusercontent.com/94175324/172291885-ccf1e03e-df4c-4c5f-b256-8d28cdf24c71.png)
![image](https://user-images.githubusercontent.com/94175324/172291895-f1112134-0c94-4c1a-8374-259d43405edc.png)
![image](https://user-images.githubusercontent.com/94175324/172291920-62648fb3-dc6a-4443-86b3-def11f715b1e.png)
![image](https://user-images.githubusercontent.com/94175324/172291937-153812c1-2452-4b9d-82df-dad8abeef1a5.png)









Bar Charts:

![image](https://user-images.githubusercontent.com/94175324/172291968-06321446-7c08-42d5-91e1-c15543af5d8c.png)
![image](https://user-images.githubusercontent.com/94175324/172291984-b79a1b0b-42a4-4a08-8cb8-006dd6f857c3.png)
![image](https://user-images.githubusercontent.com/94175324/172292004-62fc9a6f-e675-440e-831a-191bdaee2ee5.png)
![image](https://user-images.githubusercontent.com/94175324/172292039-040aa434-d322-462c-bdb2-10bfaaa295b6.png)
![image](https://user-images.githubusercontent.com/94175324/172292053-f39ca310-2c5e-41e4-a4d5-d052e7a61a65.png)
![image](https://user-images.githubusercontent.com/94175324/172292069-4c36b9b8-3de4-4928-8bdb-690d9b9f62da.png)















KDE Plots:

![image](https://user-images.githubusercontent.com/94175324/172292091-82a8144b-c3a8-4000-b9bb-7cd86e08a30e.png)
![image](https://user-images.githubusercontent.com/94175324/172292117-f57e2fca-53a1-47a3-bba7-2df3f7f7e4ff.png)
![image](https://user-images.githubusercontent.com/94175324/172292138-e9ca6b01-9bc6-40e2-a71f-0437893c84db.png)







Violin Plot:

![image](https://user-images.githubusercontent.com/94175324/172292158-8fb25a75-376b-4207-b933-96e8fb71173b.png)
![image](https://user-images.githubusercontent.com/94175324/172292175-caa9657c-7a11-4f1e-bc21-e664fa5ea7aa.png)
![image](https://user-images.githubusercontent.com/94175324/172292211-96ec0635-66ce-47b0-96ac-80b6f011cc4d.png)







Point Plots:

![image](https://user-images.githubusercontent.com/94175324/172292234-60eb471e-b431-409c-a412-539d8b099896.png)
![image](https://user-images.githubusercontent.com/94175324/172292244-d67eed03-3756-4ab6-8cf4-c5914c970307.png)
![image](https://user-images.githubusercontent.com/94175324/172292266-fe935cd6-7b64-454f-811b-288ba02b9e12.png)





Pie Charts:


![image](https://user-images.githubusercontent.com/94175324/172292281-c725d5f8-7306-4be0-80a5-8069719cf144.png)
![image](https://user-images.githubusercontent.com/94175324/172292312-97c8afda-abf8-473d-ad9a-39147e235d57.png)
![image](https://user-images.githubusercontent.com/94175324/172292358-5ca3e373-3e31-470f-8afa-275f6339d760.png)
![image](https://user-images.githubusercontent.com/94175324/172292382-2ba24f49-cd7b-4039-994d-04aaf9571f31.png)










HeatMap:

![image](https://user-images.githubusercontent.com/94175324/172292396-1c40ea57-56be-49a6-a8f4-a1333560045a.png)

# Result:
Hence,Data Visualization is applied on the complex dataset using libraries like Seaborn and Matplotlib successfully and the data is saved to file.
