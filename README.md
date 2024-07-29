  ### FOOD COST DELIVERY ANALYSIS
```
import pandas as pd
df=pd.read_csv("food delivery costs.csv")
df
```
![image](https://github.com/user-attachments/assets/d1386477-3a61-4e94-8dc4-1e81751f8b02)
```
df.head()
```
![image](https://github.com/user-attachments/assets/d79a71a6-a36f-46e5-b56e-caf6a680e878)
```
df.info()
```
![image](https://github.com/user-attachments/assets/6c6e30b0-1374-46ef-920f-99589864c9ba)
```
#cleaning data
df["Order Date and Time"]=pd.to_datetime(df["Order Date and Time"])
df.info()
```

![image](https://github.com/user-attachments/assets/ff008042-dacd-4d3c-a58e-a5b7aeb4ccd3)

```
df["Delivery Date and Time"]=pd.to_datetime(df["Delivery Date and Time"])
df.info()
```
![image](https://github.com/user-attachments/assets/dc1d736a-d6c0-4c39-b56f-3bebe659e147)

```
def extract(val):
  slt=str(val).split(" ")
  return slt[0]
df["Discounts and Offers"]=df["Discounts and Offers"].apply(extract)
df.head()
```

![image](https://github.com/user-attachments/assets/26799d66-023f-4515-842e-af34bc40c7b5)

```
def remove_perc(val):
  if "%" in val:
    a=val.replace("%","")
    return float(a)
  else:
    return float(val)
df["Discounts and Offers"]=df["Discounts and Offers"].apply(remove_perc)
df.head()
```

![image](https://github.com/user-attachments/assets/10619fa0-545a-42e4-9270-de6f7c04c7cc)

```
df.loc[(df["Discounts and Offers"]<=15),"Discounts and Offers"]=(df["Discounts and Offers"]/100)*df["Order Value"]
df.head()
```

![image](https://github.com/user-attachments/assets/d2b1b293-b079-4e53-ac79-67059c6b9d68)

```
df["Discounts and Offers"]=df["Discounts and Offers"].fillna(0)
df.head()
```

![image](https://github.com/user-attachments/assets/015e1f8b-5b87-4399-b665-bd28bc621214)

```
df["Cost"]=df["Delivery Fee"] + df["Discounts and Offers"]+df["Payment Processing Fee"]
df.head()
```
![image](https://github.com/user-attachments/assets/5fa88f72-13a3-4ee2-a4c4-d18ce1419f77)

```
df["Profit"]=df["Commission Fee"]-df["Cost"]
df.head()
```

![image](https://github.com/user-attachments/assets/e3342953-939e-439e-ba26-d6537e5e1449)


```
df["Profit"].sum()
```
![image](https://github.com/user-attachments/assets/95a7b57a-d9f9-49d6-ab44-ca93b5980603)

```
cost_dist=df[["Delivery Fee","Payment Processing Fee","Discounts and Offers"]].sum()
cost_dist
```
![image](https://github.com/user-attachments/assets/65857a7a-c5dc-464a-8f95-f5b65d2c3e51)

```
import matplotlib.pyplot as plt
plt.figure(figsize=(3,3))
plt.pie(cost_dist,labels=cost_dist.index,autopct="%1.1f%%")
plt.show()
```
![image](https://github.com/user-attachments/assets/17a700fc-ff62-47e8-a9cc-72b87918564e)
```
information=df[["Commission Fee","Cost","Profit"]].sum()
information
```
![image](https://github.com/user-attachments/assets/43920750-722a-49c0-9e5d-bc3ef228bc50)
```
plt.figure(figsize=(3,3))
plt.bar(information.index,information)
plt.show()
```
![image](https://github.com/user-attachments/assets/57e85503-fa73-4c9b-8a02-85d1d8019041)
