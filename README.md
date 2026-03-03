# Lab4_Test
This GitHub repo will show a demonstration of commmits and documentation

## Issues
My first challenge was to find an API, so I googled around and found a Github repo that had a list of APIs. I am using deck of cards API.

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


# My second challenge was trying to draw cards and retrieving the card information.
### I did a quick google search and saw on the documentation that I will have to manually make a cards list since the API does not return numeric ranking but just strings.

    def CreateDeck():
    response = requests.get(BASE_URL + "new/shuffle/?deck_count=1")
    data = response.json()
    return data["deck_id"]



# Function to call API to draw cards 
    def DrawCards(deck_id):
    response = requests.get(BASE_URL + deck_id + "/draw/?count=2")
    data = response.json()
    return data["cards"], data["remaining"]

# Ranking system for cards that are strings.  
    def ConvertValues(value):
    if value == "ACE":
        return 14
    elif value == "KING":
        return 13
    elif value == "QUEEN":
        return 12
    elif value == "JACK":
        return 11
    else:
        return int(value)
  
# Function to get the highest value card 
    def GetHighest(cards):
    highest = 0
    for card in cards:
        number = ConvertValues(card["value"])
        if number > highest:
            highest = number
    return highest
        
# Main Program ( Will be split into multiple parts explaining how the API's work in action)
## Main Part One - welcomes player to the game and call method CreateDeck that contains an API to make a new deck/shuffle. Prompts the user to "bet amount" 
    def main(): -- main function
    print("Welcome to War, Have ya money ready!")
    money = 100
    deck_id = CreateDeck()

    while money > 0:
        print("\nYou have $", money)

        try:
            bet = int(input("Enter your bet amount: "))
        except:
            print("Invalid input.")
            continue

        if bet > money or bet <= 0:
            print("Invalid bet amount.")
            continue

            print("Cards remainig:", remaining)
        
## Main Part Two - After user enters "bet amount." DrawCards() Function is then called which contsains an API that hold card values and suit, deck_id, and remaining amount of cards. - It then compares players card value against the dealer's cards. Person with the higher value card wins. Player can play again as long as money balance is greater than 0. if not they can restart a new game and CreateDeck() is called and sends a request using an API.
        player_cards, remaining = DrawCards(deck_id)
        dealer_cards, remaining = DrawCards(deck_id)
        print("Cards remainig:", remaining)
        

        print("\nPlayer Cards:")
        for card in player_cards:
            print(card["value"], "of", card["suit"])

        print("\nDealer Cards:")
        for card in dealer_cards:
            print(card["value"], "of", card["suit"])

        player_high = GetHighest(player_cards)
        dealer_high = GetHighest(dealer_cards)

        if player_high > dealer_high:
            print("\nYou win this round!")
            money += bet
        elif dealer_high > player_high:
            print("\nDealer wins this round!")
            money -= bet
        else:
            print("\nTie! No money lost.")

        if remaining < 0:
            print("\nReshuffling deck...")
            deck_id = CreateDeck()
           

        again = input("\nPlay again? (y/n): ").lower()
        if again != "y":
            break

    print("\nGame Over. Final Balance: $", money)


    

