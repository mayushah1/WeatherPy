
In this example, you'll be creating a Python script to visualize the weather of 500+ cities across the world of varying distance from the equator. To accomplish this, you'll be utilizing a [simple Python library](https://pypi.python.org/pypi/citipy), the [OpenWeatherMap API](https://openweathermap.org/api), and a little common sense to create a representative model of weather across world cities.

Your objective is to build a series of scatter plots to showcase the following relationships:

* Temperature (F) vs. Latitude
* Humidity (%) vs. Latitude
* Cloudiness (%) vs. Latitude
* Wind Speed (mph) vs. Latitude

Your final notebook must:

* Randomly select **at least** 500 unique (non-repeat) cities based on latitude and longitude.
* Perform a weather check on each of the cities using a series of successive API calls. 
* Include a print log of each city as it's being processed with the city number, city name, and requested URL.
* Save both a CSV of all data retrieved and png images for each scatter plot.

As final considerations:

* You must use the Matplotlib and Seaborn libraries.
* You must include a written description of three observable trends based on the data. 
* You must use proper labeling of your plots, including aspects like: Plot Titles (with date of analysis) and Axes Labels.
* You must include an exported markdown version of your Notebook called  `README.md` in your GitHub repository.  
* See [Example Solution](WeatherPy_Example.pdf) for a reference on expected format. 

## Three observable trends based on the data

 - Tempratures in cities close to equator (-20 to +20 latitude) are hotter (more than 80F) during february
 - Humidity is close to 100% near equater and on positive latitudes
 - wind speed is more than 30 MPH for the latitude between +60 and +70



```python
# Dependencies
import matplotlib.pyplot as plt
import requests as req
import pandas as pd
import openweathermapy.core as ow
import numpy as np
import seaborn as sns
from citipy import citipy
import json
from localenv import api_key
```


```python
url = "http://api.openweathermap.org/data/2.5/weather?"
units = "imperial" 
appid = api_key
settings = {"units": "imperial", "appid": api_key}
query_url = f"{url}appid={api_key}&units={units}&q="
```


```python
random_lat = []
random_lon = []
cities = []
country_code = []
name = []
weather_json = []
weather_dict = {}
for x in range (1400):
    random_lat = np.random.uniform(low=-90, high=90, size=1)
    random_lon =np.random.uniform(low=-180, high=180, size=1)
    cityname = citipy.nearest_city(random_lat, random_lon)
    if cityname not in cities:
        cities.append(cityname)
print(len(cities))
```

    580



```python
c=1
for city in cities:
    name.append(city.city_name)
    country_code.append(city.country_code)
    response = req.get(query_url+city.city_name).json()
    print("Processing Record "+str(c)+" of "+ str(len(cities))+" "+query_url+city.city_name)
    weather_json.append(response)
    c +=1
    
print("-"*100)
print("                Data Retrieval Complete")
print("-"*100)
```

    Processing Record 1 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=sentyabrskiy
    Processing Record 2 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=nelson bay
    Processing Record 3 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=carnarvon
    Processing Record 4 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=yellowknife
    Processing Record 5 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=port alfred
    Processing Record 6 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=bluff
    Processing Record 7 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=hermanus
    Processing Record 8 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=severo-kurilsk
    Processing Record 9 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=cape town
    Processing Record 10 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=qaanaaq
    Processing Record 11 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=mataura
    Processing Record 12 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=salta
    Processing Record 13 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=porgera
    Processing Record 14 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=kapaa
    Processing Record 15 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=olpad
    Processing Record 16 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=port hardy
    Processing Record 17 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=pangnirtung
    Processing Record 18 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=itarema
    Processing Record 19 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=ushuaia
    Processing Record 20 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=atuona
    Processing Record 21 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=kamenskoye
    Processing Record 22 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=laguna
    Processing Record 23 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=castro
    Processing Record 24 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=nikolskoye
    Processing Record 25 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=ponta do sol
    Processing Record 26 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=bethel
    Processing Record 27 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=berlevag
    Processing Record 28 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=narsaq
    Processing Record 29 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=butaritari
    Processing Record 30 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=kamenka
    Processing Record 31 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=rikitea
    Processing Record 32 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=oranjemund
    Processing Record 33 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=limon
    Processing Record 34 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=acarau
    Processing Record 35 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=busselton
    Processing Record 36 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=namatanai
    Processing Record 37 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=ust-ishim
    Processing Record 38 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=mao
    Processing Record 39 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=souillac
    Processing Record 40 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=faanui
    Processing Record 41 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=ayorou
    Processing Record 42 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=east london
    Processing Record 43 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=taunggyi
    Processing Record 44 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=saint-francois
    Processing Record 45 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=nouadhibou
    Processing Record 46 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=chihuahua
    Processing Record 47 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=upernavik
    Processing Record 48 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=lata
    Processing Record 49 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=victoria
    Processing Record 50 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=bredasdorp
    Processing Record 51 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=rodrigues alves
    Processing Record 52 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=bartica
    Processing Record 53 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=tezu
    Processing Record 54 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=touros
    Processing Record 55 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=anchovy
    Processing Record 56 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=nipawin
    Processing Record 57 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=taolanaro
    Processing Record 58 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=colonia
    Processing Record 59 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=iqaluit
    Processing Record 60 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=acapulco
    Processing Record 61 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=thompson
    Processing Record 62 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=morehead
    Processing Record 63 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=khatanga
    Processing Record 64 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=broome
    Processing Record 65 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=rustenburg
    Processing Record 66 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=saskylakh
    Processing Record 67 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=sangar
    Processing Record 68 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=lloydminster
    Processing Record 69 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=beloha
    Processing Record 70 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=leshukonskoye
    Processing Record 71 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=yarada
    Processing Record 72 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=ribeira grande
    Processing Record 73 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=krasnovishersk
    Processing Record 74 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=jamestown
    Processing Record 75 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=tiksi
    Processing Record 76 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=srednekolymsk
    Processing Record 77 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=puerto ayora
    Processing Record 78 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=port hedland
    Processing Record 79 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=havoysund
    Processing Record 80 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=kavieng
    Processing Record 81 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=albany
    Processing Record 82 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=vila velha
    Processing Record 83 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=dikson
    Processing Record 84 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=henties bay
    Processing Record 85 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=mar del plata
    Processing Record 86 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=poronaysk
    Processing Record 87 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=hobart
    Processing Record 88 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=ostrovnoy
    Processing Record 89 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=punta arenas
    Processing Record 90 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=vaini
    Processing Record 91 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=san juan
    Processing Record 92 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=nemuro
    Processing Record 93 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=saint-philippe
    Processing Record 94 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=duku
    Processing Record 95 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=georgetown
    Processing Record 96 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=kavaratti
    Processing Record 97 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=guerrero negro
    Processing Record 98 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=cagayan de tawi-tawi
    Processing Record 99 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=vaitupu
    Processing Record 100 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=komsomolskiy
    Processing Record 101 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=port elizabeth
    Processing Record 102 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=norman wells
    Processing Record 103 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=grand river south east
    Processing Record 104 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=barentsburg
    Processing Record 105 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=pozoblanco
    Processing Record 106 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=sao jose da coroa grande
    Processing Record 107 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=viedma
    Processing Record 108 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=hithadhoo
    Processing Record 109 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=juneau
    Processing Record 110 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=new norfolk
    Processing Record 111 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=illoqqortoormiut
    Processing Record 112 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=kruisfontein
    Processing Record 113 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=rio tercero
    Processing Record 114 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=port lincoln
    Processing Record 115 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=morondava
    Processing Record 116 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=lagoa
    Processing Record 117 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=lavrentiya
    Processing Record 118 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=saint-pierre
    Processing Record 119 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=ust-kuyga
    Processing Record 120 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=verona
    Processing Record 121 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=waddan
    Processing Record 122 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=quatre cocos
    Processing Record 123 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=kaitangata
    Processing Record 124 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=nanortalik
    Processing Record 125 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=opuwo
    Processing Record 126 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=lazaro cardenas
    Processing Record 127 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=ornskoldsvik
    Processing Record 128 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=tasiilaq
    Processing Record 129 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=san quintin
    Processing Record 130 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=nuuk
    Processing Record 131 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=igbo ora
    Processing Record 132 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=chuy
    Processing Record 133 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=kerch
    Processing Record 134 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=tuktoyaktuk
    Processing Record 135 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=shubarkuduk
    Processing Record 136 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=arlit
    Processing Record 137 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=te anau
    Processing Record 138 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=hami
    Processing Record 139 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=pontes e lacerda
    Processing Record 140 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=manoel urbano
    Processing Record 141 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=yulara
    Processing Record 142 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=khed brahma
    Processing Record 143 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=beneditinos
    Processing Record 144 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=belushya guba
    Processing Record 145 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=coquimbo
    Processing Record 146 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=clyde river
    Processing Record 147 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=taltal
    Processing Record 148 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=hobyo
    Processing Record 149 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=pemba
    Processing Record 150 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=muriwai beach
    Processing Record 151 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=warmbad
    Processing Record 152 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=bandarbeyla
    Processing Record 153 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=adrar
    Processing Record 154 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=pisco
    Processing Record 155 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=porto novo
    Processing Record 156 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=mahaicony
    Processing Record 157 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=petropavlovsk-kamchatskiy
    Processing Record 158 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=severnyy
    Processing Record 159 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=srinagar
    Processing Record 160 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=yagodnoye
    Processing Record 161 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=inongo
    Processing Record 162 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=shenkursk
    Processing Record 163 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=hilo
    Processing Record 164 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=katangli
    Processing Record 165 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=odweyne
    Processing Record 166 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=mahebourg
    Processing Record 167 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=nome
    Processing Record 168 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=sioux lookout
    Processing Record 169 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=meulaboh
    Processing Record 170 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=northam
    Processing Record 171 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=riyadh
    Processing Record 172 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=nichinan
    Processing Record 173 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=tagusao
    Processing Record 174 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=buraydah
    Processing Record 175 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=arraial do cabo
    Processing Record 176 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=mexico
    Processing Record 177 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=avarua
    Processing Record 178 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=talnakh
    Processing Record 179 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=saint george
    Processing Record 180 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=fukue
    Processing Record 181 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=lebu
    Processing Record 182 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=podbelsk
    Processing Record 183 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=katsuura
    Processing Record 184 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=narrabri
    Processing Record 185 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=talaya
    Processing Record 186 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=ust-charyshskaya pristan
    Processing Record 187 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=sawtell
    Processing Record 188 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=aklavik
    Processing Record 189 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=naryan-mar
    Processing Record 190 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=torbay
    Processing Record 191 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=ust-ordynskiy
    Processing Record 192 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=naze
    Processing Record 193 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=nantucket
    Processing Record 194 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=barrow
    Processing Record 195 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=jiexiu
    Processing Record 196 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=thunder bay
    Processing Record 197 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=bathsheba
    Processing Record 198 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=teahupoo
    Processing Record 199 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=verkhnevilyuysk
    Processing Record 200 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=doncaster
    Processing Record 201 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=clemencia
    Processing Record 202 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=mys shmidta
    Processing Record 203 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=vastseliina
    Processing Record 204 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=snyder
    Processing Record 205 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=bargal
    Processing Record 206 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=saint anthony
    Processing Record 207 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=grand gaube
    Processing Record 208 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=samusu
    Processing Record 209 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=cortez
    Processing Record 210 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=codrington
    Processing Record 211 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=attawapiskat
    Processing Record 212 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=bom jesus
    Processing Record 213 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=viligili
    Processing Record 214 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=nizhneyansk
    Processing Record 215 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=seoul
    Processing Record 216 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=ketchikan
    Processing Record 217 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=bengkulu
    Processing Record 218 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=phan rang
    Processing Record 219 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=birjand
    Processing Record 220 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=sorvag
    Processing Record 221 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=batesville
    Processing Record 222 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=vryburg
    Processing Record 223 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=high prairie
    Processing Record 224 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=urengoy
    Processing Record 225 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=tomatlan
    Processing Record 226 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=makung
    Processing Record 227 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=kifri
    Processing Record 228 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=mahon
    Processing Record 229 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=atasu
    Processing Record 230 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=rayong
    Processing Record 231 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=north myrtle beach
    Processing Record 232 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=lasa
    Processing Record 233 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=lapua
    Processing Record 234 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=timaru
    Processing Record 235 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=los llanos de aridane
    Processing Record 236 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=mbekenyera
    Processing Record 237 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=kuche
    Processing Record 238 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=bambous virieux
    Processing Record 239 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=lamar
    Processing Record 240 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=ancud
    Processing Record 241 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=trincomalee
    Processing Record 242 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=yaan
    Processing Record 243 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=venta
    Processing Record 244 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=kachikau
    Processing Record 245 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=kisiwani
    Processing Record 246 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=powell river
    Processing Record 247 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=san-pedro
    Processing Record 248 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=nileshwar
    Processing Record 249 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=pangkalanbuun
    Processing Record 250 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=beringovskiy
    Processing Record 251 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=minden
    Processing Record 252 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=griffith
    Processing Record 253 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=izumrud
    Processing Record 254 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=isangel
    Processing Record 255 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=rungata
    Processing Record 256 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=bac lieu
    Processing Record 257 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=saint-joseph
    Processing Record 258 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=lithakia
    Processing Record 259 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=klaksvik
    Processing Record 260 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=katobu
    Processing Record 261 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=karaul
    Processing Record 262 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=aasiaat
    Processing Record 263 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=chokurdakh
    Processing Record 264 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=vilyuysk
    Processing Record 265 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=cabo san lucas
    Processing Record 266 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=lorengau
    Processing Record 267 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=san cristobal
    Processing Record 268 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=lompoc
    Processing Record 269 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=leningradskiy
    Processing Record 270 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=airai
    Processing Record 271 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=kenai
    Processing Record 272 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=rudnaya pristan
    Processing Record 273 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=mareeba
    Processing Record 274 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=comodoro rivadavia
    Processing Record 275 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=kerouane
    Processing Record 276 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=luderitz
    Processing Record 277 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=santa rosa
    Processing Record 278 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=concepcion del oro
    Processing Record 279 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=mora
    Processing Record 280 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=creston
    Processing Record 281 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=iracoubo
    Processing Record 282 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=turukhansk
    Processing Record 283 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=vardo
    Processing Record 284 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=sosnovo
    Processing Record 285 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=ahipara
    Processing Record 286 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=shenjiamen
    Processing Record 287 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=mantua
    Processing Record 288 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=borama
    Processing Record 289 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=tsihombe
    Processing Record 290 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=manzanillo
    Processing Record 291 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=visnes
    Processing Record 292 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=ibra
    Processing Record 293 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=richards bay
    Processing Record 294 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=smithers
    Processing Record 295 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=deputatskiy
    Processing Record 296 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=plettenberg bay
    Processing Record 297 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=pacific grove
    Processing Record 298 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=aksu
    Processing Record 299 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=amderma
    Processing Record 300 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=aswan
    Processing Record 301 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=auki
    Processing Record 302 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=fortuna
    Processing Record 303 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=bhimavaram
    Processing Record 304 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=tsienyane
    Processing Record 305 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=road town
    Processing Record 306 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=cape coast
    Processing Record 307 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=port macquarie
    Processing Record 308 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=zeerust
    Processing Record 309 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=muros
    Processing Record 310 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=tarko-sale
    Processing Record 311 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=yerbogachen
    Processing Record 312 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=husavik
    Processing Record 313 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=maragogi
    Processing Record 314 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=altar
    Processing Record 315 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=vestmannaeyjar
    Processing Record 316 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=bermejillo
    Processing Record 317 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=hauterive
    Processing Record 318 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=owando
    Processing Record 319 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=maraba
    Processing Record 320 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=saldanha
    Processing Record 321 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=merke
    Processing Record 322 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=bonavista
    Processing Record 323 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=margate
    Processing Record 324 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=mehamn
    Processing Record 325 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=yumen
    Processing Record 326 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=ammon
    Processing Record 327 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=tateyama
    Processing Record 328 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=yershichi
    Processing Record 329 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=yanan
    Processing Record 330 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=fianarantsoa
    Processing Record 331 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=egvekinot
    Processing Record 332 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=karratha
    Processing Record 333 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=labuhan
    Processing Record 334 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=verkh-usugli
    Processing Record 335 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=samarai
    Processing Record 336 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=basse
    Processing Record 337 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=el faiyum
    Processing Record 338 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=alto araguaia
    Processing Record 339 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=kodiak
    Processing Record 340 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=wageningen
    Processing Record 341 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=monrovia
    Processing Record 342 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=hatton
    Processing Record 343 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=tromso
    Processing Record 344 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=lima
    Processing Record 345 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=sao filipe
    Processing Record 346 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=lira
    Processing Record 347 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=nuzvid
    Processing Record 348 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=cidreira
    Processing Record 349 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=tyup
    Processing Record 350 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=baker city
    Processing Record 351 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=teya
    Processing Record 352 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=nyandoma
    Processing Record 353 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=manokwari
    Processing Record 354 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=phrai bung
    Processing Record 355 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=teguldet
    Processing Record 356 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=solnechnyy
    Processing Record 357 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=kongolo
    Processing Record 358 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=sao joao da barra
    Processing Record 359 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=santa cruz cabralia
    Processing Record 360 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=mtimbira
    Processing Record 361 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=hay river
    Processing Record 362 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=salalah
    Processing Record 363 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=flinders
    Processing Record 364 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=zhuhai
    Processing Record 365 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=paoua
    Processing Record 366 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=cherskiy
    Processing Record 367 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=waihi beach
    Processing Record 368 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=aykhal
    Processing Record 369 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=niamey
    Processing Record 370 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=ossora
    Processing Record 371 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=sept-iles
    Processing Record 372 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=mitsamiouli
    Processing Record 373 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=poum
    Processing Record 374 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=butajira
    Processing Record 375 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=shelburne
    Processing Record 376 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=anloga
    Processing Record 377 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=dudinka
    Processing Record 378 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=saint-augustin
    Processing Record 379 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=tuatapere
    Processing Record 380 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=general roca
    Processing Record 381 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=rawson
    Processing Record 382 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=pochutla
    Processing Record 383 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=diu
    Processing Record 384 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=grand-lahou
    Processing Record 385 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=romny
    Processing Record 386 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=burgdorf
    Processing Record 387 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=ardistan
    Processing Record 388 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=praia
    Processing Record 389 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=halalo
    Processing Record 390 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=mayo
    Processing Record 391 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=esperance
    Processing Record 392 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=yefira
    Processing Record 393 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=stornoway
    Processing Record 394 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=tarnalelesz
    Processing Record 395 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=newburgh
    Processing Record 396 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=prince rupert
    Processing Record 397 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=iquique
    Processing Record 398 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=navlya
    Processing Record 399 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=marawi
    Processing Record 400 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=hacari
    Processing Record 401 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=lujan
    Processing Record 402 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=torrington
    Processing Record 403 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=pocatello
    Processing Record 404 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=nuevo progreso
    Processing Record 405 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=coihaique
    Processing Record 406 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=ambon
    Processing Record 407 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=haines junction
    Processing Record 408 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=fairbanks
    Processing Record 409 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=coruripe
    Processing Record 410 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=carutapera
    Processing Record 411 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=dingle
    Processing Record 412 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=ilanskiy
    Processing Record 413 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=erken-shakhar
    Processing Record 414 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=tahoua
    Processing Record 415 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=vostok
    Processing Record 416 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=virden
    Processing Record 417 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=russell
    Processing Record 418 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=harlow
    Processing Record 419 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=mindelo
    Processing Record 420 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=rypefjord
    Processing Record 421 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=rocha
    Processing Record 422 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=fevralsk
    Processing Record 423 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=santa maria
    Processing Record 424 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=waipawa
    Processing Record 425 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=solton
    Processing Record 426 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=mondeville
    Processing Record 427 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=faya
    Processing Record 428 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=provideniya
    Processing Record 429 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=raikot
    Processing Record 430 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=pevek
    Processing Record 431 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=longyearbyen
    Processing Record 432 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=yanam
    Processing Record 433 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=brigantine
    Processing Record 434 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=berdigestyakh
    Processing Record 435 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=constitucion
    Processing Record 436 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=waingapu
    Processing Record 437 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=skwierzyna
    Processing Record 438 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=santiago
    Processing Record 439 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=fare
    Processing Record 440 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=gunjur
    Processing Record 441 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=metro
    Processing Record 442 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=oistins
    Processing Record 443 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=sinnamary
    Processing Record 444 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=la ronge
    Processing Record 445 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=hastings
    Processing Record 446 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=santo antonio do ica
    Processing Record 447 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=plastun
    Processing Record 448 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=concepcion
    Processing Record 449 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=hasaki
    Processing Record 450 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=khingansk
    Processing Record 451 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=hofn
    Processing Record 452 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=mugur-aksy
    Processing Record 453 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=havre-saint-pierre
    Processing Record 454 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=krasnoselkup
    Processing Record 455 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=tomobe
    Processing Record 456 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=ngunguru
    Processing Record 457 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=inuvik
    Processing Record 458 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=luena
    Processing Record 459 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=biu
    Processing Record 460 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=kamaishi
    Processing Record 461 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=shache
    Processing Record 462 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=nishihara
    Processing Record 463 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=vila
    Processing Record 464 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=geraldton
    Processing Record 465 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=jujuy
    Processing Record 466 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=kargasok
    Processing Record 467 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=ariquemes
    Processing Record 468 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=bassano
    Processing Record 469 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=bolobo
    Processing Record 470 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=veraval
    Processing Record 471 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=marcona
    Processing Record 472 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=okhotsk
    Processing Record 473 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=satitoa
    Processing Record 474 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=bonthe
    Processing Record 475 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=puerto leguizamo
    Processing Record 476 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=portland
    Processing Record 477 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=mirabad
    Processing Record 478 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=saleaula
    Processing Record 479 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=cecina
    Processing Record 480 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=talcahuano
    Processing Record 481 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=marsa matruh
    Processing Record 482 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=bayangol
    Processing Record 483 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=namtsy
    Processing Record 484 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=rosemount
    Processing Record 485 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=baraya
    Processing Record 486 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=toronto
    Processing Record 487 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=catuday
    Processing Record 488 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=port keats
    Processing Record 489 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=cherepanovo
    Processing Record 490 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=envira
    Processing Record 491 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=tuggurt
    Processing Record 492 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=skjervoy
    Processing Record 493 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=smidovich
    Processing Record 494 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=alta floresta
    Processing Record 495 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=lichinga
    Processing Record 496 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=corovode
    Processing Record 497 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=astana
    Processing Record 498 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=lianran
    Processing Record 499 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=preobrazheniye
    Processing Record 500 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=chauk
    Processing Record 501 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=mnogovershinnyy
    Processing Record 502 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=bealanana
    Processing Record 503 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=ellisras
    Processing Record 504 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=dianopolis
    Processing Record 505 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=gao
    Processing Record 506 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=chern
    Processing Record 507 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=san policarpo
    Processing Record 508 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=ginir
    Processing Record 509 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=aden
    Processing Record 510 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=vanimo
    Processing Record 511 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=tumannyy
    Processing Record 512 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=gushikawa
    Processing Record 513 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=tonekabon
    Processing Record 514 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=komyshuvakha
    Processing Record 515 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=grand island
    Processing Record 516 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=carauari
    Processing Record 517 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=songea
    Processing Record 518 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=luang prabang
    Processing Record 519 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=casablanca
    Processing Record 520 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=gelgaudiskis
    Processing Record 521 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=kot diji
    Processing Record 522 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=kuandian
    Processing Record 523 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=havelock
    Processing Record 524 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=san patricio
    Processing Record 525 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=buin
    Processing Record 526 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=tonj
    Processing Record 527 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=port blair
    Processing Record 528 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=lensk
    Processing Record 529 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=morant bay
    Processing Record 530 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=manzil salim
    Processing Record 531 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=port-cartier
    Processing Record 532 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=rafai
    Processing Record 533 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=bulgan
    Processing Record 534 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=alice springs
    Processing Record 535 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=jardim
    Processing Record 536 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=biak
    Processing Record 537 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=mount isa
    Processing Record 538 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=asau
    Processing Record 539 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=aligudarz
    Processing Record 540 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=kariba
    Processing Record 541 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=belozerskoye
    Processing Record 542 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=sitka
    Processing Record 543 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=kupang
    Processing Record 544 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=zafra
    Processing Record 545 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=ilulissat
    Processing Record 546 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=bloomfield
    Processing Record 547 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=palmer
    Processing Record 548 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=port-gentil
    Processing Record 549 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=merauke
    Processing Record 550 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=kaya
    Processing Record 551 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=buala
    Processing Record 552 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=tazovskiy
    Processing Record 553 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=chagda
    Processing Record 554 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=saurimo
    Processing Record 555 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=paraiso
    Processing Record 556 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=goderich
    Processing Record 557 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=champerico
    Processing Record 558 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=skerries
    Processing Record 559 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=hojai
    Processing Record 560 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=christchurch
    Processing Record 561 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=necochea
    Processing Record 562 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=sirsilla
    Processing Record 563 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=pyapon
    Processing Record 564 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=visby
    Processing Record 565 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=conceicao do araguaia
    Processing Record 566 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=shakawe
    Processing Record 567 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=kolyvan
    Processing Record 568 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=joigny
    Processing Record 569 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=ust-tsilma
    Processing Record 570 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=fatehgarh
    Processing Record 571 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=joshimath
    Processing Record 572 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=ruwi
    Processing Record 573 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=diapaga
    Processing Record 574 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=luanda
    Processing Record 575 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=birobidzhan
    Processing Record 576 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=panzhihua
    Processing Record 577 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=hamilton
    Processing Record 578 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=luganville
    Processing Record 579 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=palabuhanratu
    Processing Record 580 of 580 http://api.openweathermap.org/data/2.5/weather?appid=ac0a8667ef38d3fbbf5db74d091358c9&units=imperial&q=cabedelo
    ----------------------------------------------------------------------------------------------------
                    Data Retrieval Complete
    ----------------------------------------------------------------------------------------------------



```python
lat_data = []
temp_data = []
city_data = []
country = []
Humi_data = []
cld_data = []
wind_data = []
long_data = []
temp_max = []
for data in weather_json:
    try:
        lat1 = data.get("coord").get("lat")
        lat_data.append(lat1)
        temp1 = data.get("main").get("temp")
        temp_data.append(temp1)
        city1 = data.get("name")
        city_data.append(city1)
        country1 = data.get("sys").get("country")
        country.append(country1)
        Humi1 = data.get("main").get("humidity")
        Humi_data.append(Humi1)
        cld1 = data.get("clouds").get("all")
        cld_data.append(cld1)
        wind1 = data.get("wind").get("speed")
        wind_data.append(wind1)
        long1 = data.get("coord").get("lon")
        long_data.append(long1)
        temp1 = data.get("main").get("temp_max")
        temp_max.append(temp1)

    except:
        pass

    continue

weather_dict = {"Temperature (F)": temp_data, "Latitude": lat_data, "Longitude":long_data, "city":city_data, "Country":country,
                "Humidity": Humi_data, "Cloudiness":cld_data,"Wind Speed":wind_data, "Max_Temp":temp_max}
weather_df = pd.DataFrame(weather_dict)
weather_df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Cloudiness</th>
      <th>Country</th>
      <th>Humidity</th>
      <th>Latitude</th>
      <th>Longitude</th>
      <th>Max_Temp</th>
      <th>Temperature (F)</th>
      <th>Wind Speed</th>
      <th>city</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>AU</td>
      <td>77</td>
      <td>-32.72</td>
      <td>152.14</td>
      <td>66.20</td>
      <td>66.20</td>
      <td>5.82</td>
      <td>Nelson Bay</td>
    </tr>
    <tr>
      <th>1</th>
      <td>0</td>
      <td>ZA</td>
      <td>48</td>
      <td>-30.97</td>
      <td>22.13</td>
      <td>54.51</td>
      <td>54.51</td>
      <td>2.48</td>
      <td>Carnarvon</td>
    </tr>
    <tr>
      <th>2</th>
      <td>20</td>
      <td>CA</td>
      <td>67</td>
      <td>62.45</td>
      <td>-114.38</td>
      <td>17.60</td>
      <td>17.60</td>
      <td>6.93</td>
      <td>Yellowknife</td>
    </tr>
    <tr>
      <th>3</th>
      <td>76</td>
      <td>ZA</td>
      <td>92</td>
      <td>-33.59</td>
      <td>26.89</td>
      <td>65.76</td>
      <td>65.76</td>
      <td>6.73</td>
      <td>Port Alfred</td>
    </tr>
    <tr>
      <th>4</th>
      <td>64</td>
      <td>AU</td>
      <td>97</td>
      <td>-23.58</td>
      <td>149.07</td>
      <td>78.45</td>
      <td>78.45</td>
      <td>12.44</td>
      <td>Bluff</td>
    </tr>
    <tr>
      <th>5</th>
      <td>0</td>
      <td>ZA</td>
      <td>96</td>
      <td>-34.42</td>
      <td>19.24</td>
      <td>51.00</td>
      <td>51.00</td>
      <td>3.71</td>
      <td>Hermanus</td>
    </tr>
    <tr>
      <th>6</th>
      <td>48</td>
      <td>RU</td>
      <td>100</td>
      <td>50.68</td>
      <td>156.12</td>
      <td>24.95</td>
      <td>24.95</td>
      <td>9.31</td>
      <td>Severo-Kurilsk</td>
    </tr>
    <tr>
      <th>7</th>
      <td>0</td>
      <td>ZA</td>
      <td>92</td>
      <td>-33.93</td>
      <td>18.42</td>
      <td>62.75</td>
      <td>62.75</td>
      <td>16.24</td>
      <td>Cape Town</td>
    </tr>
    <tr>
      <th>8</th>
      <td>64</td>
      <td>GL</td>
      <td>88</td>
      <td>77.48</td>
      <td>-69.36</td>
      <td>8.12</td>
      <td>8.12</td>
      <td>10.20</td>
      <td>Qaanaaq</td>
    </tr>
    <tr>
      <th>9</th>
      <td>0</td>
      <td>NZ</td>
      <td>80</td>
      <td>-46.19</td>
      <td>168.86</td>
      <td>68.37</td>
      <td>68.37</td>
      <td>4.61</td>
      <td>Mataura</td>
    </tr>
    <tr>
      <th>10</th>
      <td>44</td>
      <td>AR</td>
      <td>100</td>
      <td>-24.79</td>
      <td>-65.41</td>
      <td>56.94</td>
      <td>56.94</td>
      <td>2.48</td>
      <td>Salta</td>
    </tr>
    <tr>
      <th>11</th>
      <td>92</td>
      <td>PG</td>
      <td>100</td>
      <td>-5.46</td>
      <td>143.15</td>
      <td>54.20</td>
      <td>54.20</td>
      <td>2.59</td>
      <td>Porgera</td>
    </tr>
    <tr>
      <th>12</th>
      <td>90</td>
      <td>US</td>
      <td>69</td>
      <td>22.08</td>
      <td>-159.32</td>
      <td>77.00</td>
      <td>74.70</td>
      <td>13.87</td>
      <td>Kapaa</td>
    </tr>
    <tr>
      <th>13</th>
      <td>8</td>
      <td>IN</td>
      <td>76</td>
      <td>21.34</td>
      <td>72.75</td>
      <td>76.56</td>
      <td>76.56</td>
      <td>5.95</td>
      <td>Olpad</td>
    </tr>
    <tr>
      <th>14</th>
      <td>90</td>
      <td>CA</td>
      <td>75</td>
      <td>50.70</td>
      <td>-127.42</td>
      <td>42.80</td>
      <td>42.80</td>
      <td>11.41</td>
      <td>Port Hardy</td>
    </tr>
    <tr>
      <th>15</th>
      <td>90</td>
      <td>CA</td>
      <td>54</td>
      <td>66.15</td>
      <td>-65.72</td>
      <td>28.40</td>
      <td>28.40</td>
      <td>21.92</td>
      <td>Pangnirtung</td>
    </tr>
    <tr>
      <th>16</th>
      <td>0</td>
      <td>BR</td>
      <td>87</td>
      <td>-2.92</td>
      <td>-39.92</td>
      <td>76.34</td>
      <td>76.34</td>
      <td>9.75</td>
      <td>Itarema</td>
    </tr>
    <tr>
      <th>17</th>
      <td>92</td>
      <td>AR</td>
      <td>100</td>
      <td>-54.81</td>
      <td>-68.31</td>
      <td>42.14</td>
      <td>42.14</td>
      <td>11.43</td>
      <td>Ushuaia</td>
    </tr>
    <tr>
      <th>18</th>
      <td>92</td>
      <td>PF</td>
      <td>100</td>
      <td>-9.80</td>
      <td>-139.03</td>
      <td>81.02</td>
      <td>81.02</td>
      <td>13.33</td>
      <td>Atuona</td>
    </tr>
    <tr>
      <th>19</th>
      <td>90</td>
      <td>MX</td>
      <td>93</td>
      <td>27.52</td>
      <td>-110.01</td>
      <td>57.20</td>
      <td>57.20</td>
      <td>8.05</td>
      <td>Laguna</td>
    </tr>
    <tr>
      <th>20</th>
      <td>32</td>
      <td>CL</td>
      <td>87</td>
      <td>-42.48</td>
      <td>-73.76</td>
      <td>59.01</td>
      <td>59.01</td>
      <td>2.82</td>
      <td>Castro</td>
    </tr>
    <tr>
      <th>21</th>
      <td>0</td>
      <td>RU</td>
      <td>64</td>
      <td>59.70</td>
      <td>30.79</td>
      <td>-0.41</td>
      <td>-0.41</td>
      <td>11.18</td>
      <td>Nikolskoye</td>
    </tr>
    <tr>
      <th>22</th>
      <td>80</td>
      <td>BR</td>
      <td>97</td>
      <td>-20.63</td>
      <td>-46.00</td>
      <td>67.38</td>
      <td>67.38</td>
      <td>3.04</td>
      <td>Ponta do Sol</td>
    </tr>
    <tr>
      <th>23</th>
      <td>1</td>
      <td>US</td>
      <td>78</td>
      <td>60.79</td>
      <td>-161.76</td>
      <td>17.60</td>
      <td>17.60</td>
      <td>21.92</td>
      <td>Bethel</td>
    </tr>
    <tr>
      <th>24</th>
      <td>40</td>
      <td>NO</td>
      <td>86</td>
      <td>70.86</td>
      <td>29.09</td>
      <td>30.20</td>
      <td>27.14</td>
      <td>34.45</td>
      <td>Berlevag</td>
    </tr>
    <tr>
      <th>25</th>
      <td>20</td>
      <td>GL</td>
      <td>42</td>
      <td>60.91</td>
      <td>-46.05</td>
      <td>6.80</td>
      <td>6.80</td>
      <td>4.70</td>
      <td>Narsaq</td>
    </tr>
    <tr>
      <th>26</th>
      <td>100</td>
      <td>KI</td>
      <td>97</td>
      <td>3.07</td>
      <td>172.79</td>
      <td>83.94</td>
      <td>83.94</td>
      <td>17.47</td>
      <td>Butaritari</td>
    </tr>
    <tr>
      <th>27</th>
      <td>20</td>
      <td>RU</td>
      <td>73</td>
      <td>53.19</td>
      <td>44.05</td>
      <td>-6.33</td>
      <td>-6.33</td>
      <td>9.42</td>
      <td>Kamenka</td>
    </tr>
    <tr>
      <th>28</th>
      <td>80</td>
      <td>PF</td>
      <td>100</td>
      <td>-23.12</td>
      <td>-134.97</td>
      <td>80.97</td>
      <td>80.97</td>
      <td>13.78</td>
      <td>Rikitea</td>
    </tr>
    <tr>
      <th>29</th>
      <td>24</td>
      <td>ZA</td>
      <td>95</td>
      <td>-28.55</td>
      <td>16.43</td>
      <td>62.84</td>
      <td>62.84</td>
      <td>11.77</td>
      <td>Oranjemund</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>494</th>
      <td>80</td>
      <td>GA</td>
      <td>100</td>
      <td>-0.72</td>
      <td>8.78</td>
      <td>77.42</td>
      <td>77.42</td>
      <td>3.83</td>
      <td>Port-Gentil</td>
    </tr>
    <tr>
      <th>495</th>
      <td>80</td>
      <td>ID</td>
      <td>100</td>
      <td>-8.49</td>
      <td>140.40</td>
      <td>79.26</td>
      <td>79.26</td>
      <td>6.06</td>
      <td>Merauke</td>
    </tr>
    <tr>
      <th>496</th>
      <td>24</td>
      <td>SB</td>
      <td>78</td>
      <td>-8.15</td>
      <td>159.59</td>
      <td>87.90</td>
      <td>87.90</td>
      <td>3.04</td>
      <td>Buala</td>
    </tr>
    <tr>
      <th>497</th>
      <td>0</td>
      <td>RU</td>
      <td>65</td>
      <td>67.47</td>
      <td>78.70</td>
      <td>-34.59</td>
      <td>-34.59</td>
      <td>5.95</td>
      <td>Tazovskiy</td>
    </tr>
    <tr>
      <th>498</th>
      <td>88</td>
      <td>AO</td>
      <td>99</td>
      <td>-9.66</td>
      <td>20.40</td>
      <td>65.45</td>
      <td>65.45</td>
      <td>2.71</td>
      <td>Saurimo</td>
    </tr>
    <tr>
      <th>499</th>
      <td>75</td>
      <td>MX</td>
      <td>23</td>
      <td>24.01</td>
      <td>-104.61</td>
      <td>75.20</td>
      <td>75.20</td>
      <td>18.34</td>
      <td>Paraiso</td>
    </tr>
    <tr>
      <th>500</th>
      <td>20</td>
      <td>CA</td>
      <td>70</td>
      <td>43.74</td>
      <td>-81.71</td>
      <td>44.16</td>
      <td>44.16</td>
      <td>17.47</td>
      <td>Goderich</td>
    </tr>
    <tr>
      <th>501</th>
      <td>0</td>
      <td>MX</td>
      <td>38</td>
      <td>16.38</td>
      <td>-93.60</td>
      <td>82.50</td>
      <td>82.50</td>
      <td>1.48</td>
      <td>Champerico</td>
    </tr>
    <tr>
      <th>502</th>
      <td>75</td>
      <td>IE</td>
      <td>86</td>
      <td>53.58</td>
      <td>-6.11</td>
      <td>30.20</td>
      <td>30.20</td>
      <td>18.34</td>
      <td>Skerries</td>
    </tr>
    <tr>
      <th>503</th>
      <td>12</td>
      <td>IN</td>
      <td>92</td>
      <td>26.00</td>
      <td>92.85</td>
      <td>58.65</td>
      <td>58.65</td>
      <td>1.36</td>
      <td>Hojai</td>
    </tr>
    <tr>
      <th>504</th>
      <td>68</td>
      <td>NZ</td>
      <td>82</td>
      <td>-43.53</td>
      <td>172.64</td>
      <td>62.60</td>
      <td>62.60</td>
      <td>8.05</td>
      <td>Christchurch</td>
    </tr>
    <tr>
      <th>505</th>
      <td>64</td>
      <td>AR</td>
      <td>83</td>
      <td>-38.55</td>
      <td>-58.74</td>
      <td>68.19</td>
      <td>68.19</td>
      <td>2.37</td>
      <td>Necochea</td>
    </tr>
    <tr>
      <th>506</th>
      <td>0</td>
      <td>IN</td>
      <td>63</td>
      <td>18.39</td>
      <td>78.81</td>
      <td>61.17</td>
      <td>61.17</td>
      <td>3.15</td>
      <td>Sirsilla</td>
    </tr>
    <tr>
      <th>507</th>
      <td>0</td>
      <td>MM</td>
      <td>100</td>
      <td>16.29</td>
      <td>95.68</td>
      <td>68.91</td>
      <td>68.91</td>
      <td>4.72</td>
      <td>Pyapon</td>
    </tr>
    <tr>
      <th>508</th>
      <td>48</td>
      <td>SE</td>
      <td>100</td>
      <td>57.64</td>
      <td>18.30</td>
      <td>19.05</td>
      <td>19.05</td>
      <td>21.39</td>
      <td>Visby</td>
    </tr>
    <tr>
      <th>509</th>
      <td>12</td>
      <td>BR</td>
      <td>92</td>
      <td>-8.26</td>
      <td>-49.26</td>
      <td>76.79</td>
      <td>76.79</td>
      <td>4.38</td>
      <td>Conceicao do Araguaia</td>
    </tr>
    <tr>
      <th>510</th>
      <td>92</td>
      <td>BW</td>
      <td>96</td>
      <td>-18.36</td>
      <td>21.84</td>
      <td>66.57</td>
      <td>66.57</td>
      <td>9.98</td>
      <td>Shakawe</td>
    </tr>
    <tr>
      <th>511</th>
      <td>56</td>
      <td>RU</td>
      <td>75</td>
      <td>55.31</td>
      <td>82.74</td>
      <td>-18.41</td>
      <td>-18.41</td>
      <td>2.24</td>
      <td>Kolyvan</td>
    </tr>
    <tr>
      <th>512</th>
      <td>0</td>
      <td>FR</td>
      <td>57</td>
      <td>47.98</td>
      <td>3.40</td>
      <td>19.40</td>
      <td>19.40</td>
      <td>6.93</td>
      <td>Joigny</td>
    </tr>
    <tr>
      <th>513</th>
      <td>80</td>
      <td>RU</td>
      <td>85</td>
      <td>65.44</td>
      <td>52.15</td>
      <td>14.60</td>
      <td>14.60</td>
      <td>5.73</td>
      <td>Ust-Tsilma</td>
    </tr>
    <tr>
      <th>514</th>
      <td>0</td>
      <td>IN</td>
      <td>89</td>
      <td>27.36</td>
      <td>79.63</td>
      <td>61.49</td>
      <td>61.49</td>
      <td>2.82</td>
      <td>Fatehgarh</td>
    </tr>
    <tr>
      <th>515</th>
      <td>0</td>
      <td>IN</td>
      <td>100</td>
      <td>30.57</td>
      <td>79.57</td>
      <td>4.92</td>
      <td>4.92</td>
      <td>0.47</td>
      <td>Joshimath</td>
    </tr>
    <tr>
      <th>516</th>
      <td>44</td>
      <td>OM</td>
      <td>100</td>
      <td>23.60</td>
      <td>58.55</td>
      <td>69.45</td>
      <td>69.45</td>
      <td>0.92</td>
      <td>Ruwi</td>
    </tr>
    <tr>
      <th>517</th>
      <td>56</td>
      <td>BF</td>
      <td>27</td>
      <td>12.07</td>
      <td>1.79</td>
      <td>83.90</td>
      <td>83.90</td>
      <td>10.76</td>
      <td>Diapaga</td>
    </tr>
    <tr>
      <th>518</th>
      <td>76</td>
      <td>AO</td>
      <td>100</td>
      <td>-8.83</td>
      <td>13.24</td>
      <td>74.00</td>
      <td>74.00</td>
      <td>4.61</td>
      <td>Luanda</td>
    </tr>
    <tr>
      <th>519</th>
      <td>0</td>
      <td>RU</td>
      <td>62</td>
      <td>48.79</td>
      <td>132.93</td>
      <td>0.96</td>
      <td>0.96</td>
      <td>3.49</td>
      <td>Birobidzhan</td>
    </tr>
    <tr>
      <th>520</th>
      <td>0</td>
      <td>CN</td>
      <td>73</td>
      <td>26.59</td>
      <td>101.72</td>
      <td>38.27</td>
      <td>38.27</td>
      <td>1.92</td>
      <td>Panzhihua</td>
    </tr>
    <tr>
      <th>521</th>
      <td>75</td>
      <td>BM</td>
      <td>72</td>
      <td>32.30</td>
      <td>-64.78</td>
      <td>64.40</td>
      <td>64.40</td>
      <td>21.92</td>
      <td>Hamilton</td>
    </tr>
    <tr>
      <th>522</th>
      <td>0</td>
      <td>VU</td>
      <td>99</td>
      <td>-15.51</td>
      <td>167.18</td>
      <td>84.48</td>
      <td>84.48</td>
      <td>7.74</td>
      <td>Luganville</td>
    </tr>
    <tr>
      <th>523</th>
      <td>88</td>
      <td>BR</td>
      <td>95</td>
      <td>-6.97</td>
      <td>-34.84</td>
      <td>80.57</td>
      <td>80.57</td>
      <td>12.55</td>
      <td>Cabedelo</td>
    </tr>
  </tbody>
</table>
<p>524 rows × 9 columns</p>
</div>




```python
weather_df.count()
```




    Cloudiness         524
    Country            524
    Humidity           524
    Latitude           524
    Longitude          524
    Max_Temp           524
    Temperature (F)    524
    Wind Speed         524
    city               524
    dtype: int64




```python
weather_df.to_csv("my_weather.csv",encoding="utf-8",index=False)
```

### Temperature (F) vs. Latitude


```python
plt.scatter(weather_df["Latitude"], 
            weather_df["Max_Temp"], c="gold", 
            edgecolor="black", linewidths=1, marker="o", 
            alpha=0.8, label="Temp")

# Incorporate the other graph properties
plt.title("City Max Temperature vs. Latitude (02/24/2018)")
plt.ylabel("Max Temperature (F)")
plt.xlabel("Latitude")
plt.xlim((-90,90))
plt.grid(True)
sns.set()
plt.savefig("Temperature (F) vs. Latitude.png")
plt.show()
```


![png](output_11_0.png)


### Humidity (%) vs. Latitude


```python
plt.scatter(weather_df["Latitude"], 
            weather_df["Humidity"], c="blue", 
            edgecolor="black", linewidths=1, marker="o", 
            alpha=0.8, label="Humidity")

# Incorporate the other graph properties
plt.title("City Humidity vs. Latitude (02/24/2018)")
plt.ylabel("Humidity (%)")
plt.xlabel("Latitude")
plt.xlim((-90,90))
plt.grid(True)
sns.set()
plt.savefig("Humidity (%) vs. Latitude.png")
plt.show()
```


![png](output_13_0.png)


### Cloudiness (%) vs. Latitude


```python
plt.scatter(weather_df["Latitude"], 
            weather_df["Cloudiness"], c="green", 
            edgecolor="black", linewidths=1, marker="o", 
            alpha=0.8, label="Cloudiness")

# Incorporate the other graph properties
plt.title("City Cloudiness vs. Latitude (02/24/2018)")
plt.ylabel("Cloudiness (%)")
plt.xlabel("Latitude")
plt.xlim((-90,90))
plt.grid(True)
sns.set()
plt.savefig("Cloudiness (%) vs. Latitude.png")
plt.show()
```


![png](output_15_0.png)


### Wind Speed (mph) vs. Latitude


```python
plt.scatter(weather_df["Latitude"], 
            weather_df["Wind Speed"], c="red", 
            edgecolor="black", linewidths=1, marker="o", 
            alpha=0.8, label="wind speed")

# Incorporate the other graph properties
plt.title("City Wind Speed vs. Latitude (02/24/2018)")
plt.ylabel("Wind Speed (MPH)")
plt.xlabel("Latitude")
plt.xlim((-90,90))
plt.grid(True)
sns.set()
plt.savefig("Wind Speed (MPH) vs. Latitude.png")
plt.show()
```


![png](output_17_0.png)

