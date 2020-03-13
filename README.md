Calculate the fastest way from point A to point B with the use of the Warsaw city bikes.

#Introduction

Last two decades are being called the ‘golden age’ of Polish economic growth with its center in the country's capital, Warsaw.  Unfortunately with a great power comes great responsibility, in this case I am talking traffic which by far excided the road capacity. City residents on average spend 415 hours in traffic jams a year. It is more than an hour a day. In 2012 city bikes were introduced as one of the solutions for this issue. 
As a former ‘Warszawiak’ I can recommend everyone who has an opportunity to visit the city to use one city bikes. They are amazingly cheap and easy to use. You can download mobile app and rent bike in no time. There are almost 400 bike stations with around 5700 bikes. 
With the application installed we can see the map of the bikes and count of available bikes on the station. But if you don’t know Warsaw it may not be enough. Let’s say you want to get from point A to point B in the shortest possible time with the use of the city bike. How to decide which station to pick as a starting point and which as a destination? Unfortunately answer to that question is not as easy as going to the closest station on the map. 
Data 

To calculate the fastest route we will need location of the station with available bikes, as opposed to trying to calculate the fastest way from the station that has no available bikes.  All of this data is fairly simple to get from this page: https://www.veturilo.waw.pl/mapa-stacji/. 

#Methodology

GitHub repository was used to host Jupiter notebook which was used to collect, store and visualize the data. First step is gathering the data from city bike provider’s webpage and storing it into the table.
 
To test a data city map was created with the use of folium library with bike station superimposed as a markers.
 
As an input I provided two addresses in Warsaw, start and finish. Format of the addresses is not important as we use geopy library to convert it into geo coordinates. Let’s add this two points on the map.
 
At this point we have address A where we start our journey and address B as destination point. From this data we can calculate the distance between those points and every available station. It is important to remember not to calculate distance between point A and stations that don’t have available bikes. Geopy was used for this measurement, as a result we got two tables, which I limited to top 5 closes stations. 
 
 
Unfortunately geographical distance may be deceptive so I decided to use openrouteservice library to calculate walking time duration from point A to five closest stations and the same duration from 5 stations near destination to point B. 
 
 
Next I calculated the cycling time from every station close to point A to every station close to point B.
 
With three of those calculation we are ready to decide which route is going to be the fastest. To do that we need to combination that give us the shortest duration time. As a result we one row will be generated with the following columns:
 
With the use of folium and openrouteservice libraries we can now generate the fastest route on the map. 





Walking route from point A to selected station:
 
Walking route from point destination station to point B:
 

Overall route with mid section calculated for the for the bike:
 
 
#Conclusion

With available data and python libraries we were able to calculate the fastest route from A to B in the city of Warsaw with the use of city bikes.

#Future plans

I plan on adding additional features to the app, calculating the bike route comfort. So the user can pick the route that only has bike lanes available. 
Another feature is adding point in between. If user wants to do something on the way home we can calculate the fastest way to do that. Idea is to cluster the stations by the venues available around every station. 
As the input user would need to provide venue type, for example: cinema. This will allow to calculate fastest route from start to destination address with stop in between to watch some movie.


