# MIST 4610 Group Project 1 - Spring 2025
SQL Sports Betting group project from MIST 4610 with Dr. Akshat Lakhiwal

## Team Name: 
21484 Group 8

## Team Members:

1) Tobey Barden @TobeyGarden
2) Daniel Pritchard @dcpritch
3) Ian Arnold @ian-uga
4) Austin Zeiller @Austinz7303
5) Owen Herring @Oherring22

## Problem Description:
We are creating a relational database for a sports betting application that allows users to place bets on both teams and individual players at various sporting events, track odds and promotions for those bets, and process the user transactions correctly. The database stores and retrieves data for users, promotions, account balances, bets, transactions, payments, sports, sporting events, teams, and players.

The database will be used to accomplish many different tasks in the application. These tasks include user management, bet placement and tracking, financial transactions that occur from withdrawals, deposits, and payouts, as well as reporting various sporting events and betting markets that are ongoing so that the user has access to place many different types of bets.

Creating queries in the database will allow efficient management of all these different tasks, and ensure that the sports betting application operates smoothly and is easy for the user to use. 


## Data Model
There are 11 entities needed for our database. These entities include Users, Promotions, Users_Have_Promotions, Balance, Bets, Transactions, Payments, Teams, Player, Sporting Events, and Sports.

We begin with Users, which has a relationship with many other entities since Users are the ones who perform all of the actions on the sports betting app. It contains a one-to-one relationship with Balance, as each User will only have one account balance that tracks how much money is going in and out of their account. The Balance has a one-to-many relationship with both Transactions and Payments, as they are both used to report changes that occur within a user's account. Each user's account will record many different financial transactions and payments that happen on the app. Transactions records the money that is spent and received every time a user places a bet, while Payments records money that the user adds and removes to their account balance from outside of the app. However, the relationship between Balance, and Transactions and Payments is non-identifying as Balance is not reliant on these entities to exist since a user might choose to make an account yet not change their balance at all.

Additionally, Users has a one-to-many relationship with Bets, as each user can place many different types of bets. Additionally, Users has a many-to-many relationship with Promotions, as many users can redeem many different types of promotions, while many promotions can be applied to many different users. Because it is a many-to-many relationship, we have created an associative entity titled Redeem, which has the primary keys from Users and Promotions as foreign keys.

Bets is another very important entity because this is where a majority of the actions on the app will take place. It has a one-to-many relationship with Transactions since it records all of the money put into and paid out of an individual bet. 

Events lists all of the events that users can place bets on. It has a one-to-many relationship with both Promotions and Bets since every event will have many Promotions that can be used on it and bets that can be placed on it. Sports has a one-to-many relationship with Events due to one sport having many different events it can be performed. Sports additionally has a one-to-many relationship with Teams as one sport will have many different teams. Teams also has a one-to-many relationship with Player, as one team will have many different players as well.
![Screenshot 2025-03-19 at 13 44 11](https://github.com/user-attachments/assets/80501dff-7c60-4de9-8783-4ff25d652716)


## Data Dictionary
![Data_dictionary_combined](https://github.com/user-attachments/assets/bfb32ee3-b4bd-4ede-937a-518ed1a8747b)


## Queries
![q1](https://github.com/user-attachments/assets/0f85fada-79b0-43f7-b8af-4a9369260ec3)


<img width="651" alt="Screenshot 2025-03-20 at 16 19 10" src="https://github.com/user-attachments/assets/cfac2e3c-4851-47fc-8eb1-aa3ae075ccd9" />





-- Query 2
Query 2 allows the managers to calculate the total amount of bets that have been placed on the app across all users. This allows the managers to track the total activity that is happening on the app, as if there are a lot of total bets being placed that means the app is running successfully and is being used a lot, which means there is a lot of activity on the app and large changes are not needed to ensure the app gains users or more activity.

SELECT COUNT(betID) AS total_bets FROM Bets;

<img width="506" alt="Screenshot 2025-03-20 at 16 21 45" src="https://github.com/user-attachments/assets/a76c96a7-ebda-4059-b990-b51d4a878b67" />





![q3](https://github.com/user-attachments/assets/a75aa08f-6c87-401c-aa26-0389494527e4)

<img width="518" alt="Screenshot 2025-03-20 at 16 22 13" src="https://github.com/user-attachments/assets/41ec4200-1e47-48e4-b190-ee14d554ca30" />



![q4](https://github.com/user-attachments/assets/ffde147f-93d8-41e4-982f-eaeba68558b2)

<img width="651" alt="Screenshot 2025-03-20 at 16 16 43" src="https://github.com/user-attachments/assets/8edb05d0-1443-41e0-a6bb-58aaddbe0adc" />



-- Query 5
Query 5 retrieves the user ID, username, and total amount of bets they have placed in dollar amounts from the Users and Bets entities. It uses the sum function to find the total dollar amount in bets that each user has placed before using the group by function to display the data for each user effectively. It then orders the data by the total bet amount in descending order.


<img width="691" alt="Screenshot 2025-03-20 at 16 31 31" src="https://github.com/user-attachments/assets/8ee36020-7e5f-47b9-a69c-ab8a0fdb8554" />


Query 5 is a great way for managers to see the betting activity and style of each individual user. All users on a betting app have different risk tolerance and betting styles from one another. This means that while one user may place significantly more bets than another, they may have placed a significantly lower dollar amount in total bets. It is very important to be ankle to see the dollar amount in bets of each user in addition to the number of bets they have placed so the manager can see what users place significant money into the site and therefore deserve more rewards and promotions to keep them coming back for more.



-- Query 6 


<img width="767" alt="Screenshot 2025-03-20 at 16 30 17" src="https://github.com/user-attachments/assets/2623dc63-055b-49c1-8025-a79f27b51114" />




-- Query 7 
This query enables the operators to identify how many bets have won, lost, and drawn, and how much money has been lost or won due to the results of those bets. This helps the managers keep track of how much money is going in and out of the app due to the results of the bets, and why that money is being moved. Any money from a lose will be paid out back to the app, any money from a draw will be returned to the user, and any money from a win will be returned to the user along with the payout they receive from winning the bet.

<img width="653" alt="Screenshot 2025-03-20 at 16 27 06" src="https://github.com/user-attachments/assets/c388983f-5fd2-4c54-a5c9-439aa9c698b1" />

![q8](https://github.com/user-attachments/assets/a0acac70-dc8e-402d-95ff-aa28ef36530d)




<img width="704" alt="Screenshot 2025-03-20 at 16 25 37" src="https://github.com/user-attachments/assets/993b8c78-5d2c-48fc-8021-b3f58a3b4d55" />




![q9](https://github.com/user-attachments/assets/73e0ad82-4d38-468b-9054-507a5fdcba16)





-- Query 10 

<img width="651" alt="Screenshot 2025-03-20 at 15 52 40" src="https://github.com/user-attachments/assets/39944f87-127f-4ba8-a945-79991339250d" />



