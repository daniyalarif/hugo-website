
---
title: Jupyter Test
author: ''
date: '2021-09-18'
slug: jupyter-test
categories: []
tags: []
subtitle: ''
summary: ''
authors: []
lastmod: '2021-09-18T23:10:57+02:00'
featured: no
image:
  caption: ''
  focal_point: ''
  preview_only: no
projects: []
---


```python
# importing libraries
import random
import time
import pandas as pd
import numpy as np
from selenium.webdriver import ActionChains
from selenium import webdriver
from selenium.webdriver.support.select import Select
from bs4 import BeautifulSoup

pd.set_option('display.max_rows', 500)
pd.set_option('display.max_columns', 500)
pd.set_option('display.width', 1000)
```

### Making Table as a function


```python
def table():
    row_count = len(driver.find_elements_by_xpath('//*[@id="rapportDatasett"]/table/tbody/tr'))
    col_count = len(driver.find_elements_by_xpath('//*[@id="rapportDatasett"]/table/thead/tr[1]/th'))

    #list of table headers
    list_headers = []

    thead_first_part = "//*[@id='rapportDatasett']/table/thead/tr[1]/th["
    thead_second_part = "]"

    for n in range(1,col_count+1):
        thead_final_path = thead_first_part + str(n) + thead_second_part
        thead_table_data = driver.find_element_by_xpath(thead_final_path).text
        list_headers.append(thead_table_data)

    #list of elements of the table
    elements = []

    first_part = "//*[@id='rapportDatasett']/table/tbody/tr["
    second_part = "]/td["
    third_part = "]"

    for n in range(1,row_count):
        for m in range(1,col_count+1):
            final_path = first_part + str(n) + second_part + str(m) + third_part
            table_data = driver.find_element_by_xpath(final_path).text
            elements.append(table_data)      

    # making elements to data frame
    div = int(len(elements)/(len(list_headers)))
    list_ele = np.array_split(elements, div)
    list_headers = np.array(list_headers)
    df2 = pd.DataFrame(data=list_ele)
    df1 = pd.DataFrame(data=list_headers)
    df1=df1.transpose()
    df = pd.concat([df1, df2])
    df.columns = df.iloc[0]
    df = df[1:]

    level_1 = pd.DataFrame([l4_uni] * int(df.shape[0])) # changed
    level_1.rename(columns={0: 'Institusjonsnavn'}, inplace=True)

    df_2 = pd.concat([level_1, df], axis=1)
    return df_2
```

## Master

##### Master Applicants


```python
# # opening the selenium driver
# driver=webdriver.Chrome('D:\webdrivers\chromedriver.exe')

# #opening the website
# driver.get('https://dbh.nsd.uib.no/statistikk/rapport.action?visningId=132&visKode=false&admdebug=false&columns=arstall&index=1&formel=294&hier=insttype!9!instkode!9!fakkode!9!ufakkode!9!progkode&sti=&param=arstall%3D2021!8!2020!8!2019!9!dep_id%3D1!9!nivakode%3DM2!8!ME!8!MX!8!M5')
# driver.maximize_window()

# #sleep 3 sec
# time.sleep(2)

# clinks_p1 = driver.find_elements_by_xpath("//td[@class='text']/a") # links to capture from page/complete lists page 1

# list_links_l1 = [] # created list to store links level 1
# list_links_l2 = [] # created list to store links level 2
# list_links_l3 = [] # created list to store links level 3
# list_links_l4 = [] # created list to store links level 4

# for i in clinks_p1: # complete lists page 1
#     list_links_l1.append(i.get_attribute('href')) 
    
# for i in range(len(list_links_l1)): # from page 1 
    
#     driver.get(list_links_l1[i]) # page 2 opened 
#     time.sleep(2)
#     clinks_p2 = driver.find_elements_by_xpath("//td[@class='text']/a") # aggregating page 2 links from only university
#     #Show All links available in clinks_p2
    
#     for j in clinks_p2:
#         list_links_l2.append(j.get_attribute('href'))
        

# for i in range(len(list_links_l2)): # from page 2 
    
#     driver.get(list_links_l2[i]) # page 2 opened 
#     time.sleep(2)
#     clinks_p3 = driver.find_elements_by_xpath("//td[@class='text']/a") # aggregating page 2 links from only university
       
#     for j in clinks_p3:
#         list_links_l3.append(j.get_attribute('href'))        
        
# for i in range(len(list_links_l3)): # from page 3 
    
#     driver.get(list_links_l3[i]) # page 2 opened 
#     time.sleep(2)
#     clinks_p4 = driver.find_elements_by_xpath("//td[@class='text']/a") # aggregating page 2 links from only university
       
#     for j in clinks_p4:
#         list_links_l4.append(j.get_attribute('href'))        

# list_c = [] # list to store tables        

# for i in range(len(list_links_l4)):
#     driver.get(list_links_l4[i])
#     time.sleep(2)
#     l4_uni = driver.find_element_by_xpath('//*[@id="rapportSmuler"]/a[3]').text   
#     tbl = table()
#     list_c.append(tbl)
    
# data_final = pd.concat(list_c)
# data_final.reset_index(inplace=True)
# data_final = data_final.replace(np.nan, '', regex=True)
# data_final.to_excel("Data_Master_Applicants.xlsx")


# driver.quit() 
```
