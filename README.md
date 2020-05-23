Weather and Vacation Weather API 

Description
- Utilizing Pandas and OpenWeatherMap API, I created a representative model of weather across over 500 world cities. I was tasked with creating visulations for relationships about...

1. Temperative vs. Latitude
2. Humidity vs. Latitude
3. Cloudiness vs. Latitude
4. Wind Speed vs. Latitude

Further analysing them based off of using their hemisphere attritube as a correlation. 


```url = "http://api.openweathermap.org/data/2.5/weather?"
query_url = url + "appid=" + weather_api_key + "&q="
city_names = []
lat = []
lng = []
temp = []
humid = []
clouds = []
wind = []
number = 1

for city in cities:
    try:
        response = (requests.get(query_url + city + "&units=imperial")).json()
        city_names.append(response['name'])
        lat.append(response['coord']['lat'])
        lng.append(response['coord']['lon'])
        temp.append(response['main']['temp'])
        humid.append(response['main']['humidity'])
        clouds.append(response['clouds']['all'])
        wind.append(response['wind']['speed'])
        print(f'City number {number} of {len(cities)} complete. | Added {city}')
        number = number + 1
    
    except KeyError:
        print(f'Missing data in city number {number} of {len(cities)}. | Skipping {city}')
        number = number + 1
```
