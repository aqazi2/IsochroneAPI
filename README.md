Contents
Introduction to Mapbox Isochrone API	1
Getting started	2
Using the Isochrone API	4
Create a map	5
Add the sidebar:	6
Add the Isochrone API	8
Draw the isochrone contour:	9
Make the app interactive	10
Add a marker	11
Final product	13













Introduction to Mapbox Isochrone API

The Mapbox Isochrone API is a powerful tool that allows developers and geospatial enthusiasts to analyze travel times and create visually appealing isochrone maps. Isochrone maps display areas that can be reached from a specific location within a given travel time or distance. They are invaluable for various applications, such as urban planning, logistics, and transportation analysis.
The Mapbox Isochrone API integrates seamlessly with the Mapbox platform, which provides high-quality map data and visualization tools. With this API, you can access isochrone polygons, retrieve data for different travel modes (e.g., walking, cycling, driving), and customize the analysis based on user preferences. Whether you're building a navigation app, optimizing delivery routes, or evaluating accessibility, the Mapbox Isochrone API empowers you to gain insights into how far you can travel within a specified time frame.
In this tutorial, we will explore how to use the Mapbox Isochrone API to create isochrone maps, enabling you to visualize and analyze travel times for different scenarios. You will learn how to set up an interactive web application that allows users to select travel profiles and durations, providing real-time feedback on travel time boundaries on a map. This introduction serves as a starting point for harnessing the capabilities of the Mapbox Isochrone API to solve location-based problems and enhance user experiences.

Getting started


1.	Access Token:
•	An access token is a key that associates your usage of Mapbox services with your Mapbox account.
•	You can obtain this token from your Mapbox account. It serves as a form of authentication to access Mapbox services.
•	
•	You can usually find your access token on your Account page after logging into your Mapbox account. If you don't have an account, you'll need to sign up for one.
•	https://www.mapbox.com/account/

2. Mapbox GL JS:
•	Mapbox GL JS serves as a fundamental component for building web maps in this tutorial. It is a JavaScript API provided by Mapbox designed explicitly for constructing interactive maps for web applications. You'll be using it to incorporate the map into your app, enabling users to visualize and interact with the isochrone data. Mapbox GL JS
3. Mapbox Isochrone API:
•	The Mapbox Isochrone API is the core of this tutorial. This API is the engine behind the calculations for regions that can be reached within specific travel times from a given location. It computes these areas and returns them in the form of contours, represented as polygons or lines. These contours can be seamlessly integrated into your map, visually showcasing areas that users can reach within defined time constraints. Isochrone API
4. Mapbox Assembly:
•	For styling the user interface (UI) of your web application, we recommend using Mapbox Assembly. Assembly is an open-source CSS framework. By applying Assembly's styles, you can create an aesthetically pleasing and user-friendly UI for your travel-time estimation app. This helps in providing an intuitive user experience. Assembly 
5. Text Editor:
•	In order to code and develop the app, you'll need a text editor. The choice of text editor is yours; you can use your preferred text editor to write HTML, CSS, and JavaScript. This is where you'll create and structure the code for your web application. It's crucial to have a text editor to craft and edit the necessary files that power your app's functionality. Downloads | Notepad++ (notepad-plus-plus.org)

Using the Isochrone API

To make your travel-time estimation app work seamlessly, you need to understand how to harness the power of the Isochrone API. This API is your tool for calculating and displaying areas reachable within specific time constraints. Here's a step-by-step explanation of how to make it work:
Three Essential Parameters:
1.	Profile: This parameter determines the Mapbox routing profile your query should use. The profile depends on the type of travel you want to analyze. For example, choose "walking" for pedestrian travel times, "cycling" for bicycle travel times, or "driving" for car travel times.
2.	Coordinates: You'll need to provide a set of coordinates, which is essentially a {longitude, latitude} pair. These coordinates act as the center point around which the isochrone lines will be drawn. This point is where your travel-time calculations originate.
3.	Contours Minutes: This parameter is vital. It defines the duration of trips in minutes. You can specify one or more times, separated by commas, to indicate different time limits. Be aware that the maximum duration for each isochrone you can request is 60 minutes.
Optional Parameters:
The Isochrone API offers some optional parameters that you can use to tailor your query. For your app's specific purpose, you'll focus on one optional parameter:
•	Polygons: This parameter gives you control over whether the isochrone contours should be returned as GeoJSON polygons or linestrings. If you set "polygons" to "true," any contour that forms a ring will be returned as a polygon. This makes it easier to visualize the areas users can reach.
Constructing an API Request:
To put all these parameters together into an API request, you need to structure a URL as follows:
https://api.mapbox.com/isochrone/v1/mapbox/{profile}/{coordinates}.json?{contours_minutes}&access_token=pk.eyJ1IjoiYXFhemkiLCJhIjoiY2xvaHc4dWkzMGZqajJrcHF5MDlxY2FnNCJ9.w2rhdjTBwODsGV8thEVZmw

with your specific values. For example:
https://api.mapbox.com/isochrone/v1/mapbox/driving/-117.17282,32.71204?contours_minutes=15&polygons=true&access_token=YOUR_ACCESS_TOKEN

In this example, the request uses the driving profile, specifies coordinates, sets a travel time of 15 minutes, and requests results in polygon format.
Inspecting the JSON Response:
After making your API request, you can paste it into your web browser's address bar to receive a JSON response. This response holds critical information for your app's functionality:
•	Geometry Object: This part of the response includes an array of coordinates that define the outlines of the isochrone contour. These coordinates are the building blocks that create the shape of the reachable area on your map.
•	Features Object: In this section, you'll find details on how the isochrone should be visually represented. It includes information about the fill color and fill opacity. This data is your toolkit for styling and drawing the isochrone contours on your app's map.
Create a map

To get your app rolling, the first step is to build a map using Mapbox GL JS. Here's a detailed breakdown of how you can set up your HTML file for this purpose:
1. Open Your Text Editor:
Before we dive in, make sure you have a preferred text editor ready to go. You'll be writing HTML, CSS, and JavaScript, so a good text editor is your essential tool.
2. Create a New HTML File:
In your text editor, create a new file and save it with the name "index.html." This will be the main HTML file for your app.
3. HTML Setup:
Now, it's time to set up your HTML file. Copy and paste the following HTML code into your "index.html" file. This code will be the foundation for your app:
code

Here's what each part of the code does:
•	The <head> section imports the necessary Mapbox GL JS and Assembly CSS and JavaScript files, which are essential for creating and styling the map.
•	The <style> section provides some basic CSS for styling the page. It ensures the map takes up the entire width and height of the page without margins or padding.
•	Inside the <body> section, there is a <div> element with the ID "map." This is where the map will be displayed.
•	The <script> section initializes the map. Make sure to replace 'YOUR_MAPBOX_ACCESS_TOKEN' with your actual Mapbox access token.
4: Save and View the Map
•	Save your changes in the text editor.
•	Open the "index.html" file in your web browser.
You should see a rendered map centered on the Mapbox  in Chicago. This is your basic map created with Mapbox GL JS.
 

Add the sidebar:
To enhance the functionality of your web app, you should now implement a sidebar that allows users to select their transportation preferences and the desired time duration. This sidebar will be designed using HTML and CSS, with a focus on Assembly classes for styling.
1.	Add a New Div Element in the HTML Body: Within the <body> section of your HTML document, insert a new <div> element. This <div> will serve as the container for your app's options and will be styled using Assembly classes for a consistent and appealing appearance.
Here, we use the absolute, fl, my24, mx24, py24, px24, bg-gray-faint, and round Assembly classes to control the positioning, margin, padding, background color, and border radius of the container.
Create the Sidebar Content:
Inside the newly created <div>, you can add the content for your sidebar. The content will consist of two sections: one for selecting a travel mode and another for choosing a maximum duration.
Code:
1.	This code creates a sidebar with options for users to select their preferred mode of transportation (walking, cycling, or driving) and the maximum duration (10, 20, or 30 minutes). The Assembly classes are applied to style these elements.
2.	Styling Using Assembly: The Assembly classes applied in this code snippet provide CSS styling for various elements within the sidebar. These classes control attributes such as positioning, padding, margin, background color, and border radius, resulting in a visually appealing and consistent design. It's worth noting that you can also use your preferred CSS framework or plain CSS for styling if Assembly is not your choice.
3.	Testing the Sidebar: After implementing this code, save your work and refresh the web page. You should now see the sidebar displayed on the left side of your web app. It will look visually pleasing due to the styling applied with Assembly classes. However, at this stage, clicking the buttons won't trigger any actions.

 

Add the Isochrone API

Create a Function for Isochrone API Integration: To connect with the Isochrone API and retrieve data, you need to create a JavaScript function. You can name this function getIso. This function will construct the query string and utilize the fetch method to make an API call. Add the following code to your JavaScript file, preferably after the map constant that you previously used to initialize the map: paste the code inside body and in your JavaScript part  <script>code</script>.
Code:
1.	Here's what each part of this code does:
•	The constants urlBase, lon, lat, profile, and minutes are set. urlBase is the base URL for the Isochrone API, while lon and lat represent the coordinates of the location you want to analyze. profile sets the default routing profile (e.g., cycling), and minutes sets the default duration (e.g., 10 minutes).
•	The getIso function is created as an async function. It constructs the query URL and uses the fetch method to make a GET request to the Isochrone API. It includes the specified parameters and the Mapbox access token.
•	The API response is obtained and parsed using await query.json().
•	The data is logged to the console using console.log() for examination.
2.	Testing: At this stage, you haven't set up the layers necessary to visualize the isochrone contours on the map. As a result, when you refresh your web page and open the browser's developer tools panel, you will see the Isochrone API response object printed in the console. This allows you to inspect the data returned by the API, and it serves as a useful step for testing and debugging.
 

Draw the isochrone contour:
To draw the isochrone contour on your map, you'll need to make some changes to your JavaScript code and set up a source and a layer. Here are the detailed steps to accomplish this:
1.	Understand the Goal: In the previous step, you successfully made an API call and displayed the response in the console. However, for your web app, the objective is to visually represent the isochrone contours on the map using Mapbox GL JS.
2.	Remove the getIso() Call: You no longer need the getIso() call that was used for testing purposes. You'll replace it with code that sets up the source and layer for the isochrone contours.
3.	Setting Up the Source and Layer: To draw the isochrone contours, you need to create a new source and a new layer in Mapbox GL JS. Here's how to do it: Add the Provided Code to Your JavaScript File: Inside body in your JavaScript file<script>code</script>
Code:
Code explained:
1.	map.on('load', () => { ... }); ensures that this code runs when the map has fully loaded.
2.	map.addSource('iso', { ... }); creates a source named 'iso'. This source is of type 'geojson' and starts with an empty FeatureCollection.
3.	map.addLayer({ ... }); adds a new layer named 'isoLayer' to the map. This layer uses the 'iso' source you just created. It's of type 'fill', which is used to represent the filled area of the isochrone contour. You can customize the fill color and opacity.
4.	getIso(); is called to make the API request and obtain the isochrone data.
4.	Set the Source Data: In your getIso function, replace the console.log(data) statement with the following code to set the 'iso' source's data to the data returned by the API query:
map.getSource('iso').setData(data); 
This line updates the 'iso' source with the isochrone data you received from the API.
5.	Save and Test: Save your changes in your JavaScript file and refresh your web page in the browser. When the page loads, an isochrone contour for the specified parameters (in this case, the cycling routing profile and a trip duration of 10 minutes) will be drawn on your map.
By following these steps, you will be able to visualize the isochrone contours on your map within your web application. Users can then interact with the application to explore different isochrone areas based on their transportation mode and time duration preferences.
 


Make the app interactive

To make your app interactive, you'll need to connect the buttons you created earlier to your JavaScript code. This will allow users to select different routing profiles and trip durations and see the updated results on the map. Here's a detailed explanation of the process:
1.	In your JavaScript code, add the following code at the bottom, just before the closing </script> tag:
Code
Here's what this code does:
•	It selects the HTML form element with the id "params," which contains the radio buttons for choosing the routing profile and trip duration.
•	It adds an event listener to the form, specifically listening for the "change" event.
2.	Inside the event listener function, it checks which button was clicked (either a profile or duration button) based on the event.target.name property.
3.	If a profile button is clicked, it updates the profile variable with the new value chosen by the user.
4.	If a duration button is clicked, it updates the minutes variable with the new value chosen by the user.
5.	After updating the parameters, it calls the getIso() function again. This function constructs a new API query with the updated parameters and redraws the isochrone contours on the map.
Now, when users click on different combinations of routing profiles and trip durations on your app, the event listener will capture their choices, update the parameters, and trigger the API query to display the corresponding isochrone contours on the map.
Make sure to save your changes and refresh the page in your browser. You can then click on different buttons to see the isochrone contour change according to the selected routing profile and trip duration. This makes your app interactive and user-friendly.
 

Add a marker

Adding a Marker:
As the final step, we will incorporate a marker into your map. This marker serves the purpose of emphasizing the center of your isochrone contour, making it more visually distinctive. For this example, we have chosen to position the marker at the coordinates corresponding to the Mapbox office in Washington, D.C.
Placing the Marker on the Map:
To display the marker on your map when it loads, you should incorporate the following code under the map.on('load') function:
// Create a marker with the correct lngLat object
  const marker = new mapboxgl.Marker({
    color: '#314ccd'
  }).setLngLat([lon, lat]).addTo(map);
 
This code sets up the marker at the specific coordinates you've defined. As a result, when you save your work and refresh the page, a blue marker will be visible at the designated coordinates.
 
Final product

You've successfully created an app that leverages the Mapbox Isochrone API to help users visualize travel options within specific time limits, whether they are walking, biking, or driving. This kind of application can be very useful for people to plan their journeys and understand the areas accessible within their desired timeframe.
Code


References:
•	Isochrone API: API docs. Mapbox. (n.d.). https://docs.mapbox.com/api/navigation/isochrone/ 
•	Isochrone Map Generator. Maptive. (2023, February 28). https://www.maptive.com/isochrone-map-generator/ 
•	What are isochrones? Mapbox. (n.d.-b). https://www.mapbox.com/insights/isochrones 
