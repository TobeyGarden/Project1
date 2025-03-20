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
Query 1 retrieves the username and email of any user on the database who has placed a bet at any time. It uses the ‘Exists’ function to see if the user has any rows in the ‘Bets’ entity before retrieving the selected information from the ‘Users’ entity.

SELECT userName, userEmail
FROM Users
WHERE EXISTS (SELECT* FROM Bets WHERE Users.userID=Bets.Users_userID);

![Screenshot 2025-03-20 at 12 56 32](https://github.com/user-attachments/assets/40b9155b-8e49-4dbd-b3ee-6f02eb480c9c)

Query 1 is important for managers because it allows them to see what users have actually placed bets within the site. People often make accounts on sports betting websites but never actually end up placing any bets. Since the website profits are dependent on users making bets it is very useful information to see which users are actually contributing and send them promotions or rewards to their email. 

Query 2 retrieves the sum of payment amounts and lists it as current deposits, the sum of transaction amounts to see the total profit from betting, and the sum of each to see the current balance of each user on the platform. 

SELECT acctID, SUM(paymentAmount) AS ‘Current Deposits’, SUM(transactionAmount) ‘Betting Profit/Loss’, SUM(SUM(paymentAmount) AND SUM(transactionAmount)) AS ‘Current Balance’
FROM Payments
JOIN Balance ON Payments.acctID=Balance.acctID
JOIN Transactions ON Transactions.acctID=Balance.acctID
GROUP BY acctID;

Query 2 is important for managers because it shows the financial position and activity of the users on the site. Since the cash inflow and outflows that happen within the site are separated from the deposits and withdrawals connected beyond the site, managers have the ability to see separate the money associated with the wins and losses from betting from the withdrawals and deposits from the users balance while still being able to add them up to find the current balance for each individual user. 

Query 3 retrieves the name, sport, and count of bets placed for each individual event from the events entity. It joins the event and sports entities with events serving as the parent and sports serving as the child to retrieve both the amount of bets placed and the name of the event. It then orders the events in order of the number of bets placed descending. 

SELECT eventName, sportName, COUNT(betID) AS ‘Number of Bets Placed’
FROM Events
JOIN Sports ON Sports.sportID=Events.sportID
JOIN Bets ON Bets.eventID=Events.eventID
ORDER BY COUNT(betID) DESC;

Query 3 is a great way to see the demand for specific events within the site. It shows how many bets were placed by users for a specific event while also telling you what sport that event is in. By also ordering the results by the number of bets in descending order, it makes it much easier for managers to see where the most activity resides within the site. This is extremely valuable information because it can allow the site to focus more on creating events and promotions catered to the type that users are more inclined to place bets on.

Query 4 retrieves the username, type of bet, odds on the bet, amount placed, and the result of the bet from the bets entity within the database. It joins the user and bets entity with users serving as the parent and bets as the child. The query retrieves the data on bets where the amount placed exceeds 200 dollars and orders the results from largest to smallest.

SELECT userName, betType, betAmount, betOdds, betResults
FROM Bets
JOIN Users ON Bets.userID=Users.userID
WHERE betAmount > 200
ORDER BY betAmount DESC;

<img width="509" alt="Screenshot 2025-03-20 at 13 31 44" src="https://github.com/user-attachments/assets/20471f6e-41e5-4d7f-ba5a-c698a65d4740" />

Query 4 is important for managers to see the risky activity within the site. Many users will join to place small bets every now and then with little risk to the company or themselves; however, there are serious betters who often place much larger bets in the hopes of achieving serious payouts. This query allows managers to filter out the smaller bets and be able to see the activity within the much riskier and important side of the site which could have major effects on the success of the company. 

Query 5 retrieves the name of the promotion, the sport involved, the number of users who participated, and the total value of the redeemed promotions from the database. The Redeems, Promotions, Events, and Sports entities were all joined to retrieve the relevant information. The query also only retrieves the promotion where there are at least 1 participant before grouping them by promotion name and sport.

SELECT promotionName, sportName, COUNT(userID) AS ‘Number of Redeems’, SUM(promotionValue) AS ‘Total Value Redeemed’
FROM Promotions
JOIN Redeems ON Promotions.promotionID=Redeems.promotionID
JOIN Events ON Events.eventID=Promotions.eventID
JOIN Sports ON Sports.sportID=Events.sportID
WHERE COUNT(userID) > 0
GROUP BY propmotionNAME, sportName;

Query 5 is very important for managers interested in seeing promotion activity. This query allows for the manager to see what promotions users are more interested in as a whole which is important for attracting site activity and the creation of future effective promotions. The functions also groups the data effectively so each individual promotion can be examined individually.

