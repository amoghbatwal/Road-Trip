# CSCI-B 551 Elements of Artficial Intelligence

### Road-Trip

### Problem Statement
Besides baseball, McDonald’s, and reality TV, few things are as canonically American as hopping in the car for an old-fashioned road trip. We’ve prepared a dataset of major highway segments of the United States (and parts of southern Canada and northern Mexico), including highway names, distances, and speed limits; you can visualize this as a graph with nodes as towns and highway segments as edges. We’ve also prepared a dataset of cities and towns with corresponding latitude-longitude positions. These ﬁles should be in the GitHub repo you cloned in step 0. Your job is to implement algorithms that ﬁnd good driving directions between pairs of cities given by the user. Your program should be run on the command line like this:
./route.py [start-city] [end-city] [cost-function]
where:
• start-city and end-city are the cities we need a route between. 
• cost-function is one of: 
– segments tries to ﬁnd a route with the fewest number of “turns” (i.e. edges of the graph) 
– distance tries to ﬁnd a route with the shortest total distance 
– time tries to ﬁnd the fastest route, for a car that always travels at the speed limit 
– mpg tries to ﬁnd the most economical route, for a car that always travels at the speed limit and whose mileage per gallon (MPG) is a function of its velocity (in miles per hour)

The output of your program should be a nicely-formatted, human-readable list of directions, including travel times, distances, intermediate cities, and highway names, similar to what Google Maps or another site might produce. In addition, the last line of output should have the following machine-readable output about the route your code found:
[total-segments] [total-miles] [total-hours] [total-gas-gallons] [start-city] [city-1] [city-2] ... [end-city]

### Implementation
We have implemented A* algorithm with heuristic. In this the heuristic adapts to the input given by the user and changes its value depending on user selected feature of importance which are 'segments', 'time', 'distance' and 'mpg'. 
Heuristic calculates following 
  1. haversine distance between city to be explored and goal city
  2. difference of angle between current city and goal city and city to be explored and goal city  
  3. base heuristic i.e one from segments, distance, time and mpg

The final cost of heuristic is calculated by taking weighted sum of above 3 factors.

##### Why such heuristic choice
Using base heuristic, we can find the optimal solution however, number of states it has to explore results in high amount of time to get solution. To improve this, we added haversine distance. This helps selecting the city which is close to the goal city. To improve more on this, we decided to add another variable of direction which is calculated by calculating slope between 1) current city and next city to be explored and 2) current city and goal city. Slope is calculated by using coordinates of the cities in context. Finding the slope helps choose optimal direction.

##### gps calculations
As the gps file does not have co ordinates for all the cities. I calculated approximated gps values by taking weighted average of connected cities. Weight for connected city was the distance between the cities.

##### Improvements

The implementation could be improved by storing heuristic cost for each connected city. So next time a particular fringe item is to be explored, we do not need to recalculate all the values again.
