# predictive maintenance
time series sensor data analysis for predictive maintenance

# Links

# Installation
The data is in S3 bucket, so install the below packages.
Also the data is saved as parquet formation.
```python

!conda update -n base -c defaults conda -y
!conda install -c anaconda fastparquet -y
!conda install -c conda-forge python-snappy -y
```
```python
import pandas as pd
import fastparquet as fp
import s3fs
from matplotlib import pyplot as plt
```
Now, you can load parquet format files from s3 bucket.

# Usage
This data set has so many sensors value: 626 columns. 
So I used several methods to make the data set small. 
1. Delete NAN values.
> Delete 320 columns
```python
mask = (dfa.isna().sum()>0)
m_df=pd.DataFrame(mask,columns=['TF'])
keep_list=m_df[m_df.TF==0].index
```

2. Delete columns when the columns' standard deviation = 0 (It means the column is a constant value)
> Delete 32 columns
```python
mask2 = df_sm.std()==0
keep_list2 = mask2[mask2==0].index
```

3. Comparison between the data before system shutdown and after the shutdown.
> Turned out meaningless process.
```python
df_s = df_sm3.iloc[:2000,]
df_e = df_sm3.iloc[255322:257322,]
deviation = abs(df_s.mean())*1 - abs(df_e.mean())*1
```



