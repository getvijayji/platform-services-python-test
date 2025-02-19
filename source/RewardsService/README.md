# Objective
Create RESTful endpoint(s) to calculate, store, and retrieve customer rewards data from MongoDB.

# Background
* You will be using the [Tornado](http://www.tornadoweb.org) Python web framework and a MongoDB docker image.
* When starting up the 'rewardsservice' docker container in the [Setup](#setup) below, a mongo 'Rewards' database will be created for you with a "rewards" collection containing each reward a user can earn and how many points are needed to reach each reward.
    ```
    [
        { "tier": "A", "rewardName": "5% off purchase", "points": 100 },
        { "tier": "B", "rewardName": "10% off purchase", "points": 200 },
        { "tier": "C", "rewardName": "15% off purchase", "points": 300 },
        { "tier": "D", "rewardName": "20% off purchase", "points": 400 },
        { "tier": "E", "rewardName": "25% off purchase", "points": 500 },
        { "tier": "F", "rewardName": "30% off purchase", "points": 600 },
        { "tier": "G", "rewardName": "35% off purchase", "points": 700 },
        { "tier": "H", "rewardName": "40% off purchase", "points": 800 },
        { "tier": "I", "rewardName": "45% off purchase", "points": 900 },
        { "tier": "J", "rewardName": "50% off purchase", "points": 1000 }
    ]
    ```

# Instructions:
* Design and implement the following endpoints.
    * **Endpoint 1:**
        * Accept a customer's order data: **email adress**  (ex. "customer01@gmail.com") and **order total** (ex. 100.80).
        * Calculate and store the following customer rewards data into MongoDB. For each dollar a customer spends, the customer will earn 1 reward point. For example, an order of $100.80 earns 100 points. Once a customer has reached the top rewards tier, there are no more rewards the customer can earn.
            * **Email Address:** the customer's email address (ex. "customer01@gmail.com")
            * **Reward Points:** the customer's rewards points (ex. 100)
            * **Reward Tier:** the rewards tier the customer has reached (ex. "A")
            * **Reward Tier Name:** the name of the rewards tier (ex. "5% off purchase")
            * **Next Reward Tier:** the next rewards tier the customer can reach (ex. "B")
            * **Next Reward Tier Name:** the name of next rewards tier (ex. "10% off purchase")
            * **Next Reward Tier Progress:** the percentage the customer is away from reaching the next rewards tier (ex. 0.5)
    * **Endpoint 2:** Accept a customer's email address, and return the customer's rewards data that was stored in Endpoint 1.
    * **Endpoint 3:** Return the same rewards data as Endpoint 2 but for all customers.
* For bonus points, add error handling and unit tests.

# Setup
* Install docker and docker-compose dependencies.
* $ cd APP_PATH/platform-services-python-test/source/RewardsService
* $ docker-compose build
* $ docker-compose up -d
* Services are accessible at http://localhost:7050/

# Solution Details
# -----------------
# Endpoint 1
* POST http://localhost:7050/customerrewards
* request body - {"email": "customer01@gmail.com","orderTotal":445.8}
# Endpoint 2
* GET http://localhost:7050/customerrewards?email=jdoe1@example.com
# Endpoint 3
* GET http://localhost:7050/customerrewards

# For Error handling
* Created used Try/catch and created a util class ErrorThrow 
* which can be extended for custom exception management.

# For Unit Testing
* Created TestrewardsService class

# Approach taken
# --------------
# Creation of base class (new)
* **base.py, consisting a BaseHandler class which is created to pull some common behaviours together which 
* can be reused across the application as practice.

# Creation of utility classes for error handling and other utilities
* to reduce the redundancy and inprovig the re-usability of the methods which are most common in different 
* functions
* **error_thow.py : Custom Exceptions behaviour
* **jsonencoder.py : to encode json having objectId

# Added Handler Class for new end points
* **customer_rewards_handler.py : This handled all the requests related to customer rewards points.
*    **** If customer record is new then based on the order value we will assigned the rewards
*    **** If the customer exists we will update the old reward values with new one which ll be and addition to old
*   **** After customer reach to max reward point no more earning ll happen.


