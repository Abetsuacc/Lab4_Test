# Lab4_Test
This github repo will show documentation and commit to lab4

## Issues
My first challenge was to find an API, so I googled around and found a Github repo that had a list full of APIs. I am using deck of cards API.
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
def CreateDeck():
    response = requests.get(f"{BASE_URL}new/shuffle/?deck_count=1")
    data = response.json()


# My first challenge was trying to draw cards and retrieving the card information. I did a quick google search and saw on the documentation that I will have to manually make a cards list since the API does not return numeric ranking but just strings.
I run into the follow error when it comes to returning the cards.
def DrawCards():
    response = requests.get(BASE_URL + "new/shuffle/?deck_count=1")
    data = response.json()
    return data["deck_id"]
    // changed formatting to make it easier to read and returned card_Id

    data = response.json()

