# Lab4_Test
This github repo will show documentation and commit to lab4

## Issues
My first challange was to find an API, so I googled around and found a Github repo that had a list full of APIs. I am using deck of cards API.


# Below is me testing a response request to see how calling an API works.
import requests
import json 

BASE_URL = "https://deckofcardsapi.com/api/deck/new"

response = requests.get(BASE_URL)

if response.status_code == 200:
    data = response.json()
    
    print(json.dumps(data, indent=4))
    
else:
    print(f"Error: {response.status_code}")

#I made a cleaner version of the api called above in line 14. I turned it into a function
def Create_Deck():
    response = requests.get(f"{BASE_URL}new/shuffle/?deck_count=1")
    data = response.json()

