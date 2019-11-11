#Import packages
import requests
import pandas as pd
import json
from datetime import datetime, timedelta
import time


def CallAPI(url):
    r = requests.get(url)
    content = json.loads(r.content.decode('utf-8'))

    # If want to keep calling this API until return the normal data
    # while 'rows' not in content.keys():
    #     time.sleep(60)
    #     r = requests.get(url)
    #     content = json.loads(r.content.decode('utf-8'))

    Transaction_Content = content['rows']

    # Create a dataframe 
    Feature_List = list(Transaction_Content[0].keys())
    new_dic = {}
    for feature in Feature_List:
        new_dic[feature] = list(Transaction_Content[i][feature] for i in range(len(Transaction_Content)))
    
    Transaction_Data = pd.DataFrame.from_dict(new_dic)

    return Transaction_Data


Transaction_Data = CallAPI('https://data.ripple.com/v2/network/fees?interval=day&limit=1000&descending=true')

# Write it to csv file
Transaction_Data.to_csv('Transaction_Data.csv')
