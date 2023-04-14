We have a business idea to create a web based service which could show train real time schedules within 12 hours and number of vacant seats in each class (sleeper, AC - for simplicity consider only these two classes) until 30 minutes before departure time. Just in case if the train is late, new departure time could be considered. 

We would like to offer below services to our customers:
a. check realtime train schedules and available tickets in each category
b. train schedules and ticket availabilities shall be always shown in 12 hours window size
    i. Order of display should be based on price(lower price means higher rank), number of available tickets(more available ticets means higher rank) and departure time(earlier departure time means higher rank)
    ii. In case if the train is late, new departure time should be considered
    iii. Price could be changed based on demand, available tickets and departure time, so always new price should be considered for the order of display
c. last minute ticket booking facilities on some discounts i.e. we would like to offer Indian Railway last minutes ticket sell. [This requirement we would not do for now]

Indian Railway has agreed to this business idea and given us 4 paid APIs (paid APIs means, Indian Railway would impose usage charges of these APIs on us everytime we make a request) --

```
1. POST: /register
   Response Body:
   {
      "companyName": "something"
      // other parameters are omitted for simplicity
   }

   Response Expected:
   Status Code: 201
   {
       "ClientID": "UUID",
       "ClientSecret": "tough password"
   }

   This API is used to register a company who wish to use this paid service. Normally its a multi-steps process but 
   for simplicity consider success response means payment done and all necessary fields are supplied.

   2. GET: /trains?window-size=12
   This is a protected route and would require auth token in the header issued by Indian Railway. Auth token could be 
   acquired by 4th API
   
   Expected Response:
   Status Code: 200

   [
    {
     "trainName": "somthing exp",
     "trainNumber": "Fake321",
     "departureTime": "10:20 a.m.",
     "seatAvailable": {
        "sleeper": 5,
        "AC": 2
     },
     "price": {
        "sleeper": 432,
        "AC": 1232
     }
   }
   ]

  3. GET /trains/{trainNumber}
  This is a protected route and would require auth token in the header issued by Indian Railway. Auth token could be acquired by 4th API

   Expected Response:
   Status Code: 200
    {
     "trainName": "somthing exp",
     "trainNumber": "Fake321",
     "departureTime": "10:20 a.m.",
     "seatAvailable": {
        "sleeper": 5,
        "AC": 2
     },
     "price": {
        "sleeper": 432,
        "AC": 1232
     }
   }

   4. POST: /auth
    Request Body:
      {
        "ClientID": "UUID",
        "ClientSecret": "tough password"
      }
    
    Expected Response:
    Status Code: 201
    {

    }
```
