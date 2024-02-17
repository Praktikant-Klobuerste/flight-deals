```python title="Python"
import requests
import datetime as dt
from pprint import pprint

TEQUILA_ENDPOINT = "https://api.tequila.kiwi.com/v2/search"
TEQUILA_API_KEY = "BmqWtvMH7gDhgcPKAfTGkNxn3BDXMOtw"

headers = {
    "accept" : "application/json",
    "apikey" : TEQUILA_API_KEY
}

class FormatDate:
    def __init__(self, future_days : int = 30*6) -> None:
        self.today = today = self.format_date(dt.datetime.now())
        self.future_date = self.format_date(dt.datetime.now() + dt.timedelta(future_days))

    def format_date(self, date):
        return date.strftime("%d/%m/%Y")


class FlightData:
    #This class is responsible for structuring the flight data.
    def __init__(self, nights_from = "7", nights_to = "28") -> None:
        self.depature_airport_code = "MUC"
        self.arrival_airport_code = "NRT"
        self.depature_city = ""

    def get_data(self):
        self.payload = {
        "fly_from" : self.depature_airport_code,
        "fly_to" : self.arrival_airport_code,
        "dateFrom" : FormatDate().today,
        "dateTo" : FormatDate().future_date,
        "flight_type" : "round",
        "curr" : "USD",
        "nights_in_dst_from" : "7",
        "nights_in_dst_to": "28",
        "limit" : "10",
        }


        response = requests.get(url = TEQUILA_ENDPOINT, params= self.payload, headers= headers)
        response.json()
        data = response.json()
        return data["data"]


# fd = FlightData()

# pprint(fd.get_data())
# print(fd.get_data()[0]["price"])
# print(fd.get_data()[0]])




# print(FormatDate().future_date)


```
