import random
import math

# 11 = Jack
# 12 = Queen
# 13 = King

# always a full deck
deck = ["A", "A", "A", "A", 2, 2, 2, 2, 3, 3, 3, 3, 4, 4, 4, 4, 5, 5, 5, 5, 6, 6, 6, 6, 7, 7, 7, 7, 8, 8, 8, 8, 9, 9, 9, 9, 10, 10, 10, 10, 11, 11, 11, 11, 12, 12, 12, 12, 13, 13, 13, 13]

# will be reduced as cards are drawn
back_up = ["A", "A", "A", "A", 2, 2, 2, 2, 3, 3, 3, 3, 4, 4, 4, 4, 5, 5, 5, 5, 6, 6, 6, 6, 7, 7, 7, 7, 8, 8, 8, 8, 9, 9, 9, 9, 10, 10, 10, 10, 11, 11, 11, 11, 12, 12, 12, 12, 13, 13, 13, 13]

def flip_card(card):
  if card=="A":
    return "Ace"
  elif card==11:
    return "Jack"
  elif card == 12:
    return "Queen"
  elif card == 13:
    return "King"
  else:
    return str(card)


#introduction
print("Welcome to Acey Duecey, you'll be playing against two other players.")
starting_amount = int(input("How much money would you like everyone to start out with? "))

# initial variables
pot = 0
user_stack = starting_amount

#computer players
class Player:
  def __init__(self, name, cash):
    self.name = name
    self.cash = cash

  def take_ante(self):
    if self.cash>= 1:
      self.cash-=1
      global pot
      pot+=1
      

def collect_antes(player1, player2):
  global user_stack
  global pot
  player1.take_ante()
  player2.take_ante()
  user_stack-=1
  pot+=1

def show_information():
  print("--------------------------------------")
  print("You currently have " + str(user_stack) + " dollars")
  print("Comp1 has " + str(comp1.cash) + " dollars")
  print("Comp2 has " + str(comp2.cash) + " dollars")
  print("There is " + str(pot) + " dollars in the pot")
  print("--------------------------------------")



def user_plays():
  global back_up
  global pot
  global user_stack
  #reshuffling deck if needed
  if len(back_up) < 4:
    back_up[:] = deck
    print("**** Time to reshuffle the deck ****")
    print(len(back_up))
    
  #dealing the first and second cards
  first = back_up[random.randint(0, len(back_up)-1)]
  back_up.remove(first)
  print("The first card is a " + flip_card(first))
  # revaluing first ace
  if first == "A":
    print("This will be a low Ace")
    first=0
  
  second = back_up[random.randint(0, len(back_up)-1)]
  back_up.remove(second)
  print("The second card is a " + flip_card(second))
  # reevaluating second ace
  if second=="A":
    print("This will become a high Ace")
    second=14
    
  # if first and second are the same
  if first == second:
    higher_or_lower = input("Would you like to bet higher or lower than the card drawn? (H/L)  ").upper()
    
  # user inputs their bet based on border cards
  user_bet = int(input("How much would you like to bet?" ))
  if user_stack > 1:
    while (user_bet > (user_stack/2) or user_bet > pot):
      user_bet = int(input("You are only allowed to bet up to half of your stack and less than the amount that's in the pot. Please input another bet amount: "))
  else:
    while (user_bet > 1):
      user_bet = int(input("You only have 1 dollar left, either bet it or bet 0"))
    
  # ends round if user bets 0, continues if they bet
  if user_bet == 0:
    return
  else:
      
    # now we deal third card and change the balances
    third = back_up[random.randint(0, len(back_up)-1)]
    back_up.remove(third)
    print("The third card is a " + flip_card(third))

    if third == "A":
      if (first == 0 or second == 14) and not(first == 0 and second == 14):
        print("Posting on an Ace means you lose massively!")
        pot += user_bet*4
        user_stack -= user_bet*4
      elif first == 0 and second == 14:
        print("Unbelievable! You got 3 Aces and lose massively!")
        pot+= user_bet*4
        user_stack -= user_bet*4
      else:
        print("Ace always loses.")
        pot+= user_bet
        user_stack -= user_bet

    # if they're all the same
    elif third == second and second == first:
      print("Wow, all three are the same! You take a huge loss!")
      pot+= user_bet*3
      user_stack -= user_bet*3

    # if first two the same and third is greater
    elif second == first and third > second:
      if higher_or_lower == "H":
        print("You won!")
        pot -= user_bet
        user_stack += user_bet
      if higher_or_lower == "L":
        print("You lost")
        pot += user_bet
        user_stack -= user_bet
    # if first two are the same and third is lower
    elif second == first and third < second:
      if higher_or_lower == "H":
        print("You lost")
        pot += user_bet
        user_stack -= user_bet
      if higher_or_lower == "L":
        print("You won!")
        pot -= user_bet
        user_stack += user_bet

    # if third card equals either first or second
    elif third == second or third == first:
      print("You lost double!")
      pot += user_bet*2
      user_stack -= user_bet*2

    # if the third is between first and second
    elif (third > first and third < second) or (third <first and third>second):
      print("You won!")
      pot -= user_bet
      user_stack += user_bet

    # if third is less than the first and second
    elif third < first and third < second:
      print("You lost")
      pot += user_bet
      user_stack -= user_bet
    elif third > first and third>second:
      print("You lost")
      pot += user_bet
      user_stack -= user_bet


# simulates a computer playing
def comp_plays(computer):
  global back_up
  global pot
  #reshuffling deck if needed
  if len(back_up) < 4:
    back_up[:] = deck
    print("**** Time to reshuffle the deck ****")
    print(len(back_up))
    
    
  #dealing the first and second cards
  first = back_up[random.randint(0, len(back_up)-1)]
  back_up.remove(first)
  print(computer.name + "'s first card is a " + flip_card(first))
  # revaluing first ace
  if first == "A":
    print("This will be a low Ace")
    first=0
  
  second = back_up[random.randint(0, len(back_up)-1)]
  back_up.remove(second)
  print(computer.name + "'s second card is a " + flip_card(second))
  # reevaluating second ace
  if second=="A":
    print("This will become a high Ace")
    second=14

# if first and second are the same
  if first == second:
    if first>=8:
      higher_or_lower = "L"
      print("The computer chose lower")
      if computer.cash > pot:
        comp_bet = math.ceil(pot/3)
      else:
        comp_bet = math.ceil(computer.cash /4)
    else:
      higher_or_lower = "H"
      print("The computer chose higher")
      if computer.cash > pot:
        comp_bet = math.ceil(pot/3)
      else:
        comp_bet = math.ceil(computer.cash /4)
        
  # computer decides whether or not to bet
  elif abs(first-second)<=7:
    comp_bet = 0
  elif abs(first-second)>7 and abs(first-second)<10:
    if computer.cash > pot:
      comp_bet = math.ceil(pot/3)
    else:
      comp_bet = math.ceil(computer.cash /4)
  elif abs(first-second)>=10:
    if computer.cash/2 > pot:
      comp_bet = pot
    else:
      comp_bet = math.floor(computer.cash /2)

  print("The computer bet " + str(comp_bet))
  
  # ends round if computer bets 0, continues if they bet
  if comp_bet == 0:
    return
  else:
      
    # now we deal third card and change the balances
    third = back_up[random.randint(0, len(back_up)-1)]
    back_up.remove(third)
    print("The third card is a " + flip_card(third))

    # all scenarios with Ace as third card first
    if third == "A":
      if (first == 0 or second == 14) and not(first == 0 and second == 14):
        print("Posting on an Ace means they lost massively!")
        pot += comp_bet*4
        computer.cash -= comp_bet*4
      elif first == 0 and second == 14:
        print("Unbelievable! They got 3 Aces and lost massively!")
        pot+= comp_bet*4
        computer.cash -= comp_bet*4
      else:
        print("Ace always loses.")
        pot+= comp_bet
        computer.cash -= comp_bet
        
    # if they're all the same
    elif third == second and second == first:
      print("Wow, all three are the same! They take a huge loss!")
      pot+= comp_bet*3
      computer.cash -= comp_bet*3

    # if first two the same and third is greater
    elif second == first and third > second:
      if higher_or_lower == "H":
        print("They won!")
        pot -= comp_bet
        computer.cash += comp_bet
      if higher_or_lower == "L":
        print("They lost")
        pot += comp_bet
        computer.cash -= comp_bet
    # if first two are the same and third is lower
    elif second == first and third < second:
      if higher_or_lower == "H":
        print("They lost")
        pot += comp_bet
        computer.cash -= comp_bet
      if higher_or_lower == "L":
        print("They won!")
        pot -= comp_bet
        computer.cash += comp_bet

    # if third card equals either first or second
    elif third == second or third == first:
      print("They lost double!")
      pot += comp_bet*2
      computer.cash -= comp_bet*2

    # if the third is between first and second
    elif (third > first and third < second) or (third <first and third>second):
      print("They won!")
      pot -= comp_bet
      computer.cash += comp_bet

    # if third is less than the first and second
    elif third < first and third < second:
      print("They lost")
      pot += comp_bet
      computer.cash -= comp_bet
    elif third > first and third>second:
      print("They lost")
      pot += comp_bet
      computer.cash -= comp_bet


comp1 = Player("Computer 1", starting_amount)
comp2 = Player("Computer 2", starting_amount)

def play():
  
  print("First, let's collect the antes")
  collect_antes(comp1, comp2)

  while(user_stack>0 and (comp1.cash>0 or comp2.cash>0)):
    if pot==0:
      print("The pot's run empty, time to collect antes again")
      collect_antes(comp1, comp2)
    show_information()
    
    
    user_plays()

    
    if pot==0:
      print("The pot's run empty, time to collect antes again")
      collect_antes(comp1, comp2)
    show_information()

    if comp1.cash >= 1:
      comp_plays(comp1)

    if pot==0:
      print("The pot's run empty, time to collect antes again")
      collect_antes(comp1, comp2)

    if comp2.cash >= 1:
      comp_plays(comp2)

    if pot==0:
      print("The pot's run empty, time to collect antes again")
      collect_antes(comp1, comp2)

  show_information()
  if user_stack >0:
    print("Sorry, you lost all your money :(") 
  else:
    print("Nice job! The computers are all out of money so you get it all!!!")
  

play() 
