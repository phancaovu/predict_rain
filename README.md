# phan cao vu project data analyst 
- [phan cao vu project data analyst](#phan-cao-vu-project-data-analyst)
  - [Rain Predict in Australia](#rain-predict-in-australia)
  - [Library](#library)
  - [Clear data](#clear-data)
  - [Handle data error](#handle-data-error)
  - [Data Visualization](#data-visualization)

## Rain Predict in Australia

## Library 
```py  
import matplotlib.pyplot as plt
import numpy as np
import pandas as pd 
import seaborn as sns
from sklearn.model_selection import train_test_split
from sklearn import tree
from sklearn.linear_model import LogisticRegression
from sklearn.naive_bayes import GaussianNB
import sklearn.metrics 
```
## Clear data 
>```rain = pd.read_csv('./rain.csv')```
>
>
>``` rain.head()```
>
>
> ![](https://scontent.fsgn2-4.fna.fbcdn.net/v/t39.30808-6/322554606_1106347593363691_2001542980926192804_n.jpg?_nc_cat=101&ccb=1-7&_nc_sid=730e14&_nc_ohc=fRGGtlEuVjcAX8hqcLu&_nc_ht=scontent.fsgn2-4.fna&oh=00_AfA6JnIrvPxDRxRCIHfRepsG761sOKPv2Gf0zlnqt4I15w&oe=63BFF7CF)
>
>```rain.info()```
>
> ![](https://scontent.fsgn2-1.fna.fbcdn.net/v/t39.30808-6/321123435_1233446584050469_4448477147016249291_n.jpg?_nc_cat=105&ccb=1-7&_nc_sid=730e14&_nc_ohc=WZPgOKsRxakAX-C6U07&_nc_ht=scontent.fsgn2-1.fna&oh=00_AfCThbxBj5Ai_NBKYPiUBBnpTgOWM-2Vek9LSaX8BwJgCw&oe=63C0FBC0)
>
>```rain.shape```
> 
>(145460, 23)
>
>```rain.columns```
>
> Index(['Date', 'Location', 'MinTemp', 'MaxTemp', 'Rainfall', 'Evaporation',
       'Sunshine', 'WindGustDir', 'WindGustSpeed', 'WindDir9am', 'WindDir3pm',
       'WindSpeed9am', 'WindSpeed3pm', 'Humidity9am', 'Humidity3pm',
       'Pressure9am', 'Pressure3pm', 'Cloud9am', 'Cloud3pm', 'Temp9am',
       'Temp3pm', 'RainToday', 'RainTomorrow'],
      dtype='object')
>
>```(rain.isnull().sum()/len(rain))*100```
>
> kiem tra phan tram du lieu bi loi
>
> ![](https://scontent.fsgn2-7.fna.fbcdn.net/v/t39.30808-6/321400179_1230139244266428_7745902574709622622_n.jpg?_nc_cat=100&ccb=1-7&_nc_sid=730e14&_nc_ohc=0F89dpPkprsAX8fmpjq&_nc_oc=AQkFgR3iWEBGcagr2wwaWT33FlMeOYb6vZrAVR1PqmIolE3ZKL8kCsbRldj2r_ISAtQ&tn=Fxsbeo8P-gREppb6&_nc_ht=scontent.fsgn2-7.fna&oh=00_AfCaJLyBooBN_TmuC70MZOqh8tp33MJp4mJ7fERwpO83Ew&oe=63C0C720)
>
> Xoa cac cot co du lieu bi loi tren 30%
>
>```rain.drop(columns=['Evaporation','Sunshine','Cloud9am','Cloud3pm'], inplace=True)```
>
> ```rain.isnull().any()```
>
> ![](https://scontent.fsgn2-5.fna.fbcdn.net/v/t39.30808-6/323773468_5799695793419638_6530623469781198235_n.jpg?_nc_cat=104&ccb=1-7&_nc_sid=730e14&_nc_ohc=sIba56fgT3gAX8GQfDC&_nc_ht=scontent.fsgn2-5.fna&oh=00_AfDjYWwLoay_Fd7fzi8WWbtumi6Mh-uLbUviHo0Hg0xgoA&oe=63C16A7B)
>

## Handle data error 
>
> ```py
> # viết hàm xữ lý những giá trị rỗng 
>def missing_value_number(rain):
>    for col in rain.select_dtypes(['int','float']):
>       rain[col] = rain[col].fillna(rain[col].mean())
 >   return rain
>def missing_values_object(rain):
 >   for col in rain.select_dtypes(['object']):
>      rain[col] = rain[col].fillna(method='ffill')
   > return rain
>
> rain = missing_value_number(rain)
> rain = missing_values_object(rain)
>    
> ```
>```rain.isnull().any()```
> ![](https://scontent.fsgn2-8.fna.fbcdn.net/v/t39.30808-6/323884504_3429187710692457_6527387128568250653_n.jpg?_nc_cat=102&ccb=1-7&_nc_sid=730e14&_nc_ohc=3-L_64X1kg0AX-dZMYl&_nc_ht=scontent.fsgn2-8.fna&oh=00_AfBNbgST5OHPpzN0hvTztZq0OX3ejI_kwQaPc3PVAgwntA&oe=63C0B3EF)
>
> ```rain.head(5)```
> ![](https://scontent.fsgn2-5.fna.fbcdn.net/v/t39.30808-6/324244551_1314788102432304_1626457060402488696_n.jpg?_nc_cat=106&ccb=1-7&_nc_sid=730e14&_nc_ohc=KtVVWsbV9rQAX9P8XO8&_nc_ht=scontent.fsgn2-5.fna&oh=00_AfDyqMGFic_9BL0WEhJOyzyT1HKzXlm9FcGAq2BOmIAGBQ&oe=63C16526)
>

## Data Visualization
```py
# phân tích lượng mưa ở các thành phố
plt.figure(figsize=(15, 5))
sns.countplot(rain['Location'])
plt.xticks(rotation=90)
plt.show()
```
![](https://scontent.fsgn2-6.fna.fbcdn.net/v/t39.30808-6/320607255_741050664017486_5788331605001028882_n.jpg?_nc_cat=111&ccb=1-7&_nc_sid=730e14&_nc_ohc=7i5BlUUmtegAX8m0LhK&tn=Fxsbeo8P-gREppb6&_nc_ht=scontent.fsgn2-6.fna&oh=00_AfCUlpwXoH1l32-wO9HNxBGOKSjPDojCBE2hdb14rc0JFQ&oe=63C044D7)
```py
# Hướng gió trong 1 ngày 
plt.subplots(figsize=(16,8))
sns.countplot(data=rain, x='WindGustDir')
plt.show()
```
![](https://scontent.fsgn2-4.fna.fbcdn.net/v/t39.30808-6/323779747_1176914856275681_656325554053622985_n.jpg?_nc_cat=101&ccb=1-7&_nc_sid=730e14&_nc_ohc=N2a_1yXsX3kAX-6N0mT&_nc_ht=scontent.fsgn2-4.fna&oh=00_AfAbxB2c7QKE7blkcE_6TpJWA1V6mYXPUXQVRnDUl37l6w&oe=63C0CA86)
```py
# hướng gió lúc 9 giờ sáng
plt.subplots(figsize=(16,8))
sns.countplot(data=rain, x='WindDir9am')
```
![](https://scontent.fsgn2-7.fna.fbcdn.net/v/t39.30808-6/324030266_691189435809787_548453563519752509_n.jpg?_nc_cat=108&ccb=1-7&_nc_sid=730e14&_nc_ohc=6Q-qJRx3SLwAX_FDAR3&_nc_ht=scontent.fsgn2-7.fna&oh=00_AfBpppGgiNT96v-NpsJT4IG9DLNiL28U70DJ4VKcfW-ncw&oe=63BFF8F8)
```py
#Hướng gió lúc 3h chiều
plt.subplots(figsize=(16,8))
sns.countplot(data=rain, x='WindDir3pm')
plt.show()
```

![](https://scontent.fsgn2-7.fna.fbcdn.net/v/t39.30808-6/324193363_1019030055681280_6270629457741751171_n.jpg?_nc_cat=100&ccb=1-7&_nc_sid=730e14&_nc_ohc=oWBMzynrn90AX_jq3t0&_nc_ht=scontent.fsgn2-7.fna&oh=00_AfBQHYbbYhwiD1MwBd94iowoxGdlBs8gVL4yeafKpvjhuw&oe=63C1387F)

```py
#thống kê mưa hôm nay
plt.subplots(figsize=(8,6))
plt.grid(linewidth = 0.7)
sns.countplot(data=rain, x='RainToday')
plt.show()
```
![](https://scontent.fsgn2-4.fna.fbcdn.net/v/t39.30808-6/323891858_2321246314724476_4014210184603935052_n.jpg?_nc_cat=109&ccb=1-7&_nc_sid=730e14&_nc_ohc=fnySdwlX3IcAX_Xb4TL&tn=Fxsbeo8P-gREppb6&_nc_ht=scontent.fsgn2-4.fna&oh=00_AfAcoxoP9KLWqeDWGFkwiue3P7dvQReVGGPuPMeyk66jEA&oe=63C053D6)

```py 
# Thống kê mưa của ngày mai 
plt.subplots(figsize=(8,6))
plt.grid(linewidth = 0.7)
sns.countplot(data=rain, x='RainTomorrow')
```
![](https://scontent.fsgn2-7.fna.fbcdn.net/v/t39.30808-6/323708089_838308060583883_4736750582155495912_n.jpg?_nc_cat=108&ccb=1-7&_nc_sid=730e14&_nc_ohc=dLiuehWBcr4AX9N_EKh&_nc_ht=scontent.fsgn2-7.fna&oh=00_AfAGPtSKWB6Zpr0xKtECELPVtrFSgojJCQLemBxEzBmkqA&oe=63C0C3D8)
```py
# phân tích mưa hôm nay và mưa ngày hôm sau
type_plt = pd.crosstab(rain['RainToday'], rain['RainTomorrow'])

plt.rcParams["figure.figsize"] = (8,5)

type_plt.plot(kind='bar',stacked=False)

plt.xlabel('Rain Today', fontsize=15)
plt.ylabel('Count', fontsize=15)
plt.title('Rain Today - Rain Tomorrow', fontsize=20)
plt.xticks(rotation=0, fontsize=12)
plt.yticks(fontsize=12)
plt.show()
```
![](https://scontent.fsgn2-1.fna.fbcdn.net/v/t39.30808-6/323274417_3471242959773060_754192413222184919_n.jpg?_nc_cat=107&ccb=1-7&_nc_sid=730e14&_nc_ohc=NWYmjpG21K0AX-Fz_uR&_nc_ht=scontent.fsgn2-1.fna&oh=00_AfDCbu1gjGTB6kkVhq7qO_Dfqiqgyr8wCxqO2puO5RtMFQ&oe=63C07E11)

```py 
# thống kê lượng mưa theo tháng
rain['Date'] = pd.to_datetime(rain['Date'])
rainfall =[rain['Date'].dt.year, rain['Date'].dt.month, rain['Rainfall']]
headers = ['Year', 'Month', 'Rainfall']
rain_df = pd.concat(rainfall, axis=1, keys=headers)
plt.figure(figsize=(8,4))
a = rain_df.groupby('Month').agg({'Rainfall':'sum'})
a.plot(kind='bar', color='pink')
plt.title('lượng mưa trong 1 tháng', fontsize=25)
plt.xlabel('Month', fontsize=20)
plt.ylabel('Rainfall (in mm)', fontsize=20)
plt.xticks(rotation=0)
plt.show()
```
![](https://scontent.fsgn2-4.fna.fbcdn.net/v/t39.30808-6/324335296_1236670713590765_8056266185610680102_n.jpg?_nc_cat=101&ccb=1-7&_nc_sid=730e14&_nc_ohc=Ohml8CyE7YgAX-2MOzO&_nc_oc=AQldFDWIMDUV5yctgHO203kKFRzmTsTpDhVCE0HiSpl3mK8f6uXg_z1RFdCYEkdnW-Q&_nc_ht=scontent.fsgn2-4.fna&oh=00_AfCrceKLL1StDOwRsE04PdxkphYWqd_tSkpF9XbA9IoraQ&oe=63BFF169)

```py
# lượng mưa theo năm 
plt.figure(figsize=(8,4))
a = rain_df.groupby('Year').agg({'Rainfall':'sum'})
a.plot(kind='bar', color='purple')
plt.title('Lượng mưa theo năm', fontsize=25)
plt.xlabel('Year', fontsize=20)
plt.ylabel('Rainfall (in mm)', fontsize=20)
plt.xticks(rotation=0)
plt.show()
```
![](https://scontent.fsgn2-4.fna.fbcdn.net/v/t39.30808-6/323640154_3325686464338128_3279593300219348627_n.jpg?_nc_cat=101&ccb=1-7&_nc_sid=730e14&_nc_ohc=RikqKfMF69QAX9fn62L&_nc_ht=scontent.fsgn2-4.fna&oh=00_AfATw7ATB0IsfWy5HibIFK8LErSOmirjJf8yxXHl6vMcfA&oe=63C1993A)

```py
# Thống kê nhiệt độ cao nhất và thấp nhất

fig, ax = plt.subplots(1, 2, figsize=(15,5))

# MinTemp
sns.distplot(rain['MinTemp'], ax=ax[0])
ax[0].set_title("Minimum Temperature")
# MaxTemp
sns.distplot(rain['MaxTemp'], ax=ax[1])
ax[1].set_title("Maximum Temperature")

```

![](https://scontent.fsgn2-8.fna.fbcdn.net/v/t39.30808-6/323866060_861987671715053_4785322054252018153_n.jpg?_nc_cat=102&ccb=1-7&_nc_sid=730e14&_nc_ohc=fTl8xJvOFxMAX-VxKKU&_nc_ht=scontent.fsgn2-8.fna&oh=00_AfC0P2tMwNpfw8hvVxndLYQUNpq2UA7l0qSMMFeCIIo0Rg&oe=63C0BDE7)

```py
#headmap 
plt.figure(figsize=(20,9))
sns.heatmap(rain.corr(method='pearson'),annot=True)

```


>![](https://scontent.fsgn2-4.fna.fbcdn.net/v/t39.30808-6/324308149_1233919684209851_6898636663263980159_n.jpg?_nc_cat=109&ccb=1-7&_nc_sid=730e14&_nc_ohc=sN386es9-pAAX8-i_Qu&tn=Fxsbeo8P-gREppb6&_nc_ht=scontent.fsgn2-4.fna&oh=00_AfBQaS8oVUyzBJgv7_dlEpGb7wQQ7it93dO7IWINzTdOuA&oe=63C17D8E)

>## Predict 
>```py
>from sklearn.preprocessing import LabelEncoder
>rain['Date'] = pd.to_datetime(rain['Date'],infer_datetime_format=True)
>rain['Date'] = rain['Date'].apply(lambda x: x.toordinal())
>
>encoder = LabelEncoder()
>for col in rain.columns[[i==object for i in rain.dtypes]]:
>    rain.loc[:,col] = encoder.fit_transform(rain[col])
>
