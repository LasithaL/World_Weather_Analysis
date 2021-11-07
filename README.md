# World_Weather_Analysis
The Weather Data Analysis repository was created to be used as a location where all pertinent files can be stored. Having a central location that is easily shared with other members of the workgroup is essential in the joint efforts of getting work done.  The repository allows us to check out portions of the project and work on them individualy while keeping ahead of changes through revision control. This method is far better than routing files on email or shared file location where only one member can work on a file at a time. Below is a brief explanation of the project.

## Weather Database
For this project 2000 random Latitude, Longitude pairs were created.  Using the nearby city search of citypy, cities were matched up to the coordinates if possible. Coordinates with no sities attached were dropped form the DataFrame

The valid coordinates, through an API call to the OpenWeatherMap wer used to collect Latitude, Longitude, Maximum Temperature, Percent Humidity, Percent Cloudiness, Wind Speed, and Weather Description. The data was saved into a CSV file to be used in finding vacation travel destinations.

## Vacation Search
The data generated in the previous section was used to narrow down cities with favouable temperature by filtering the maximum temperature data of the saved file. The data was then cleaned to remove any empty rows to clear any empty rows if any. The cleaned dataset was then used to retrieve hotel information using a google maps places API. Any city where a hotel was not found was removed from the data set.

A google map was created with the city data with markers shown for each of the cities with pop up infomartion Hotel Name, City Name, Country Code, Weather Description, and Maximum Temperature.

## Vacation Itinerary
The search criteria from the Vacation Search was used to select four cities within a country. A round trip direction set and a route map were created using the google map directions API.

## Issue
- There were cities in the country of Namibia that associated with the country code of 'NA'. In the process of imprting the data from the CSV file, these data points were tagged as values with NaN. When cleaning the data for 'null' or 'NA' values, the cities from Namibia was also cleared.
    - There were two solutions that I was able to find through searches. One was to type cast the Country Code to astype(str), the other was to import the csv file with keep_default_na=False. These solutions worked if the dataset was to be static. Part of the project was to add a column to the dataset to include nearby hotels. Once the adjustments were made and the new column was added Iw as unable to clear any rows with no hotel information from the dataset.
    - The solution that worked for me was to import the csv file twice. Once as normal 'city_data_df' and the other with keeping the default na as False 'city_data_df1'. Then I replaced the 'Country' column of df with the 'Country' column of df1. This solved the issue and I was able to keep the country code of 'NA' for Namibia and remove any blank hotel names by inserting np.NaN into the rows.