|November 8th, 2019|

|
## Executive Summary
 |
| --- |

### Problem

In the event of a natural disaster, what kind of businesses and how many businesses will be available to a population a population. Also can we identify the groups of people that would be without services in the event of a distaster.

## Target Audience

The Tableau heat map and graphics are to be used by FEMA to indentify populations and services in the event of a disaster.

## API Process

When calling the Yelp Fushion API we used the the key provided by Yelp's registry and built a dictionary of categories to fun through the API call. These included, but were not limited to security for safety outfits, Water Suppliers for food outfits, Emmergency Rooms for health outfits, Utlitity providers for energy outfits, ISPs for telecomunication outfits, Medical transports for transportation services, biohazard clean-up services for Hazard stations and Police stations for public services. These were concated into separate lists and run through a for loop wiht and API call.

During the API call, the data run through a loop that will return a maximum of 50 results per call. In order to increase this, there for loop will offset by an additional 50 per call. This will return a maximum of 2500 results per query. This is then appended to a lists to be run through a separate for loop using the data portion of the call.

When running through the data portion of the call, the data was converted into a list. This list was run through a for loop and then created into a data frame for additional cleaning. The data that was pulled from the initial query is the name of the business, the address of the business, the phone number of the business, the businesses latitude and longitude, the city and zip code of the business and the business category. These were then imported into a dataframe to be concated into the data cleaning process.

## Data Cleaning

In the cleaning process the cities corresponding webscrapes were combined into a single citiwide dataframe. This is due to each dataframe needing to join all of the FEMA categories. After all of the municipalities were joined, there were concatated into a single data frame that has all of the information for every municipalities. All duplicates within the data frame were dropped resulting in approximately 9,000 disaster service stations in GA. After this was done, the FEMA codes for the businesses were added to the data frame to ensure that the categories could be mapped according. Then the data frame was filter for results only wihtin GA and then the cities were standardized. After the initial data cleaning, the zip code latitude longitudes and populations were concated onto the data frame using information from the US census. These were joined onto the data frame using the zip code and then were exported for EDA and graphing.


## EDA and graphs

Using the clean data frame, we found that there were approximately 8,500 FEMA stations mowith the majority concentrated around the north metro Atlanta area. The most serviced places are within the North Atlanta area such as Buckhead and suburbs just outside of the city such as Sandy Springs and Alpharetta. When looking at other concentrated areas, the other major towns like Macon, Savannah, Athens and Saint Simons are also well serviced. An interesting not that we found is that all services are either concentrated around city centers and major highways. While this does make sense from a business stanpoint, it does leave more rural populations isolated from services in the event of a distaster. An example would be Alamo, Ga with a population of approximately 5,000 and no access to services in the event of an emmergency. Other portions of cities such as Athens do not have any services indicating that they are underserved within the Athens city limit. In order to see a full exploration of all of the information, please see EDA notebook.

## Tool

The current tool is a heat map in Tableau. This is currnetly representing the population of an area by a deeper shade of blue and when access can show the number of services available within that area. 

## Findings

1. The major metro areas within GA can be served well within the event of a distaster. Considering the majority of the population is concetrated around Atlanta, this is not surprising. The more major concern is that there are some zip codes within a safety, or police service in their immediate area.

2. The most available services within the area are food followed by medical services. In the event of a disaster, personal can quickly be assured that populated areas will have access to food and medical treatment needed.

3. There are additional services available along the major interstates and major municipalities such as Macon, Augusta, Rome, Savannah and other major areas. This would make sense due to businesses needing a consistant 

4. There are several smaller areas within Georgia that lack services are father away from major roads and municipalities. These areas would be cut off from services in the event of a disaster.

## Recommendations

This is currently a static view that can be used to asses the total available services at this time. There are cards of information that can allow a user to access a the exact location cards of the business in real time. You can use the information available in the static view using the is_closed boolean function. This is currently all business are shown as active, but this can be used to give a live view of the map to be used in real time and give exact location and contact information. Also this only shows the services available in Georgia, but can be expanded throughout the country using similar principles. All of the data and code is available to do so, but due to limitations are API resources this was not capable in this timeframe.

## Data 

FEMA disaster Data for Atlanta Dictionary

|Feature|Type|Dataset|Description|
|---|---|---|---|
|Index|int|all|This is the row ID for the data set.| 
|name|object|all|The name of the business according to Yelp Fushion API.|
|address|object|all|The address of the business according to Yelp Fushion API.|
|phone_number|object|all|The phone number of the business according to Yelp Fushion API.|
|location_latitude|int|all|The latitiude of the location according to the Yelp Fushion API.| 
|location_longitude|int|all|The longitude of the location according to the Yelp Fushion API.| 
|is_closed|boolean|all|The currently open for business marker of the location according to the Yelp Fushion API.| 
|city|object|all|The city of the business according to Yelp Fushion API.|
|zip_code|int|all|The zip code of the business according to Yelp Fushion API.|
|category|object|all|The Yelp primary category of the business according to Yelp Fushion API.|
|FEMA_category|object|all|The correlated FEMA category for the business that matches with the Yelp primary category.|
|zip_code_latitude|int|all|The latitiude of the zip code according to the 2010 US Census.|
|zip_code_longitude|int|all|The longitude of the zip code according to the 2010 US Census.|
|2010_zip_code_census_population|int|all|The population of the zip code according to the 2010 US Census.|

## Sources
 
 Yelp Fushion API calls
 2010 Census Data