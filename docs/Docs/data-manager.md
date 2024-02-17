```python title="data_manager.py"

import requests
import time
sheety_endpoint = "https://api.sheety.co/6412b111864fc4fd885a00370c1e4359/flightDeals/prices"

class DataManager:
#This class is responsible for talking to the Google Sheet.

    def __init__(self) -> None:
        self.sheet_data = {}

    def get_sheet_data(self):
        data = requests.get(url= sheety_endpoint)
        self.sheet_data = data.json()["prices"]
        return self.sheet_data

    def update_iATA_codes(self):
        """Updated Google sheet with missing iATA Codes"""
        for city in self.sheet_data:
            new_data = {
                "price": {
                    "iataCode" : city["iataCode"]
                }
            }
            # time.sleep(1)
            response = requests.put(url=f"{sheety_endpoint}/{city['id']}", json=new_data)
            # print(response.text)
```
