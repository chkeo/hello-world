# hello-world
just another repository

import pandas as pd
from pandas import ExcelWriter
from pandas import ExcelFile
import numpy as np


                    '''  USING COMP PROVIDER XLS  '''
                        

''' A function to combine Affiliate and Dr. ID to assist in Original vlookups
    by using EEID as an INDEX  '''

''' read excel file into Python '''
xls = pd.ExcelFile('2017v2018 Comp by Provider - FADG - October 2018 - Updated v2 Keo.xlsx')

''' Create new dataframes by specfic sheets from the workbook '''
df_main = pd.read_excel(xls, 'Payroll Pay')
df_lookup = pd.read_excel(xls, 'Lookup')

''' Subsetting the lookup columns to Dr. ID, EEID, & affiliate '''

df_lookup = df_lookup[['Dr. ID', 'EEID', 'Affiliate']]
df_lookup.head()

'''  Create new column according to rows of original sheet to 
    replace with affiliate + Dr. ID '''

df_lookup['AFFDR'] = df_lookup.shape[0]*['NA']
df_lookup

''' Create new columns AFFDR to assist in EEID lookup  '''
    ''' Concatenate string and integer columns '''
     
df_lookup['AFFDR'] = df_lookup['Affiliate']+ "-"+ df_lookup['Dr. ID'].astype(str)
df_lookup['AFFDR'].head()


'''    EXPORT XLS FILE w/ Affiliate-Dr. ID   '''

writer = ExcelWriter('vlookup.xlsx')
df_lookup.to_excel(writer,'Sheet1',index=False)
writer.save()

