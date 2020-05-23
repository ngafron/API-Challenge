Weather and Vacation Weather API 

Description
- Utilizing Pandas and OpenWeatherMap API, I created a representative model of weather across over 500 world cities. I was tasked with creating visulations for relationships about...

1. Temperative vs. Latitude
2. Humidity vs. Latitude
3. Cloudiness vs. Latitude
4. Wind Speed vs. Latitude

Further analysing them based off of using their hemisphere attritube as a correlation. 

```
url = "http://api.openweathermap.org/data/2.5/weather?"
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
Temperature vs Latitude Example
```
temps = weather_df["Temperature"]

x_axis = weather_df["Latitude"]

plt.scatter(x_axis, temps, marker="o", facecolors="red", edgecolors="black")
plt.title("City Latitude vs. Temperature")
plt.xlabel("Latitude")
plt.ylabel("Temperature")
plt.savefig('../output_data/NG_temp.png')
```
Northern Hemisphere - Max Temp vs. Latitude Linear Regression
```
x_values = northern_df["Latitude"]
y_values = northern_df["Temperature"]

plt.scatter(x_values, y_values, marker="o", facecolors="red", edgecolors="black")
plt.plot(x_values, line_reg(x_values, y_values),"b-")
plt.annotate(line_eq(x_values, y_values),(10,240),fontsize=15,color="red")
plt.title("Northern Hemisphere - Max Temp vs. Latitude Linear Regression")
plt.xlabel("Latitude")
plt.ylabel("Temperature")
print(f"The r-squared is: {r_value(x_values, y_values)}")
plt.show()
The r-squared is: -0.8429321063481434
```
