# MIST 4610 Group Project 1 - Spring 2025
SQL Sports Betting group project from MIST 4610 with Dr. Akshat Lakhiwal

## Team Name: 
21484 Group 8

## Team Members:

1) Tobey Barden 
2) Daniel Pritchard
3) Ian
4) Austin
5) Owen Herring

## Problem Description:
We are creating a relational database for a sports betting application that allows users to place bets on both teams and individual players at various sporting events, track odds and promotions for those bets, and process the user transactions correctly. The database stores and retrieves data for users, promotions, account balances, bets, transactions, payments, sports, sporting events, teams, and players.

The database will be used to accomplish many different tasks in the application. These tasks include user management, bet placement and tracking, financial transactions that occur from withdrawals, deposits, and payouts, as well as reporting various sporting events and betting markets that are ongoing so that the user has access to place many different types of bets.

Creating queries in the database will allow efficient management of all these different tasks, and ensure that the sports betting application operates smoothly and is easy for the user to use. 


## Data Model
There are 11 entities needed for our database. These entities include Users, Promotions, Users_Have_Promotions, Balance, Bets, Transactions, Payments, Teams, Player, Sporting Events, and Sports.

We begin with Users, which has a relationship with many other entities since Users are the ones who perform all of the actions on the sports betting app. It contains a one-to-one relationship with Balance, as each User will only have one account balance that tracks how much money is going in and out of their account. The Balance has a one-to-many relationship with both Transactions and Payments, as they are both used to report changes that occur within a user's account. Each user's account will record many different financial transactions and payments that happen on the app. Transactions records the money that is spent and received every time a user places a bet, while Payments records money that the user adds and removes to their account balance from outside of the app. However, the relationship between Balance, and Transactions and Payments is non-identifying as Balance is not reliant on these entities to exist since a user might choose to make an account yet not change their balance at all.

Additionally, Users has a one-to-many relationship with Bets, as each user can place many different types of bets. Additionally, Users has a many-to-many relationship with Promotions, as many users can redeem many different types of promotions, while many promotions can be applied to many different users. Because it is a many-to-many relationship, we have created an associative entity titled Users_has_Promotions, which has the primary keys from Users and Promotions as foreign keys.

Bets is another very important entity because this is where a majority of the actions on the app will take place. It has a one-to-many relationship with Transactions since it records all of the money put into and paid out of an individual bet. 

Sporting Events lists all of the events that users can place bets on. It has a one-to-many relationship with both Promotions and Bets since every Sporting Event will have many Promotions that can be used on it and bets that can be placed on it. Sports has a one-to-many relationship with Sporting Events due to one sport having many different events it can be performed. Sports additionally has a one-to-many relationship with Teams as one sport will have many different teams. Teams also has a one-to-many relationship with Player, as one team will have many different players as well.
![Screenshot 2025-03-19 at 13 44 11](https://github.com/user-attachments/assets/80501dff-7c60-4de9-8783-4ff25d652716)


## Data Dictionary
![Data_Dictionary_All_Pages](https://github.com/user-attachments/assets/68a5a6f0-19a1-4c3d-98d0-fcbcf3f358a6)

## Queries



Query 9



Query 10

<img width="651" alt="Screenshot 2025-03-20 at 15 52 40" src="https://github.com/user-attachments/assets/39944f87-127f-4ba8-a945-79991339250d" />



