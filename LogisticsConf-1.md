## Logistics in Mobility Conf Seesion - 2  

* **Swiggy : Order Batch prediction** :
  * If it can be batched with the number of orders in the system you batch and a predict SLA
  * If it can’t be batched with the current orders then send it to first order batching
  * First Order Batching prediction 
      * Depends upon demand prediction 
          * Order at the same restaurant
          * Customer geohash future orders
          * Customer geohash and the restaurant
      * Also depends upon how far the two clustered customer are 
      * Order preparation time;
      *  order SLA; give a degraded SLA
      * Item level constraint : ice cream can’t be batched. 
      * Number of data points : 11 million
      * Precision: 90% 
  * Random forest, boosting algorithm 
    ****
    
* **BoF : Shuttl, Bigbasket and Zoomcar [Chatham House]**
    * Shuttl 60K rides daily
    * Bbinstant machine placed in the apartment 
    * Slotted delivery model: 
        * prediction model
        * Roaster defined. 
        * Take less orders in case of any real time events.
    * express delivery model
    * Optimisation : 
        * Quantity 
        * Quality 
        * time
    * Driver information may not be shared
    * In that case the eta has to be very accurate.
    * Problems
        * When GPS doesn’t work
        * When GPS is not accurate: 
            * 20 min distance can be the other side of the road 
            * Might affect the ETA includes a U-Turn
            * Change your GPS to your nearest known location.
        * When buses actually move on a road which google doesn’t consider them bus routes
        * Vandalism should be taken into account.
        * Crime should be taken into account
        * Fraud by the customer should be taken into account
        * Pushing the product is not a target when your fill rate is high
        * Bouncer and fraud detection model for stealing food orders
        * Replace the delivered item with a expired item.
        * Chicken maggi to jain family 
        
      ****
* **Vahan: Last Mile Workforce**

    * Automating and scaling high volume workforce for e-commerce 
    *  Flipkart had additional 60K delivery boys for Diwali sales.
    * Design consideration
        * Reduce the manual effort by automation
        * One stop shop
        * Must work at scale
        * Account for high churn rate and attrition 
        * Not a daily used application
    * Automating job seeker engagement on the existing messaging platforms
        * WhatsApp is 97% adopted
    * automate
        * Job pitch
        * Gauge user interest
        * Basic screening
        * Schedule walk in
    * Solutions
        * IVR: limited input capability
        * Voice based: data connectivity can be a throttle
        * Chat based seems to works
    * Avoid hopping across channels
        * Lead generation: classified, naukri, quick, etc
        * processing : excel sheets
        * Engagement: tele calling
        * Screening: on site
    * Goal Oriented Dialog System
        * User text input
        * Text normalisation [yes, yessss, ya, you] by Machine Translation
        * Intent Classification
        * Response lookup
    * User base may mix multiple language: "call maddi"
    * Regional and cultural influences also affect the way people type
    * Train good ML models to handle this
    * Own data collection : 
        * Jokes and daily quotes
            * Too much spam
        * Translation bot 
            * English API from the google translate
            * Sporadic usage
        * English Learning Bot
            * Narrow Content
        * Friend Finder Bot
            * Anonymus messages collections
    * Hii I have bike and mere pas bike hit 
        * Both hii should be text normalised differently
    * WER : Neural machine translation 2.7%
    * Code mixed data set
    * Personalisation for the regional 
* ShadowFax: Product development for fleet management
    * Last mile delivery 
    * Rider Persona
        * Finding exact location
        * Customer not picking up calls
        * Payment discrepancies
        * Route and order allocation favours
        * Held hostage unless PayTm returns money
        * Going to far off location for delivery
        * Insufficient orders to fulfil
        * ~12 to 15K vs ~8k to 20K
    * Engineering Challenges
        * Patchy network : marking delivered is going to be a problem, customer doorstep, restaurant areas
        * Battery drain     : delivery boy being on the platform is the 
        * Location impacts earning
        * Location impacts customer experience
    * MQTT protocol 
        * Battery draining in a opening vs a intermittent http protocol 
        * Start with a mqtt protocol on a pub sub with http protocol as a backup
    * Look for a strategy to polling a location. 
        * When a partner is idle you don’t need at all times
        * When the partner is out for delivery you need a real time tracking. 
        * The hardware in the location sensors depends on the device 
        * ^^^ this might be overriding the location demanded by android
    * Routing Engine and ETA prediction
        * Google Distance Matrix API 
            * Response Time - 100 ms -150 ms
            * Expensive ~ $3000/month
        * Naive methods: 
            * Haversine method between the coordinates
            *  
        * OSRM : 
            * An open source routing engine which computes the shorter path between points in a given map
            * Feed in the open street map data on OSRM
            * Response Time :  5- 10 ms
            * t2.medium  was ec2 ~ $40
            * A* algorithm 
            * No traffic data  : weightage to each edges. 
        * Location Familiarity 
        * In-app training 
            * Effective training is a must 
            * Customer experience
            * Brand loyalty 
            * Best practises. 
            * Video content is better, surprise pay, vernacular content is better
        * Fraud Detection
            * Build that and predict early
            * Bad apples should have no tolerance policy
            * Strong focus on KYC: 
                * Image processing
            * Location Intelligence 
                * Location stream and task stream can replicate the ground scenario
                * Kepler.gl data exploration tool: client only data application; data stores in browser: which metric to chase
                * deck.gl
****
* **Locus.sh : Sales fleet Optimisation.**: 
    * Sales beat
        * Whom to visit
        * When to visit
        * Whom to send
        * Minimize the cost ( transportation cost) 
        * Cost of the missed sale is very high
        * Wholesale store visit time vs retail store visit time
        * Limited resource for buy
    * Set of outlets need to be visited; 
    * different salesmen for different product; 
    * and finite time for the salesmen
        * Assignment of sales person
        * Route assignment
        * Scheduling problem
        * Salesmen fatigue : should visit higher revenue store before fatigue sets in
        *  Salesperson feature set
            * Product familiarity
            * Outlet familiarity 
            * experience
            * Region familiarity
    * Same store is listed multiple time a day: PROBLEM from heuristics
    * Problem Classification 
        * Periodic 
        * CVRP
        * multi-trips
        * Multi-days
        * clustering : outlets being visited on the same day
        * Multi-product: 
        * Heterogeneous fleet
    * Solution approach
        * Routing + Bin Packing
        * Integer Program - Heuristic Hybrid
        * Scheduling problem
        * Single MIP 
        
        ****
