# CS459-Service-Mashup
CS459 - Introduction to Services Computing


# Travel Guide

__Description of Business & Motivation__

COVID-19 has started to change people's life in different aspects, especially limiting their experience of traveling. However, it is going to disappear eventually, these days. As a result of that, people started to travel across different countries and places again. Therefore, it is necessary to choose where to go by taking into account their interest, in which sightseeing places, upcoming events, and weather conditions are suitable for them. Searching all those aforementioned characteristics of a new place can be cumbersome, considering the fact it is done separately. So, my business is offering the users to simply search the name of the location they want to visit, and it provides all necessary information quickly in the same user-friendly interface, including weather conditions- detailed descriptions, temperature, humidity and so on; one of the most famous places around there along with the rate according to the previous customer reviews; finally one of the upcoming mass scale events will be held at that region with the necessary dates and time.

__A brief explanation of the Web services used for the mashup__

__OpenTripMap API - GeoCoding__ <br />
It takes an input of the name of the place and converts the name into the latitude and longitude, respectively. The name of the place will be input_text into the msg.payload, and the necessary result will be transferred as msg.payload.lat and msg.payload.lon.

__OpenWeatherMap API__ <br />
It receives the latitude and longitude of the desired location through the flow of msg.payload. Then it returns the verbal description of the current weather along with timezone and other details needed.

__OpenTripMap API - Sightseeing Places__ <br />
It receives the latitude and longitude of the desired location through the flow of msg.payload, and returns most famous places closest to the chosen location with an observation distance of radius=2000 meters.

__TicketMaster Discovery API - Event Details__ <br />
It receives the latitude and longitude of the desired location through the flow of msg.payload, and returns the upcoming events by assigning unique id’s to them along with necessary dates & times.

__TicketMaster Discovery API - Event Images__ <br />
It receives the id of an event retrieved by the Event Details request, then it provides various images regarding that event.

__Node-Red Dashboard__ <br />
It creates a live webpage in a very quick manner, by customizable layout in node-red by neglecting the cumbersome work to write front-end and back-end codes. It basically facilitates the work by providing various codeable nodes of text, input, form etc. to make the interface more interactive easily.

__Explanation about the mashup application__ 

In order to fulfill the demand discussed above, I have developed a “Travel Guide” Service. It basically reduces the cumbersome process of searching about the current events and situations in some places, which facilitates the answer to the question of where and when to go? 
The Process starts with a user-friendly interface in which the user is asked to enter the name of places he/she considers to visit or wants to get some information. Afterwards the geocoding API will be requested to provide the latitude and longitude in order to feed other API’s for other concerns. 
Here there are three sub-branches, i.e. services, will be provided.
On the weather side, the http-requested results from API are converted to the nice-looking format along with adjustments to make it eye-catching and human readable by the help of function- Format Weather. Then outcomes will be fed into the text results of the dashboard, and they will appear in the interface to show temperature, timezone, description of weather, sunrise/sunset times, humidity.
On the sightseeing places side, the http-requested results from API will be received. Then the results will be formatted in the function- Famous Place, and it will also choose a random place among all retrieved results along with its rate by previous reviewers and category, i.e. details. All those will be shown on the second column of the dashboard-layout.
On the events side, the first API will get the events by sending the request. Then the function- get id- will make global variables to flow inside of the msg (not msg.payload) including the id, name, date, and time of the event. Afterwards, the second API will request to get the images of the event with a specific id. Before showing the results the function- change w/h- will choose a single image from the event and will make adjustments on the sizes at the dashboard-layout to put the image. At the end, the chosen event’s name, its start date/time, and related image will be shown in the interface. In case of no event found at the specified place, it shows an empty screen. 

__Reference__

[1] https://home.openweathermap.org/  <br />
[2] https://opentripmap.io/product  <br />
[3] https://developer.ticketmaster.com/products-and-docs/apis/discovery-api/v2/ 

__Remark__

Note that since it is publicly used, unique API keys have been removed from flow. In case of reproducing the results, one should create their own keys through the open-API’s provided in reference.


__Further Extensions__

There is a very large open-room for further advancements and improvements. <br />
First of all, even though covid-19 pandemic is almost disappearing, I am planning to add an API to show the current data- cases in specific countries. <br />
Secondly, for now we can only see one event or one sightseeing place at a time, which is randomly chosen and changes in each input (even though input is the same). I will try to extend by adding buttons to change and see all events & places to visit in order to provide more flexibility. <br />
Thirdly, it is also one of the considerations to know the ticket prices when we travel. Since I was not able to find open-api’s to provide the ticket prices between  two places, at this phase I was not able to implement. But in further development, one can try to integrate the some airline API to show the prices in order to give some rough idea to the customer about the prices. <br />
Finally, as an extension of the third one, one can add a living-cost API to see the accommodation & food prices for a fixed time interval.
