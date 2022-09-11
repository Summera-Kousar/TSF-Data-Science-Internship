# The Sparks Foundation - GRIP
## Data Science & Business Analytics Intern
## Task 3 : Exploratory Data Analysis -Retail
In this exploratory task have tried to analyse the reatil data and got insights from the available data.
### STEP 1: IMPORTING THE STANDARD LIBRARIES
```py
import pandas as pd 
import numpy as np 
import plotly.express as px
import matplotlib.pyplot as plt
import seaborn as sns
from plotly.subplots import make_subplots
import plotly.graph_objs as go
import plotly.offline as pyo
pyo.init_notebook_mode()


import warnings
warnings.filterwarnings("ignore")
```
#### STEP 2: LOAD THE DATASET
```py
df = pd.read_csv('SampleSuperstore.csv')
```
### STEP 3: DATA PRE-PROCESSING
```py
df.head()
```
![S1](https://user-images.githubusercontent.com/102469583/189522118-33ccbdc3-f88d-4632-bd03-4268d926c17c.PNG)
```py
df.info()
```
![S2](https://user-images.githubusercontent.com/102469583/189522193-1fefcd95-af7b-4ff2-b1a6-467ff4cb3fcf.PNG)
```py
df.isnull().sum()
```
![S3](https://user-images.githubusercontent.com/102469583/189522231-f29a978c-6d8a-4091-a519-5c1ab7af342f.PNG)
```py
df.shape
```
![S4](https://user-images.githubusercontent.com/102469583/189522285-5d2304fd-3f6b-4685-b108-9f200e9b8ccc.PNG)
```py
df.columns
```
![S5](https://user-images.githubusercontent.com/102469583/189522325-2f3b090d-5c58-42e8-8f63-132ccbf853d4.PNG)
```py
df['Profit_Margin']= df['Profit']/df['Sales']
```
### STEP 4: Exploratory Data Analysis
```py
ax2= px.treemap(df,path=['State'],title="Top States by Sales and Profit")
ax2.show()
```
![S6](https://user-images.githubusercontent.com/102469583/189522416-fb669840-e394-4a46-b2c3-dc912c7fabc1.PNG)
## Observations:
- Here we can see that **California, New York and Texas** are high sales and profit states as compared to other states.
- And **Kansas, Idaho, Montana, South Dakota, Vermont, Maine, District of Columbia** and West Verginia are low sale and profit states.
```py
ax2= px.treemap(df,path=['City'],title="Top Cities by Sales and Profit")
ax2.show()
```
![S7](https://user-images.githubusercontent.com/102469583/189522524-3fc5aea4-1fdf-4d3e-9032-697d36c55714.PNG)
#### Observation:
- Here we can observe that **New York, Los Angeles, Philadelphia, San Francisco and Settle** have high Sale and Profit.
- There are alot of cities which we can observe from visulization with low Sales and profit where we need to take a step to improve their sales and profit.
```py
fig=px.pie(df,values='Profit_Margin',names='Region',color_discrete_sequence=px.colors.sequential.RdBu)
fig.update_layout(title='Profit By State',font_size=15,title_x=0.45)
fig.update_traces(textfont_size=15,textinfo='percent')
fig.show()
```
![S8](https://user-images.githubusercontent.com/102469583/189522618-4053bd6e-6b4d-496f-b542-07116c5df578.PNG)
#### Observaions:
- **West** has high Profit Margin as compared to other regions.
```py
fig = make_subplots(rows=1, cols=2, specs=[[{'type':'domain'}, {'type':'domain'}]])
fig.add_trace(go.Pie(labels=df['Category'], values=df['Profit']),
              1, 1)
fig.add_trace(go.Pie(labels=df['Category'], values=df['Sales']),
              1, 2)
fig.update_traces(hole=.3, hoverinfo="label+percent+name")

fig.update_layout(
    title_text="Sales and Profit by Category",
    # Add annotations in the center of the donut pies.
    annotations=[dict(text='Profit', x=0.18, y=0.5, font_size=20, showarrow=False),
                 dict(text='Sales', x=0.82, y=0.5, font_size=20, showarrow=False)])
fig.show()
```
![S9](https://user-images.githubusercontent.com/102469583/189522683-d9ea8c9f-74ca-40e1-882e-28c23dbe8b42.PNG)
### Observations:
- **Technology** have **high Sales and Profit** compared to other Categories.
-  **Office** Supplies have **low Sales but high Profit**.
- **Furniture** have **high Sales but low profit**.
```py
fig=px.pie(df,values='Discount',names='Category',color_discrete_sequence=px.colors.sequential.RdBu, hole =.4)
fig.update_layout(title='Profit By State',font_size=15,title_x=0.45, annotations=[dict(text='Discount',  font_size=20, showarrow=False)])
fig.update_traces(textfont_size=15,textinfo='percent')
fig.show()
```
![S10](https://user-images.githubusercontent.com/102469583/189522725-8ad2aba6-f924-479f-8254-d6fb6675dbed.PNG)
#### Observations:
- **Here we can understand why Office Supplies have high profit. The Reason behind is that Office Supplies are offering more 
discount. There sales are still less but because of discount their profit is high as compare to Furniture.**
- **Here is another point to be noticed that technology is not offering too much discout as compared to other categories but 
their profit is still high because technology have high sales as compared to others.**
```py
fig = make_subplots(rows=1, cols=2, specs=[[{'type':'domain'}, {'type':'domain'}]])
fig.add_trace(go.Pie(labels=df['Sub-Category'], values=df['Profit']),
              1, 1)
fig.add_trace(go.Pie(labels=df['Sub-Category'], values=df['Sales']),
              1, 2)
fig.update_traces(hole=.3, hoverinfo="label+percent+name")

fig.update_layout(
    title_text="Sales and Profit by Sub-Category",
    # Add annotations in the center of the donut pies.
    annotations=[dict(text='Profit', x=0.18, y=0.5, font_size=20, showarrow=False),
                 dict(text='Sales', x=0.82, y=0.5, font_size=20, showarrow=False)])
fig.show()
```

![S11](https://user-images.githubusercontent.com/102469583/189522788-7ce9ffec-183b-406a-854b-a1e708172387.PNG)
#### Observations:
- **Copiers, Phones, Accessories, Paper and Binder** have **high Profit.** 
- **Phones, Accessories, Storage and Tables** have **high Sales.**
```py
plt.figure(figsize = (15,10))
p = sns.barplot(data=df, x ='Sub-Category', y ='Discount', palette = "bright", ci=None)
sns.set_theme(style = "darkgrid")
plt.xticks(rotation = 50)
plt.xlabel('Sub-Category',fontsize=15)
plt.ylabel('Discount',fontsize=15)
plt.title('Discount By Sub-Category',fontsize=18)
plt.show(p)
```
![S12](https://user-images.githubusercontent.com/102469583/189522923-8712fa99-4fb0-43bf-8277-5cc0fd417de2.PNG)
### Observations:
- **Binder, Machine and Tables** offering more **discount** as compared to other Sub-Categories.
```py
plt.figure(figsize = (10,10))
p = sns.scatterplot(data=df, x ='Ship Mode', y ='Sales', palette = "bright", ci=None)
sns.set_theme(style = "darkgrid")
plt.xticks(rotation = 50)
plt.xlabel('Ship Mode',fontsize=15)
plt.ylabel('Sales',fontsize=15)
plt.title('Sales By Ship Mode',fontsize=18)
plt.show(p)
```
![S13](https://user-images.githubusercontent.com/102469583/189522989-18bdb3ca-9aff-4abb-8bd7-817d79a580d3.PNG)
### Conclousion:
- Focusing on **Standard Class** as **shipment mode** more as it brings **most profit and sales.**
- More **Discount** should be offered for **technology** that will **increase profit and sales more.**
- Uplifting the **Sales** in the **States** that are facing losses such as **Kansas, Idaho, Montana, South Dakota, Vermont, Maine, District of Columbia and West Verginia.**
- Keeping focus over the **cities** with most buyers, **sales and profit** such as **California and New york.**
- **Increasing sale**s in **cities** that are facing losses such as **Tennessee, Colorado, North Carolina, Ilionis, Pennsylvania, Ohio and Texas.**

