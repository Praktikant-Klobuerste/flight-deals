Hi

```python title="main.py"

#This file will need to use the DataManager,FlightSearch,
#FlightData, NotificationManager classes to achieve the program requirements.
import json

from data_manager import DataManager
from flight_data import FlightData
from flight_search import FlightSearch
from notification_manager import NotificationManager

dt = DataManager()
search = FlightSearch()
fd = FlightData()


# print(dt.sheet_data)
dt.get_sheet_data()
# pprint(dt.sheet_data)

#Cycles every row in Google Sheet
is_empty = False
Price_list = {}
for _ in dt.sheet_data:
    # if _["iataCode"] == "":
        # is_empty = True
    _["iataCode"] =  search.getiATA_code(_["city"])
    fd.arrival_airport_code = _["iataCode"]
    flight_info = fd.get_data()[0]
    print(_["iataCode"] ,flight_info["price"])

    Price_list[_["city"]] = {
                    "iATA Code" :  _["iataCode"],
                    "Price" : flight_info["price"],
                    "Airline" : flight_info["airlines"],
                    "Duration": flight_info["duration"],
                    "URL" : flight_info["deep_link"],
    }

with open(file = "./Price_list.json", mode= "w") as file:
    json.dump(Price_list, file, indent= 4)

# if is_empty:
dt.update_iATA_codes()

```
