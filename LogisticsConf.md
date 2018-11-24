## Logistics in Mobility Conf Seesion -1 (before lunch)

* Go JEK : Automated Daily Run Sheet
    * The DRS creation is almost always manual. 
    * Source of data : customer address
        *  Structure the address : 
            * Format changes across the state.
            * Also the problem can be more complicated when 3rd party collect data
            * Make a text corpus.
            * Problems : Spelling mistakes, Combined text, Separator,  Gibberish Text, No address Information
        * Named Entity Recognition
            * Ground Truth : Dispatch Centre lat long, and find the complete address with google which is mostly formatted, comma separated address. 
            * Get a vocabulary of different classes - roads, apartment, etc
            * Create a spell checker [old address? ]
                * Develop a similarity score where you compare and replace. 
            * Preprocess the data:
                * Remove all the English stop words and the address stop words. 
            * Supervised Training Data Set
                * Create custom address tags
                * FNS FNC FNC : manual ways in which addresses are written. 
                * Training the data around ~8.5 K address. 
            * Model Building
                * Maximum Entropy Model
                    * Model will predict tag for a given token
                    * Feature set to be generated maxent based on business case [ eg: when the 3rd word is Apartment then the tag is BNC]
                    * These features goes to MaxEnt ~98% tags of the words
                * Geo Coding
                    * Get a tags for all the addresses
                    * From a priority of the address tags, not all are important
                    * Definite LMI >>> Importance of non definitive LMI
                    * Final accuracy should be sensible ~200m 
        * Cluster
            * Modified K-Means cluster. 
            * Business decisions:
                * One cluster cannot be 35 and other 85, the k can be defined beforehand. 
    * Questions: 
        * Google needs a structured address, if it cannot be identified by google then it just returns the lat long of the recognised centroid. 
        * Taking the feedback and feeding it into the systems
        * Why not a vehicle routing problem over a cluster? FE generally knows the area. 
        * Clustering need to modified for the time slots: sub cluster
 ************************
* Flipkart: [Product] Location Intelligence and Automated Beat Planner. 
    * FSG kicks in once the customer has placed an order and aims to be the best in class of the services. 
    * Order Placed
        * Create in shipments
        * Fulfilment center
        * Sortation center
        * Delivery hub
        * customer
    * Address problem 
        * Near Dharmaram Bus Station, Bus station, Gujarat is a address
        * Address is some other pin code than the actual address itself
        * Asking some one: is mentioned in the address. 
    * Scale of address
        * Non standardised address attributes: Centers, Nagar, Galli, etc.
        * Address are poorly organised. Sector 42 may not be next to sector 43
        * User himself does not understand the address
        * Problem is exaggerated in tier 2/tier 3 cities
    * Effect
        * Inefficient manual planning: requires the local knowledge
        * Unoptimised shipment flow: pin code wrong can have lot of effects
        * Customer discovery: calling multiple times. 
    * First Level of Solution
        * Some standardisation is needed in the address
        * One way is tags
        * FLIP [Flipkart Location Intelligence Platform]
            * Crowd sourced. 
                * Own Database
                * Map my India 
            * I/P : Address text 
            * Tokenise a address
            * Dwarka, Sector 14, Sheeed Bahgat Singh Apartmanet
            * Generate a polygon for each of the area token
            * Score: area intersection with all the other tokens
            * Highest scores, diagonal is the prediction precision. 
            * Lat/Long and precision are the only attributes. 
    * Automated Beat Planner
        * I/P : order size and type, geo codes, slot time, capacity [ range rather than a absolute ] , traffic
        * O/P : Slot Wise Route Plan, Beat Plan UI, Manual Override for the Planner, ETA for delivery, Out of delivery area indicator. 
        * Out of delivery area : feedback is looped into the I/P
        * Modules: Geo-Location, Geo-Distance, Maps Interface, Traffic Prediction 
    * Aim : Perfect Match of supply and demand
        * Each order should be addressed to a correct delivery channel
        * One end is customer and other is the delivery executive. 
    * Customer Availability Service: 
        * Prediction for the time of delivery. 
        * Office delivery address
    * Allocation Engine in the automated beat planner should have input of the FE performance (fake attempt), skill (any demo required?) and time preference  
************************
* Pikkol : Visualisation and Fleet Managmenet
    * Ground up problem:  visualise the data
    * Preattentive attributes: Collin Ware
    * Design : color scales, numerical scales, interaction bounderies
    * Can’t reduce cost without volume and can’t increase volume without cutting the price
    * Unpredictable demand and supply
    * Dataset: Places and Loads
    * Detailing
        * See all the loads in a channel
        * All the loads originating from a particular port on a particular date
            * Lat/Long - position
            * Shape - Ports:  circle
            * Color : Aggregation 
        * D3js and dialogFlow
    * Optimisation algorithm 
* PEDL : Revenue maximisation 
    * Aim : for short distance rides
    * Basket is solar panel for the IoT devices
    * Vandalism: Inside a lock a buzzer 
    * How many cycles at a station: Low ticket item a ride is around 3 rupee
    * Optimise the number of trips per cycle
        * Optimise the current network of station within an area
            * Cycle rebalancing
            * Identify frequented routes
            * Identify dead station
            * Identify areas where people abandon cycle
            * Subscription package
        * Expanding the new areas with high demand
            * Empty search areas
            * Identifying the connecting neigbourhood
        * Number of cycle that should be present at the start of the day
        * Rates of Trips from a station [ROT] : number of expected of trips per days from a station, given a cycle availability
        * Assumption: Impulsive business : you see a cycle and you ride it. 
        * Network Chain: Understanding the transition probabilities,  gives cycle at the end of the day. 
        * Cycle init>= 0 cycle end >= 0 sum of cycles == total no of cycle : removes the dead states
        * Kepler.gl, Folium, Mapbox and deck
        * Build maps to highlight actions and not just plotting the data. 
************************
* BoF : Zoomcar, Flipkart, Swiggy and Pikkol [Chatham House]
    * Accuracy precision differs : in search your accuracy may not be same as the assignment accuracy. 
    * Places API : Things are well mapped
    * Elevation may be relevant in the some cases, metadata matters. 
    *  OSM and leaflet for visualisation, how frequent the satellite imagery is updated
    * How to layer on different kind of information 
    * State of the map: keeps changing, the institution and the governing body. 
    * Data integration related to the other funnels. 
    * Cache the google api results. 
    * Cross verify the results [google api and OSM]
    * Google maps overlays traffic data : OSRM hence if you want traffic data. 
    * Data providers : Google Maps, OSM, MapMyIndia
        * Google : price jump is very pinching
        * OSM data being very patchy, authenticity and vandalism, 
            * distance is not accurate, offset is also not constant with google.
        * Map box : India data is not their focus. 
        * Mapmyindia: data is good, API not properly designed. 
    * Estimate time offset should be adjusted based on the vehicle size. Trucks movement ETA are almost 
double that google mentions. 
    * Using your own map powered by previous google and own dataset
        * Authenticity of the data is more prominent problem
        * Use cases which are specific to the business case may be useful  
    * Route assignment is better after delivery is defined. 
    * Heivenstien distance for defining delivery. 
    * Accurate routes or travelling distances. 
* Director of Products, Flipkart, Supply Chains and network intelligence 
    *  Network is the composition of the all parts starting from the supplier to the customer .
    * Fast scaling vs intelligence
        * Incoming demand is pushed to a warehouse
        * Need to be sorted in 20k pinched, based on the type of product, furniture wrt to fragile will be different
        * Dynamic routing (LTL) 
        * Implication : unhappy customer. Last mile is the most angry customer base hence becomes prominent. 
    * What is the fulfilment model to be operated?
    * How should the inventory should be reserved? What place when order is placed?
    * When the inventory should be released?
    * Should orders be real time or batched?
    * What should be shipment flow path?
    * Customer expectation management
    * Flexibility offered to the customer at a point in the order journey
    * Workflow -> get the right data -> awareness should be propagated in the network -> employee as control over the intelligence 
    * Ideally, this should result in orderly and predictability 
    * Every activity is modelled as the lead time and the throughput
    * What kind of services should be offered to what customer 
    * Real time engine which publishes the events and insights which happens
    * Demand prediction 
        * Give preference to loyal customer? (!! This would limit your customer base !!)
    * Fulfilment decision cockpit
    * Primarily, defining a constraint aware planning system
        * That creates a profitable distribution decisions with viability into network wide inventory & capacity. 
            * Incoming demand
            * Batch orders before pushing to the warehouse
            * Planned picking based on the batch 
            * Sort for a plan : transportation plan is known before hand. 
            * Planned routing (FTL) instead of LTL
    * Which warehouse to select given a order?
        * No point in time decisions - consider future orders
        * List warehouse with inventory
        * Identify the flow path choices; cost vs SLA trade off
        * Consider an iPhone X vs a t shirt delivery. 
        * Assess risks: SLA vs reliability 
        * Inventory allocation (pre/now/later)
    * How to batch the orders
        * Determine the flow path
        * Tranport connection balancing 
        * Transport connection - grouping
        * Backword propagation - Zero queues: latest time to release the order
        * Forward propagation - earliest time to release the. order & minimise the risks
    * Guidelines 
        * Model everything into a common unit: business values
        * Model time into opportunity cost 
        * Model risk as reliability coefficient 
        * Objective function : max value of the batch of the orders
        * Parameters: 
            * Max cost of the serving the order : earliest order
            * Min cost of the serving the order : delay the order
            * Cost of risks of the flow path
