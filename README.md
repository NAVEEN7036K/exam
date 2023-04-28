# exam
Loading...
ML 1A
ML 1A_
[ ]

EDA
Aim: To understand the relationship between variables and gather the insights about the data

Description:Exploratory data analysis refers to the process of performing initial investigations on data, so as to discover patterns, to spot anomolies, to test hypothesis and to check assumptions with the help of summary statistics and graphical assumptions. Here in this experiment the techniques such as Datacleaning, outlier analysis, corelation analysis, univariate, bivariate, and multivariate analysis In this analysis I have used the "Stores.csv" dataset.

[ ]
#1
import pandas as pd
import numpy as np
df=pd.read_csv("/content/drive/MyDrive/ML LAB DATASETS/Stores_URK20AI1036.csv")
[ ]
#2
df.head(5)


[ ]
df.tail()

[ ]
#3
df.shape
(50, 15)
[ ]
#4
numeric=df._get_numeric_data().columns
len(numeric)

9
[ ]
catCols = df.select_dtypes("object").columns
len(catCols)
6
[ ]
catCols
Index(['Branch', 'City', 'Customer', 'Gender', 'Product line', 'Payment'], dtype='object')
[ ]
cols=df.columns
cate=list(set(cols) - set(numeric))
print(cate)
['Product line', 'City', 'Branch', 'Gender', 'Customer', 'Payment']
[ ]
#5
#min,max and mean of numeical columns
df.describe()

[ ]
#6
null=df.columns.isnull().sum()
print(null)
0
[ ]
#7 
import matplotlib.pyplot as plt
summary=df['Age'].describe()
plt.boxplot(summary)
plt.figure(figsize=(10,10))

[ ]
#8
from scipy import stats
zscore=stats.zscore(df['Quantity'])
print(zscore)
0    -0.174041
1    -0.314396
2    -0.174041
3    -0.103863
4     3.545376
5    -0.174041
6    -0.244218
7     0.036492
8    -0.524929
9    -0.454751
10   -0.384574
11   -0.384574
12   -0.314396
13    0.036492
14    0.036492
15   -0.244218
16   -0.174041
17   -0.244218
18   -0.454751
19   -0.524929
20   -0.314396
21    3.194487
22   -0.524929
23   -0.314396
24   -0.454751
25   -0.103863
26   -0.595107
27   -0.524929
28   -0.314396
29   -0.033685
30   -0.314396
31   -0.033685
32   -0.103863
33   -0.524929
34   -0.384574
35   -0.595107
36   -0.314396
37    3.334843
38   -0.103863
39   -0.103863
40   -0.595107
41   -0.524929
42   -0.244218
43   -0.103863
44   -0.524929
45   -0.384574
46   -0.033685
47    3.264665
48   -0.244218
49   -0.244218
Name: Quantity, dtype: float64
[ ]
plt.boxplot(df['Quantity'])

[ ]
#9
cols=df[['Age','Price','Tax','Quarterly_Tax','Rating']]
corr=cols.corr()
print(corr)
                    Age     Price       Tax  Quarterly_Tax    Rating
Age            1.000000  0.258092  0.319308      -0.178355 -0.219052
Price          0.258092  1.000000  0.614725      -0.105419 -0.167489
Tax            0.319308  0.614725  1.000000       0.170913 -0.126537
Quarterly_Tax -0.178355 -0.105419  0.170913       1.000000  0.306072
Rating        -0.219052 -0.167489 -0.126537       0.306072  1.000000
[ ]
corr.style.background_gradient(cmap ='coolwarm')

[ ]
#10
cor_matrix = df.corr().abs()
print(cor_matrix)
upper_tri = cor_matrix.where(np.triu(np.ones(cor_matrix.shape),k=1).astype(np.bool))
print(upper_tri)
to_drop = [column for column in upper_tri.columns if any(upper_tri[column] > 0.60)]
print(); print(to_drop)
               Unit_price  Quantity       Tax     Total      cogs    Rating  \
Unit_price       1.000000  0.052122  0.614725  0.614725  0.614725  0.167489   
Quantity         0.052122  1.000000  0.232583  0.232583  0.232583  0.315102   
Tax              0.614725  0.232583  1.000000  1.000000  1.000000  0.126537   
Total            0.614725  0.232583  1.000000  1.000000  1.000000  0.126537   
cogs             0.614725  0.232583  1.000000  1.000000  1.000000  0.126537   
Rating           0.167489  0.315102  0.126537  0.126537  0.126537  1.000000   
Age              0.258092  0.025231  0.319308  0.319308  0.319308  0.219052   
Quarterly_Tax    0.105419  0.030031  0.170913  0.170913  0.170913  0.306072   
Price            1.000000  0.052122  0.614725  0.614725  0.614725  0.167489   

                    Age  Quarterly_Tax     Price  
Unit_price     0.258092       0.105419  1.000000  
Quantity       0.025231       0.030031  0.052122  
Tax            0.319308       0.170913  0.614725  
Total          0.319308       0.170913  0.614725  
cogs           0.319308       0.170913  0.614725  
Rating         0.219052       0.306072  0.167489  
Age            1.000000       0.178355  0.258092  
Quarterly_Tax  0.178355       1.000000  0.105419  
Price          0.258092       0.105419  1.000000  
               Unit_price  Quantity       Tax     Total      cogs    Rating  \
Unit_price            NaN  0.052122  0.614725  0.614725  0.614725  0.167489   
Quantity              NaN       NaN  0.232583  0.232583  0.232583  0.315102   
Tax                   NaN       NaN       NaN  1.000000  1.000000  0.126537   
Total                 NaN       NaN       NaN       NaN  1.000000  0.126537   
cogs                  NaN       NaN       NaN       NaN       NaN  0.126537   
Rating                NaN       NaN       NaN       NaN       NaN       NaN   
Age                   NaN       NaN       NaN       NaN       NaN       NaN   
Quarterly_Tax         NaN       NaN       NaN       NaN       NaN       NaN   
Price                 NaN       NaN       NaN       NaN       NaN       NaN   

                    Age  Quarterly_Tax     Price  
Unit_price     0.258092       0.105419  1.000000  
Quantity       0.025231       0.030031  0.052122  
Tax            0.319308       0.170913  0.614725  
Total          0.319308       0.170913  0.614725  
cogs           0.319308       0.170913  0.614725  
Rating         0.219052       0.306072  0.167489  
Age                 NaN       0.178355  0.258092  
Quarterly_Tax       NaN            NaN  0.105419  
Price               NaN            NaN       NaN  

['Tax', 'Total', 'cogs', 'Price']
<ipython-input-16-22ea98dfc234>:4: DeprecationWarning: `np.bool` is a deprecated alias for the builtin `bool`. To silence this warning, use `bool` by itself. Doing this will not modify any behavior and is safe. If you specifically wanted the numpy scalar type, use `np.bool_` here.
Deprecated in NumPy 1.20; for more details and guidance: https://numpy.org/devdocs/release/1.20.0-notes.html#deprecations
  upper_tri = cor_matrix.where(np.triu(np.ones(cor_matrix.shape),k=1).astype(np.bool))
[ ]
#11
import warnings
warnings.filterwarnings('ignore')
import seaborn as sb
skew=df.Tax.skew()
sb.distplot(df['Tax'])
print(f'The skewness of tax is {skew}')

[ ]
#12
#Perform univariate analysis for categorical variable “City” using bar plot with counts
sb.countplot(df['City'])


[ ]
#13
sb.swarmplot(df['Rating'],color='Green')


[ ]
sb.violinplot(df['Rating'])

[ ]
#14
x=df['Tax']
y=df['cogs']
plt.scatter(x,y)

[ ]
#15
x=df['Gender']
y=df['Age']
sb.barplot(x,y)

[ ]
#15
sb.countplot(x)

[ ]
sb.countplot(y)

[ ]
pd.crosstab(x,y)

Double-click (or enter) to edit

[ ]
#16
sb.pairplot(data=df,vars=['Age', 'Price', 'Tax', 'Rating','cogs'],hue='City')

*************************************************************************************************************************************************************


