```python title="flight_search.py"
import requests

TEQUILA_ENDPOINT = "https://tequila-api.kiwi.com/locations/query"
TEQUILA_API_KEY = "BmqWtvMH7gDhgcPKAfTGkNxn3BDXMOtw"

headers = {
    "accept" : "application/json",
    "apikey" : TEQUILA_API_KEY
}


"locale=de-DE&location_types=airport&limit=1&active_only=true"

class FlightSearch:

    #This class is responsible for talking to the Flight Search API.
    def getiATA_code(self, city_name) -> str:
        return self.get_flight_data(city_name)["id"]


    def get_flight_data(self, city_name = "Tokio"):
        self.payload = {
            "term" : city_name,
            "locale" : "en-US",
            "location_types" : "airport",
            "limit" : "1",
            "active_only" : "true"
        }
        data = requests.get(url=TEQUILA_ENDPOINT, params=self.payload, headers=headers)
        return data.json()["locations"][0]


```
