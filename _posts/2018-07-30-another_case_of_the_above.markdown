---
layout: post
title:      "Another case of the above"
date:       2018-07-30 19:22:12 +0000
permalink:  another_case_of_the_above
---


I've arrived at my rails project at last. This one was a ton of fun because using rails I was able to create the framework of my Magic Manager Pro project in a more logical flow. I very much enjoyed this project and the challenges I faced to accomplish it although most of my challenges were posed by me rather than the project requirements. 

I wanted to create this in such a way that the user had the best experience possible and so that they could get all of the information that they needed to to form their decks and play the game. The most complicated part of this was figuring out how to create a database of magic cards so that the user was creating their decks out of real magic cards rather then having the user create a card on their own. With some help and alot of time and research I managed to scrape all of the details I could ever want (and more) from an API that some other people who play the game created. This gives my users the ability to choose a card and view all of the information about the cards so that they can create a deck that is useable in a real format of the game. 

The next big challenge I had was figuring out a way to join a user-card (join model) with a deck to create a deck-card (join model) and figure out how to allow a user to create a full deck of these deck cards. Again, with a little help this was finally accomplished using nested forms to handle the creation of Deck_cards under the new deck view. 

The application is finally complete with the abilities to: 

* Create new users
* Log in with existing users
* Log in with Facebook
* Create new user cards using the scraped Magic Cards
* Add details about your personal cards
* Edit details about your personal cards
* Delete your personal cards
* View pertinent details about the card
* Create/Edit/View fomat specific decks
* Add cards to your decks, view those cards

This was a long and involved project but I am proud of the result as it is comprehensive and works well.
