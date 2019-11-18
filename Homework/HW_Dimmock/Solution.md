# WeatherPy

- - -

## Analysis

* As expected, the weather becomes significantly warmer as one approaches the equator (0 Deg. Latitude). More interestingly, however, is the fact that the southern hemisphere tends to be warmer this time of year than the northern hemisphere. This may be due to the tilt of the earth.
* There is no strong relationship between latitude and cloudiness, however, it is interesting to see that a strong band of cities sits at 0, 80, and 100% cloudiness.
* There is no strong relationship between latitude and wind speed, however in northern hemispheres there is a flurry of cities with over 20 mph of wind.

```python
# Dependencies and Setup
import matplotlib.pyplot as plt
import pandas as pd
import numpy as np
import requests
import time
import urllib

# Import API key
api_key = "fac24ee030b2a4a4d846167e98ff19cb"

# Incorporated citipy to determine city based on latitude and longitude
from citipy import citipy

# Output File (CSV)
output_data_file = "output_data/cities.csv"

# Range of latitudes and longitudes
lat_range = (-90, 90)
lng_range = (-180, 180)
```

## Generate Cities List

```python
# List for holding lat_lngs and cities
lat_lngs = []
cities = []

# Create a set of random lat and lng combinations
lats = np.random.uniform(low=-90.000, high=90.000, size=1500)
lngs = np.random.uniform(low=-180.000, high=180.000, size=1500)
lat_lngs = zip(lats, lngs)

# Identify nearest city for each lat, lng combination
for lat_lng in lat_lngs:
    city = citipy.nearest_city(lat_lng[0], lat_lng[1]).city_name

    # If the city is unique, then add it to a our cities list
    if city not in cities:
        cities.append(city)

# Print the city count to confirm sufficient count
len(cities)
    620
```

## Perform API Calls
import urllib

def getWeather(city, api_key):
    
    #Convert spaces in city names to %20
 city = urllib.quote(city)
 print(api_key)
    # Query the url to get the result
 response = requests.get('https://api.openweathermap.org/data/2.5/weather', params={'q': city, 'appid': api_key},)
    
 if response.status_code == 200:
        return response.text
    else:
        return None

print(getWeather(city="riyadh", api_key=api_key))


fac24ee030b2a4a4d846167e98ff19cb
{"coord":{"lon":46.72,"lat":24.63},"weather":[{"id":800,"main":"Clear","description":"clear sky","icon":"01d"}],"base":"stations","main":{"temp":299.15,"pressure":1011,"humidity":27,"temp_min":299.15,"temp_max":299.15},"visibility":10000,"wind":{"speed":1.16,"deg":164.339},"clouds":{"all":0},"dt":1568776408,"sys":{"type":1,"id":7424,"message":0.0063,"country":"SA","sunrise":1568774410,"sunset":1568818496},"timezone":10800,"id":108410,"name":"Riyadh","cod":200}


import time
# Create an array to store the output
output = []
cities_that_errored_out = []
# Write a for loop to iterate through the cities array 
for city in cities:
    # Call the getWeather function for each city in the cities array
    try:
        result = getWeather(city=city, api_key=api_key)
        # If the function returns something:
        print(city)
        if result:
            output.append(result)
    except:
        cities_that_errored_out.append(city)
        pass
    # Wait one second before going to the next call
    time.sleep(1)

fac24ee030b2a4a4d846167e98ff19cb
riyadh
fac24ee030b2a4a4d846167e98ff19cb
jamestown
fac24ee030b2a4a4d846167e98ff19cb
toliary
fac24ee030b2a4a4d846167e98ff19cb
goundam
fac24ee030b2a4a4d846167e98ff19cb
punta arenas
fac24ee030b2a4a4d846167e98ff19cb
tiksi
fac24ee030b2a4a4d846167e98ff19cb
bourail
fac24ee030b2a4a4d846167e98ff19cb
eucaliptus
fac24ee030b2a4a4d846167e98ff19cb
kapaa
fac24ee030b2a4a4d846167e98ff19cb
port elizabeth
fac24ee030b2a4a4d846167e98ff19cb
georgetown
fac24ee030b2a4a4d846167e98ff19cb
albany
fac24ee030b2a4a4d846167e98ff19cb
chokurdakh
fac24ee030b2a4a4d846167e98ff19cb
te anau
fac24ee030b2a4a4d846167e98ff19cb
ushuaia
fac24ee030b2a4a4d846167e98ff19cb
saskylakh
fac24ee030b2a4a4d846167e98ff19cb
namatanai
fac24ee030b2a4a4d846167e98ff19cb
castro
fac24ee030b2a4a4d846167e98ff19cb
falealupo
fac24ee030b2a4a4d846167e98ff19cb
saint-philippe
fac24ee030b2a4a4d846167e98ff19cb
hilo
fac24ee030b2a4a4d846167e98ff19cb
yorkton
fac24ee030b2a4a4d846167e98ff19cb
jumla
fac24ee030b2a4a4d846167e98ff19cb
saint george
fac24ee030b2a4a4d846167e98ff19cb
yellowknife
fac24ee030b2a4a4d846167e98ff19cb
avarua
fac24ee030b2a4a4d846167e98ff19cb
dogondoutchi
fac24ee030b2a4a4d846167e98ff19cb
sioux lookout
fac24ee030b2a4a4d846167e98ff19cb
riohacha
fac24ee030b2a4a4d846167e98ff19cb
kouroussa
fac24ee030b2a4a4d846167e98ff19cb
atuona
fac24ee030b2a4a4d846167e98ff19cb
sentyabrskiy
fac24ee030b2a4a4d846167e98ff19cb
oistins
fac24ee030b2a4a4d846167e98ff19cb
faanui
fac24ee030b2a4a4d846167e98ff19cb
acarau
fac24ee030b2a4a4d846167e98ff19cb
bluff
fac24ee030b2a4a4d846167e98ff19cb
cabo san lucas
fac24ee030b2a4a4d846167e98ff19cb
barentsburg
fac24ee030b2a4a4d846167e98ff19cb
rabo de peixe
fac24ee030b2a4a4d846167e98ff19cb
rikitea
fac24ee030b2a4a4d846167e98ff19cb
hithadhoo
fac24ee030b2a4a4d846167e98ff19cb
cidreira
fac24ee030b2a4a4d846167e98ff19cb
meyungs
fac24ee030b2a4a4d846167e98ff19cb
illoqqortoormiut
fac24ee030b2a4a4d846167e98ff19cb
busselton
fac24ee030b2a4a4d846167e98ff19cb
nome
fac24ee030b2a4a4d846167e98ff19cb
cape town
fac24ee030b2a4a4d846167e98ff19cb
jalu
fac24ee030b2a4a4d846167e98ff19cb
mataura
fac24ee030b2a4a4d846167e98ff19cb
airai
fac24ee030b2a4a4d846167e98ff19cb
hirtshals
fac24ee030b2a4a4d846167e98ff19cb
grindavik
fac24ee030b2a4a4d846167e98ff19cb
hirara
fac24ee030b2a4a4d846167e98ff19cb
victoria
fac24ee030b2a4a4d846167e98ff19cb
erenhot
fac24ee030b2a4a4d846167e98ff19cb
havoysund
fac24ee030b2a4a4d846167e98ff19cb
husavik
fac24ee030b2a4a4d846167e98ff19cb
ponta do sol
fac24ee030b2a4a4d846167e98ff19cb
severo-kurilsk
fac24ee030b2a4a4d846167e98ff19cb
puerto ayora
fac24ee030b2a4a4d846167e98ff19cb
saleaula
fac24ee030b2a4a4d846167e98ff19cb
mazagao
fac24ee030b2a4a4d846167e98ff19cb
karratha
fac24ee030b2a4a4d846167e98ff19cb
kahului
fac24ee030b2a4a4d846167e98ff19cb
taolanaro
fac24ee030b2a4a4d846167e98ff19cb
kiunga
fac24ee030b2a4a4d846167e98ff19cb
ribeira grande
fac24ee030b2a4a4d846167e98ff19cb
ilulissat
fac24ee030b2a4a4d846167e98ff19cb
kampot
fac24ee030b2a4a4d846167e98ff19cb
faya
fac24ee030b2a4a4d846167e98ff19cb
clyde river
fac24ee030b2a4a4d846167e98ff19cb
college
fac24ee030b2a4a4d846167e98ff19cb
tsihombe
fac24ee030b2a4a4d846167e98ff19cb
nisia floresta
fac24ee030b2a4a4d846167e98ff19cb
butaritari
fac24ee030b2a4a4d846167e98ff19cb
topolevo
fac24ee030b2a4a4d846167e98ff19cb
bowen
fac24ee030b2a4a4d846167e98ff19cb
rio gallegos
fac24ee030b2a4a4d846167e98ff19cb
avera
fac24ee030b2a4a4d846167e98ff19cb
jacareacanga
fac24ee030b2a4a4d846167e98ff19cb
barrow
fac24ee030b2a4a4d846167e98ff19cb
touros
fac24ee030b2a4a4d846167e98ff19cb
mar del plata
fac24ee030b2a4a4d846167e98ff19cb
novska
fac24ee030b2a4a4d846167e98ff19cb
great yarmouth
fac24ee030b2a4a4d846167e98ff19cb
manta
fac24ee030b2a4a4d846167e98ff19cb
port alfred
fac24ee030b2a4a4d846167e98ff19cb
pacific grove
fac24ee030b2a4a4d846167e98ff19cb
vaini
fac24ee030b2a4a4d846167e98ff19cb
panalingaan
fac24ee030b2a4a4d846167e98ff19cb
norman wells
fac24ee030b2a4a4d846167e98ff19cb
nalut
fac24ee030b2a4a4d846167e98ff19cb
del gallego
fac24ee030b2a4a4d846167e98ff19cb
villarrica
fac24ee030b2a4a4d846167e98ff19cb
nuevo imperial
fac24ee030b2a4a4d846167e98ff19cb
new norfolk
fac24ee030b2a4a4d846167e98ff19cb
hualmay
fac24ee030b2a4a4d846167e98ff19cb
key largo
fac24ee030b2a4a4d846167e98ff19cb
hermanus
fac24ee030b2a4a4d846167e98ff19cb
vallenar
fac24ee030b2a4a4d846167e98ff19cb
attawapiskat
fac24ee030b2a4a4d846167e98ff19cb
saldanha
fac24ee030b2a4a4d846167e98ff19cb
naze
fac24ee030b2a4a4d846167e98ff19cb
tuktoyaktuk
fac24ee030b2a4a4d846167e98ff19cb
barcelos
fac24ee030b2a4a4d846167e98ff19cb
klaksvik
fac24ee030b2a4a4d846167e98ff19cb
ust-tsilma
fac24ee030b2a4a4d846167e98ff19cb
flinders
fac24ee030b2a4a4d846167e98ff19cb
santa cruz de tenerife
fac24ee030b2a4a4d846167e98ff19cb
pringsewu
fac24ee030b2a4a4d846167e98ff19cb
khatanga
fac24ee030b2a4a4d846167e98ff19cb
kargil
fac24ee030b2a4a4d846167e98ff19cb
visnes
fac24ee030b2a4a4d846167e98ff19cb
cururupu
fac24ee030b2a4a4d846167e98ff19cb
ngama
fac24ee030b2a4a4d846167e98ff19cb
imbituba
fac24ee030b2a4a4d846167e98ff19cb
lompoc
fac24ee030b2a4a4d846167e98ff19cb
guaymas
fac24ee030b2a4a4d846167e98ff19cb
provideniya
fac24ee030b2a4a4d846167e98ff19cb
nouadhibou
fac24ee030b2a4a4d846167e98ff19cb
saint-denis
fac24ee030b2a4a4d846167e98ff19cb
upata
fac24ee030b2a4a4d846167e98ff19cb
mys shmidta
fac24ee030b2a4a4d846167e98ff19cb
grand gaube
fac24ee030b2a4a4d846167e98ff19cb
haifa
fac24ee030b2a4a4d846167e98ff19cb
bredasdorp
fac24ee030b2a4a4d846167e98ff19cb
bargal
fac24ee030b2a4a4d846167e98ff19cb
kaitangata
fac24ee030b2a4a4d846167e98ff19cb
tawzar
fac24ee030b2a4a4d846167e98ff19cb
vangaindrano
fac24ee030b2a4a4d846167e98ff19cb
nanortalik
fac24ee030b2a4a4d846167e98ff19cb
marsa matruh
fac24ee030b2a4a4d846167e98ff19cb
souillac
fac24ee030b2a4a4d846167e98ff19cb
las vegas
fac24ee030b2a4a4d846167e98ff19cb
kodiak
fac24ee030b2a4a4d846167e98ff19cb
isangel
fac24ee030b2a4a4d846167e98ff19cb
mwense
fac24ee030b2a4a4d846167e98ff19cb
port lincoln
fac24ee030b2a4a4d846167e98ff19cb
estacion coahuila
fac24ee030b2a4a4d846167e98ff19cb
pisco
fac24ee030b2a4a4d846167e98ff19cb
tuatapere
fac24ee030b2a4a4d846167e98ff19cb
andevoranto
fac24ee030b2a4a4d846167e98ff19cb
tasiilaq
fac24ee030b2a4a4d846167e98ff19cb
bethel
fac24ee030b2a4a4d846167e98ff19cb
sabha
fac24ee030b2a4a4d846167e98ff19cb
carnarvon
fac24ee030b2a4a4d846167e98ff19cb
shkotovo-26
fac24ee030b2a4a4d846167e98ff19cb
vostok
fac24ee030b2a4a4d846167e98ff19cb
qaanaaq
fac24ee030b2a4a4d846167e98ff19cb
aloleng
fac24ee030b2a4a4d846167e98ff19cb
chuy
fac24ee030b2a4a4d846167e98ff19cb
dasoguz
fac24ee030b2a4a4d846167e98ff19cb
esperance
fac24ee030b2a4a4d846167e98ff19cb
narsaq
fac24ee030b2a4a4d846167e98ff19cb
borama
fac24ee030b2a4a4d846167e98ff19cb
la suiza
fac24ee030b2a4a4d846167e98ff19cb
salina
fac24ee030b2a4a4d846167e98ff19cb
rio negrinho
fac24ee030b2a4a4d846167e98ff19cb
honggang
fac24ee030b2a4a4d846167e98ff19cb
lucapa
fac24ee030b2a4a4d846167e98ff19cb
moranbah
fac24ee030b2a4a4d846167e98ff19cb
yanchukan
fac24ee030b2a4a4d846167e98ff19cb
oktyabrskiy
fac24ee030b2a4a4d846167e98ff19cb
zlatoustovsk
fac24ee030b2a4a4d846167e98ff19cb
vernon
fac24ee030b2a4a4d846167e98ff19cb
mahebourg
fac24ee030b2a4a4d846167e98ff19cb
hobart
fac24ee030b2a4a4d846167e98ff19cb
asau
fac24ee030b2a4a4d846167e98ff19cb
amderma
fac24ee030b2a4a4d846167e98ff19cb
sofiysk
fac24ee030b2a4a4d846167e98ff19cb
samusu
fac24ee030b2a4a4d846167e98ff19cb
katsuura
fac24ee030b2a4a4d846167e98ff19cb
camopi
fac24ee030b2a4a4d846167e98ff19cb
srednekolymsk
fac24ee030b2a4a4d846167e98ff19cb
bayir
fac24ee030b2a4a4d846167e98ff19cb
tidore
fac24ee030b2a4a4d846167e98ff19cb
bathsheba
fac24ee030b2a4a4d846167e98ff19cb
luderitz
fac24ee030b2a4a4d846167e98ff19cb
cap malheureux
fac24ee030b2a4a4d846167e98ff19cb
slavutych
fac24ee030b2a4a4d846167e98ff19cb
naron
fac24ee030b2a4a4d846167e98ff19cb
nandu
fac24ee030b2a4a4d846167e98ff19cb
baker city
fac24ee030b2a4a4d846167e98ff19cb
bambous virieux
fac24ee030b2a4a4d846167e98ff19cb
koulamoutou
fac24ee030b2a4a4d846167e98ff19cb
hasaki
fac24ee030b2a4a4d846167e98ff19cb
toora-khem
fac24ee030b2a4a4d846167e98ff19cb
requena
fac24ee030b2a4a4d846167e98ff19cb
boende
fac24ee030b2a4a4d846167e98ff19cb
athens
fac24ee030b2a4a4d846167e98ff19cb
north bend
fac24ee030b2a4a4d846167e98ff19cb
malartic
fac24ee030b2a4a4d846167e98ff19cb
srivardhan
fac24ee030b2a4a4d846167e98ff19cb
manzhouli
fac24ee030b2a4a4d846167e98ff19cb
lavrentiya
fac24ee030b2a4a4d846167e98ff19cb
aste
fac24ee030b2a4a4d846167e98ff19cb
najran
fac24ee030b2a4a4d846167e98ff19cb
langxiang
fac24ee030b2a4a4d846167e98ff19cb
cap-aux-meules
fac24ee030b2a4a4d846167e98ff19cb
necochea
fac24ee030b2a4a4d846167e98ff19cb
tres picos
fac24ee030b2a4a4d846167e98ff19cb
uralskiy
fac24ee030b2a4a4d846167e98ff19cb
porto-vecchio
fac24ee030b2a4a4d846167e98ff19cb
wanning
fac24ee030b2a4a4d846167e98ff19cb
shemonaikha
fac24ee030b2a4a4d846167e98ff19cb
shihezi
fac24ee030b2a4a4d846167e98ff19cb
pevek
fac24ee030b2a4a4d846167e98ff19cb
hambantota
fac24ee030b2a4a4d846167e98ff19cb
mount isa
fac24ee030b2a4a4d846167e98ff19cb
marzuq
fac24ee030b2a4a4d846167e98ff19cb
arlit
fac24ee030b2a4a4d846167e98ff19cb
masallatah
fac24ee030b2a4a4d846167e98ff19cb
lagoa
fac24ee030b2a4a4d846167e98ff19cb
smithers
fac24ee030b2a4a4d846167e98ff19cb
palu
fac24ee030b2a4a4d846167e98ff19cb
upernavik
fac24ee030b2a4a4d846167e98ff19cb
talnakh
fac24ee030b2a4a4d846167e98ff19cb
kamenskoye
fac24ee030b2a4a4d846167e98ff19cb
safaqis
fac24ee030b2a4a4d846167e98ff19cb
shitkino
fac24ee030b2a4a4d846167e98ff19cb
shar
fac24ee030b2a4a4d846167e98ff19cb
baboua
fac24ee030b2a4a4d846167e98ff19cb
thessalon
fac24ee030b2a4a4d846167e98ff19cb
broome
fac24ee030b2a4a4d846167e98ff19cb
cairns
fac24ee030b2a4a4d846167e98ff19cb
longyearbyen
fac24ee030b2a4a4d846167e98ff19cb
thompson
fac24ee030b2a4a4d846167e98ff19cb
bozhou
fac24ee030b2a4a4d846167e98ff19cb
fortuna
fac24ee030b2a4a4d846167e98ff19cb
strezhevoy
fac24ee030b2a4a4d846167e98ff19cb
quatre cocos
fac24ee030b2a4a4d846167e98ff19cb
maceio
fac24ee030b2a4a4d846167e98ff19cb
belyy yar
fac24ee030b2a4a4d846167e98ff19cb
sao joao da barra
fac24ee030b2a4a4d846167e98ff19cb
torbay
fac24ee030b2a4a4d846167e98ff19cb
arang
fac24ee030b2a4a4d846167e98ff19cb
dawlatabad
fac24ee030b2a4a4d846167e98ff19cb
thunder bay
fac24ee030b2a4a4d846167e98ff19cb
comodoro rivadavia
fac24ee030b2a4a4d846167e98ff19cb
kudahuvadhoo
fac24ee030b2a4a4d846167e98ff19cb
belushya guba
fac24ee030b2a4a4d846167e98ff19cb
queanbeyan
fac24ee030b2a4a4d846167e98ff19cb
miraflores
fac24ee030b2a4a4d846167e98ff19cb
asosa
fac24ee030b2a4a4d846167e98ff19cb
brewster
fac24ee030b2a4a4d846167e98ff19cb
gazanjyk
fac24ee030b2a4a4d846167e98ff19cb
saint-augustin
fac24ee030b2a4a4d846167e98ff19cb
nazarovo
fac24ee030b2a4a4d846167e98ff19cb
shingu
fac24ee030b2a4a4d846167e98ff19cb
atar
fac24ee030b2a4a4d846167e98ff19cb
kokstad
fac24ee030b2a4a4d846167e98ff19cb
sao sebastiao
fac24ee030b2a4a4d846167e98ff19cb
bichura
fac24ee030b2a4a4d846167e98ff19cb
ejutla de crespo
fac24ee030b2a4a4d846167e98ff19cb
kencong
fac24ee030b2a4a4d846167e98ff19cb
saeby
fac24ee030b2a4a4d846167e98ff19cb
beringovskiy
fac24ee030b2a4a4d846167e98ff19cb
east london
fac24ee030b2a4a4d846167e98ff19cb
aklavik
fac24ee030b2a4a4d846167e98ff19cb
lovozero
fac24ee030b2a4a4d846167e98ff19cb
nouakchott
fac24ee030b2a4a4d846167e98ff19cb
bellevue
fac24ee030b2a4a4d846167e98ff19cb
union
fac24ee030b2a4a4d846167e98ff19cb
inuvik
fac24ee030b2a4a4d846167e98ff19cb
louisbourg
fac24ee030b2a4a4d846167e98ff19cb
chagda
fac24ee030b2a4a4d846167e98ff19cb
grand river south east
fac24ee030b2a4a4d846167e98ff19cb
divnomorskoye
fac24ee030b2a4a4d846167e98ff19cb
kurmanayevka
fac24ee030b2a4a4d846167e98ff19cb
san patricio
fac24ee030b2a4a4d846167e98ff19cb
arraial do cabo
fac24ee030b2a4a4d846167e98ff19cb
fare
fac24ee030b2a4a4d846167e98ff19cb
boueni
fac24ee030b2a4a4d846167e98ff19cb
opuwo
fac24ee030b2a4a4d846167e98ff19cb
seoul
fac24ee030b2a4a4d846167e98ff19cb
urumqi
fac24ee030b2a4a4d846167e98ff19cb
cheuskiny
fac24ee030b2a4a4d846167e98ff19cb
verkh-usugli
fac24ee030b2a4a4d846167e98ff19cb
ancud
fac24ee030b2a4a4d846167e98ff19cb
santiago del estero
fac24ee030b2a4a4d846167e98ff19cb
dingle
fac24ee030b2a4a4d846167e98ff19cb
bengkulu
fac24ee030b2a4a4d846167e98ff19cb
alyangula
fac24ee030b2a4a4d846167e98ff19cb
okhotsk
fac24ee030b2a4a4d846167e98ff19cb
cayenne
fac24ee030b2a4a4d846167e98ff19cb
rungata
fac24ee030b2a4a4d846167e98ff19cb
vardo
fac24ee030b2a4a4d846167e98ff19cb
buala
fac24ee030b2a4a4d846167e98ff19cb
northam
fac24ee030b2a4a4d846167e98ff19cb
fuxin
fac24ee030b2a4a4d846167e98ff19cb
jabinyanah
fac24ee030b2a4a4d846167e98ff19cb
haibowan
fac24ee030b2a4a4d846167e98ff19cb
derzhavinsk
fac24ee030b2a4a4d846167e98ff19cb
muros
fac24ee030b2a4a4d846167e98ff19cb
sinop
fac24ee030b2a4a4d846167e98ff19cb
petropavlovsk-kamchatskiy
fac24ee030b2a4a4d846167e98ff19cb
wagar
fac24ee030b2a4a4d846167e98ff19cb
guerrero negro
fac24ee030b2a4a4d846167e98ff19cb
chapais
fac24ee030b2a4a4d846167e98ff19cb
vaitupu
fac24ee030b2a4a4d846167e98ff19cb
mount gambier
fac24ee030b2a4a4d846167e98ff19cb
lebu
fac24ee030b2a4a4d846167e98ff19cb
chernyshevskiy
fac24ee030b2a4a4d846167e98ff19cb
havre-saint-pierre
fac24ee030b2a4a4d846167e98ff19cb
mackay
fac24ee030b2a4a4d846167e98ff19cb
margate
fac24ee030b2a4a4d846167e98ff19cb
nikolskoye
fac24ee030b2a4a4d846167e98ff19cb
karamea
fac24ee030b2a4a4d846167e98ff19cb
chiredzi
fac24ee030b2a4a4d846167e98ff19cb
kushmurun
fac24ee030b2a4a4d846167e98ff19cb
businga
fac24ee030b2a4a4d846167e98ff19cb
sterling
fac24ee030b2a4a4d846167e98ff19cb
belaya gora
fac24ee030b2a4a4d846167e98ff19cb
rosetta
fac24ee030b2a4a4d846167e98ff19cb
belgrade
fac24ee030b2a4a4d846167e98ff19cb
fairmont
fac24ee030b2a4a4d846167e98ff19cb
omboue
fac24ee030b2a4a4d846167e98ff19cb
turukhansk
fac24ee030b2a4a4d846167e98ff19cb
jinchang
fac24ee030b2a4a4d846167e98ff19cb
labuhan
fac24ee030b2a4a4d846167e98ff19cb
shitanjing
fac24ee030b2a4a4d846167e98ff19cb
padang
fac24ee030b2a4a4d846167e98ff19cb
lanigan
fac24ee030b2a4a4d846167e98ff19cb
tucuma
fac24ee030b2a4a4d846167e98ff19cb
boa vista
fac24ee030b2a4a4d846167e98ff19cb
luganville
fac24ee030b2a4a4d846167e98ff19cb
xining
fac24ee030b2a4a4d846167e98ff19cb
sarankhola
fac24ee030b2a4a4d846167e98ff19cb
ngaoundere
fac24ee030b2a4a4d846167e98ff19cb
rauma
fac24ee030b2a4a4d846167e98ff19cb
sakakah
fac24ee030b2a4a4d846167e98ff19cb
verkhnyaya inta
fac24ee030b2a4a4d846167e98ff19cb
burica
fac24ee030b2a4a4d846167e98ff19cb
phayao
fac24ee030b2a4a4d846167e98ff19cb
namibe
fac24ee030b2a4a4d846167e98ff19cb
sidi bu zayd
fac24ee030b2a4a4d846167e98ff19cb
marcona
fac24ee030b2a4a4d846167e98ff19cb
palora
fac24ee030b2a4a4d846167e98ff19cb
phan thiet
fac24ee030b2a4a4d846167e98ff19cb
miandrivazo
fac24ee030b2a4a4d846167e98ff19cb
sao jose da coroa grande
fac24ee030b2a4a4d846167e98ff19cb
mon
fac24ee030b2a4a4d846167e98ff19cb
pangnirtung
fac24ee030b2a4a4d846167e98ff19cb
grootfontein
fac24ee030b2a4a4d846167e98ff19cb
plainview
fac24ee030b2a4a4d846167e98ff19cb
jonuta
fac24ee030b2a4a4d846167e98ff19cb
mao
fac24ee030b2a4a4d846167e98ff19cb
tura
fac24ee030b2a4a4d846167e98ff19cb
beloha
fac24ee030b2a4a4d846167e98ff19cb
diffa
fac24ee030b2a4a4d846167e98ff19cb
linkou
fac24ee030b2a4a4d846167e98ff19cb
santa maria
fac24ee030b2a4a4d846167e98ff19cb
komsomolskiy
fac24ee030b2a4a4d846167e98ff19cb
constitucion
fac24ee030b2a4a4d846167e98ff19cb
adrar
fac24ee030b2a4a4d846167e98ff19cb
saint-georges
fac24ee030b2a4a4d846167e98ff19cb
bandarbeyla
fac24ee030b2a4a4d846167e98ff19cb
kieta
fac24ee030b2a4a4d846167e98ff19cb
harper
fac24ee030b2a4a4d846167e98ff19cb
mandera
fac24ee030b2a4a4d846167e98ff19cb
burnie
fac24ee030b2a4a4d846167e98ff19cb
conceicao do araguaia
fac24ee030b2a4a4d846167e98ff19cb
doha
fac24ee030b2a4a4d846167e98ff19cb
vila franca do campo
fac24ee030b2a4a4d846167e98ff19cb
kayasula
fac24ee030b2a4a4d846167e98ff19cb
ayia galini
fac24ee030b2a4a4d846167e98ff19cb
brae
fac24ee030b2a4a4d846167e98ff19cb
carbondale
fac24ee030b2a4a4d846167e98ff19cb
tuggurt
fac24ee030b2a4a4d846167e98ff19cb
bure
fac24ee030b2a4a4d846167e98ff19cb
tanout
fac24ee030b2a4a4d846167e98ff19cb
shelburne
fac24ee030b2a4a4d846167e98ff19cb
cheremshan
fac24ee030b2a4a4d846167e98ff19cb
bonavista
fac24ee030b2a4a4d846167e98ff19cb
lorengau
fac24ee030b2a4a4d846167e98ff19cb
safaga
fac24ee030b2a4a4d846167e98ff19cb
bajo baudo
fac24ee030b2a4a4d846167e98ff19cb
walvis bay
fac24ee030b2a4a4d846167e98ff19cb
moissala
fac24ee030b2a4a4d846167e98ff19cb
biak
fac24ee030b2a4a4d846167e98ff19cb
moose factory
fac24ee030b2a4a4d846167e98ff19cb
naifaru
fac24ee030b2a4a4d846167e98ff19cb
westport
fac24ee030b2a4a4d846167e98ff19cb
doiwala
fac24ee030b2a4a4d846167e98ff19cb
leningradskiy
fac24ee030b2a4a4d846167e98ff19cb
bauchi
fac24ee030b2a4a4d846167e98ff19cb
serpa
fac24ee030b2a4a4d846167e98ff19cb
malacacheta
fac24ee030b2a4a4d846167e98ff19cb
formoso do araguaia
fac24ee030b2a4a4d846167e98ff19cb
saltabarranca
fac24ee030b2a4a4d846167e98ff19cb
hofn
fac24ee030b2a4a4d846167e98ff19cb
kjollefjord
fac24ee030b2a4a4d846167e98ff19cb
taltal
fac24ee030b2a4a4d846167e98ff19cb
yurginskoye
fac24ee030b2a4a4d846167e98ff19cb
ipixuna
fac24ee030b2a4a4d846167e98ff19cb
si satchanalai
fac24ee030b2a4a4d846167e98ff19cb
dikson
fac24ee030b2a4a4d846167e98ff19cb
oranjemund
fac24ee030b2a4a4d846167e98ff19cb
labutta
fac24ee030b2a4a4d846167e98ff19cb
ravar
fac24ee030b2a4a4d846167e98ff19cb
prince rupert
fac24ee030b2a4a4d846167e98ff19cb
rasht
fac24ee030b2a4a4d846167e98ff19cb
uglovskoye
fac24ee030b2a4a4d846167e98ff19cb
pavlovka
fac24ee030b2a4a4d846167e98ff19cb
bud
fac24ee030b2a4a4d846167e98ff19cb
port-de-bouc
fac24ee030b2a4a4d846167e98ff19cb
awash
fac24ee030b2a4a4d846167e98ff19cb
kindia
fac24ee030b2a4a4d846167e98ff19cb
jujuy
fac24ee030b2a4a4d846167e98ff19cb
gioia tauro
fac24ee030b2a4a4d846167e98ff19cb
umzimvubu
fac24ee030b2a4a4d846167e98ff19cb
alofi
fac24ee030b2a4a4d846167e98ff19cb
sharan
fac24ee030b2a4a4d846167e98ff19cb
popondetta
fac24ee030b2a4a4d846167e98ff19cb
akureyri
fac24ee030b2a4a4d846167e98ff19cb
dunn
fac24ee030b2a4a4d846167e98ff19cb
kenora
fac24ee030b2a4a4d846167e98ff19cb
minas
fac24ee030b2a4a4d846167e98ff19cb
severnyy-kospashskiy
fac24ee030b2a4a4d846167e98ff19cb
solnechnyy
fac24ee030b2a4a4d846167e98ff19cb
bosaso
fac24ee030b2a4a4d846167e98ff19cb
garowe
fac24ee030b2a4a4d846167e98ff19cb
curatele
fac24ee030b2a4a4d846167e98ff19cb
sao filipe
fac24ee030b2a4a4d846167e98ff19cb
quang ngai
fac24ee030b2a4a4d846167e98ff19cb
prykolotne
fac24ee030b2a4a4d846167e98ff19cb
palabuhanratu
fac24ee030b2a4a4d846167e98ff19cb
bukachacha
fac24ee030b2a4a4d846167e98ff19cb
richards bay
fac24ee030b2a4a4d846167e98ff19cb
mangai
fac24ee030b2a4a4d846167e98ff19cb
luquillo
fac24ee030b2a4a4d846167e98ff19cb
muzaffarabad
fac24ee030b2a4a4d846167e98ff19cb
egvekinot
fac24ee030b2a4a4d846167e98ff19cb
nikolayevskaya
fac24ee030b2a4a4d846167e98ff19cb
chumphon
fac24ee030b2a4a4d846167e98ff19cb
hamilton
fac24ee030b2a4a4d846167e98ff19cb
teknaf
fac24ee030b2a4a4d846167e98ff19cb
qala
fac24ee030b2a4a4d846167e98ff19cb
nizhneyansk
fac24ee030b2a4a4d846167e98ff19cb
goderich
fac24ee030b2a4a4d846167e98ff19cb
kayerkan
fac24ee030b2a4a4d846167e98ff19cb
le vauclin
fac24ee030b2a4a4d846167e98ff19cb
cherskiy
fac24ee030b2a4a4d846167e98ff19cb
parana
fac24ee030b2a4a4d846167e98ff19cb
koumra
fac24ee030b2a4a4d846167e98ff19cb
goya
fac24ee030b2a4a4d846167e98ff19cb
geraldton
fac24ee030b2a4a4d846167e98ff19cb
vanimo
fac24ee030b2a4a4d846167e98ff19cb
nogliki
fac24ee030b2a4a4d846167e98ff19cb
sao miguel do oeste
fac24ee030b2a4a4d846167e98ff19cb
galesong
fac24ee030b2a4a4d846167e98ff19cb
asfi
fac24ee030b2a4a4d846167e98ff19cb
kulu
fac24ee030b2a4a4d846167e98ff19cb
ararat
fac24ee030b2a4a4d846167e98ff19cb
san quintin
fac24ee030b2a4a4d846167e98ff19cb
ndouci
fac24ee030b2a4a4d846167e98ff19cb
banda aceh
fac24ee030b2a4a4d846167e98ff19cb
barbar
fac24ee030b2a4a4d846167e98ff19cb
gollere
fac24ee030b2a4a4d846167e98ff19cb
shimoda
fac24ee030b2a4a4d846167e98ff19cb
vestmanna
fac24ee030b2a4a4d846167e98ff19cb
la ronge
fac24ee030b2a4a4d846167e98ff19cb
ha tinh
fac24ee030b2a4a4d846167e98ff19cb
parainen
fac24ee030b2a4a4d846167e98ff19cb
ginda
fac24ee030b2a4a4d846167e98ff19cb
davila
fac24ee030b2a4a4d846167e98ff19cb
oksfjord
fac24ee030b2a4a4d846167e98ff19cb
bilibino
fac24ee030b2a4a4d846167e98ff19cb
salinas
fac24ee030b2a4a4d846167e98ff19cb
carutapera
fac24ee030b2a4a4d846167e98ff19cb
ploemeur
fac24ee030b2a4a4d846167e98ff19cb
umm durman
fac24ee030b2a4a4d846167e98ff19cb
port macquarie
fac24ee030b2a4a4d846167e98ff19cb
nola
fac24ee030b2a4a4d846167e98ff19cb
itarema
fac24ee030b2a4a4d846167e98ff19cb
adelaide
fac24ee030b2a4a4d846167e98ff19cb
iqaluit
fac24ee030b2a4a4d846167e98ff19cb
aktau
fac24ee030b2a4a4d846167e98ff19cb
ulverstone
fac24ee030b2a4a4d846167e98ff19cb
papara
fac24ee030b2a4a4d846167e98ff19cb
ostrovnoy
fac24ee030b2a4a4d846167e98ff19cb
pa sang
fac24ee030b2a4a4d846167e98ff19cb
prague
fac24ee030b2a4a4d846167e98ff19cb
uyemskiy
fac24ee030b2a4a4d846167e98ff19cb
putina
fac24ee030b2a4a4d846167e98ff19cb
aswan
fac24ee030b2a4a4d846167e98ff19cb
cherlak
fac24ee030b2a4a4d846167e98ff19cb
mustasaari
fac24ee030b2a4a4d846167e98ff19cb
dmitriyevka
fac24ee030b2a4a4d846167e98ff19cb
dakar
fac24ee030b2a4a4d846167e98ff19cb
ngukurr
fac24ee030b2a4a4d846167e98ff19cb
zolotinka
fac24ee030b2a4a4d846167e98ff19cb
zyryanka
fac24ee030b2a4a4d846167e98ff19cb
sistranda
fac24ee030b2a4a4d846167e98ff19cb
shenjiamen
fac24ee030b2a4a4d846167e98ff19cb
san juan evangelista
fac24ee030b2a4a4d846167e98ff19cb
kokopo
fac24ee030b2a4a4d846167e98ff19cb
palmer
fac24ee030b2a4a4d846167e98ff19cb
kletskaya
fac24ee030b2a4a4d846167e98ff19cb
bogande
fac24ee030b2a4a4d846167e98ff19cb
vianopolis
fac24ee030b2a4a4d846167e98ff19cb
deputatskiy
fac24ee030b2a4a4d846167e98ff19cb
conde
fac24ee030b2a4a4d846167e98ff19cb
timbo
fac24ee030b2a4a4d846167e98ff19cb
sambava
fac24ee030b2a4a4d846167e98ff19cb
pulivendla
fac24ee030b2a4a4d846167e98ff19cb
dunedin
fac24ee030b2a4a4d846167e98ff19cb
viedma
fac24ee030b2a4a4d846167e98ff19cb
amga
fac24ee030b2a4a4d846167e98ff19cb
portland
fac24ee030b2a4a4d846167e98ff19cb
tarija
fac24ee030b2a4a4d846167e98ff19cb
rocha
fac24ee030b2a4a4d846167e98ff19cb
lata
fac24ee030b2a4a4d846167e98ff19cb
auki
fac24ee030b2a4a4d846167e98ff19cb
mullaitivu
fac24ee030b2a4a4d846167e98ff19cb
palestine
fac24ee030b2a4a4d846167e98ff19cb
lapi
fac24ee030b2a4a4d846167e98ff19cb
hastings
fac24ee030b2a4a4d846167e98ff19cb
cacu
fac24ee030b2a4a4d846167e98ff19cb
sorvag
fac24ee030b2a4a4d846167e98ff19cb
wladyslawowo
fac24ee030b2a4a4d846167e98ff19cb
tumaco
fac24ee030b2a4a4d846167e98ff19cb
qaqortoq
fac24ee030b2a4a4d846167e98ff19cb
lanivtsi
fac24ee030b2a4a4d846167e98ff19cb
nguiu
fac24ee030b2a4a4d846167e98ff19cb
bridgetown
fac24ee030b2a4a4d846167e98ff19cb
cefalu
fac24ee030b2a4a4d846167e98ff19cb
meadow lake
fac24ee030b2a4a4d846167e98ff19cb
kavaratti
fac24ee030b2a4a4d846167e98ff19cb
matara
fac24ee030b2a4a4d846167e98ff19cb
soe
fac24ee030b2a4a4d846167e98ff19cb
huzhou
fac24ee030b2a4a4d846167e98ff19cb
mormugao
fac24ee030b2a4a4d846167e98ff19cb
thinadhoo
fac24ee030b2a4a4d846167e98ff19cb
collie
fac24ee030b2a4a4d846167e98ff19cb
sitka
fac24ee030b2a4a4d846167e98ff19cb
todos santos
fac24ee030b2a4a4d846167e98ff19cb
eyl
fac24ee030b2a4a4d846167e98ff19cb
manokwari
fac24ee030b2a4a4d846167e98ff19cb
bairiki
fac24ee030b2a4a4d846167e98ff19cb
wawa
fac24ee030b2a4a4d846167e98ff19cb
nioro
fac24ee030b2a4a4d846167e98ff19cb
lac du bonnet
fac24ee030b2a4a4d846167e98ff19cb
itaituba
fac24ee030b2a4a4d846167e98ff19cb
berlevag
fac24ee030b2a4a4d846167e98ff19cb
saquarema
fac24ee030b2a4a4d846167e98ff19cb
sur
fac24ee030b2a4a4d846167e98ff19cb
matagami
fac24ee030b2a4a4d846167e98ff19cb
agde
fac24ee030b2a4a4d846167e98ff19cb
ranong
fac24ee030b2a4a4d846167e98ff19cb
liverpool
fac24ee030b2a4a4d846167e98ff19cb
mushie
fac24ee030b2a4a4d846167e98ff19cb
novovorontsovka
fac24ee030b2a4a4d846167e98ff19cb
huambo
fac24ee030b2a4a4d846167e98ff19cb
kurilsk
fac24ee030b2a4a4d846167e98ff19cb
henties bay
fac24ee030b2a4a4d846167e98ff19cb
coalcoman
fac24ee030b2a4a4d846167e98ff19cb
hovd
fac24ee030b2a4a4d846167e98ff19cb
kavieng
fac24ee030b2a4a4d846167e98ff19cb
ellisras
fac24ee030b2a4a4d846167e98ff19cb
cortez
fac24ee030b2a4a4d846167e98ff19cb
sonoita
fac24ee030b2a4a4d846167e98ff19cb
khonuu
fac24ee030b2a4a4d846167e98ff19cb
kailaras
fac24ee030b2a4a4d846167e98ff19cb
lagunas
fac24ee030b2a4a4d846167e98ff19cb
oxelosund
fac24ee030b2a4a4d846167e98ff19cb
corrales
fac24ee030b2a4a4d846167e98ff19cb
kirakira
fac24ee030b2a4a4d846167e98ff19cb
tabiauea
fac24ee030b2a4a4d846167e98ff19cb
ahipara
fac24ee030b2a4a4d846167e98ff19cb
doka
fac24ee030b2a4a4d846167e98ff19cb
salmas
fac24ee030b2a4a4d846167e98ff19cb
saint-leu
fac24ee030b2a4a4d846167e98ff19cb
port victoria
fac24ee030b2a4a4d846167e98ff19cb
marsh harbour
fac24ee030b2a4a4d846167e98ff19cb
makakilo city
fac24ee030b2a4a4d846167e98ff19cb
wembley
fac24ee030b2a4a4d846167e98ff19cb
damietta
fac24ee030b2a4a4d846167e98ff19cb
sabinov
fac24ee030b2a4a4d846167e98ff19cb
arman
fac24ee030b2a4a4d846167e98ff19cb
ondjiva
fac24ee030b2a4a4d846167e98ff19cb
teguise
fac24ee030b2a4a4d846167e98ff19cb
half moon bay
fac24ee030b2a4a4d846167e98ff19cb
la rochelle
fac24ee030b2a4a4d846167e98ff19cb
mayo
fac24ee030b2a4a4d846167e98ff19cb
coxim
fac24ee030b2a4a4d846167e98ff19cb
mentok
fac24ee030b2a4a4d846167e98ff19cb
bataipora
fac24ee030b2a4a4d846167e98ff19cb
salalah
fac24ee030b2a4a4d846167e98ff19cb
poum
fac24ee030b2a4a4d846167e98ff19cb
toucheng
fac24ee030b2a4a4d846167e98ff19cb
shache
fac24ee030b2a4a4d846167e98ff19cb
pundaguitan
fac24ee030b2a4a4d846167e98ff19cb
progreso
fac24ee030b2a4a4d846167e98ff19cb
leh
fac24ee030b2a4a4d846167e98ff19cb
sorland
fac24ee030b2a4a4d846167e98ff19cb
ust-kuyga
fac24ee030b2a4a4d846167e98ff19cb
hihifo
fac24ee030b2a4a4d846167e98ff19cb
byron bay
fac24ee030b2a4a4d846167e98ff19cb
maarianhamina
fac24ee030b2a4a4d846167e98ff19cb
port hardy
fac24ee030b2a4a4d846167e98ff19cb
ijaki
fac24ee030b2a4a4d846167e98ff19cb
bengkalis
fac24ee030b2a4a4d846167e98ff19cb
pangkalanbuun
fac24ee030b2a4a4d846167e98ff19cb
severo-yeniseyskiy
fac24ee030b2a4a4d846167e98ff19cb
brooks
fac24ee030b2a4a4d846167e98ff19cb
kurush
fac24ee030b2a4a4d846167e98ff19cb
zhangjiakou
fac24ee030b2a4a4d846167e98ff19cb
dezful
fac24ee030b2a4a4d846167e98ff19cb
bonthe
fac24ee030b2a4a4d846167e98ff19cb
tokur
fac24ee030b2a4a4d846167e98ff19cb
miles city

import json
output = [json.loads(out) for out in output]
outputs_that_worked = [out for out in output if out["cod"] != "404"]

print(len(outputs_that_worked))
448

raw_data = []

for out in outputs_that_worked:
    try:
        raw_data.append(dict(lon=out["coord"]["lon"],
                        lat=out["coord"]["lat"],
                        temp=out["main"]["temp"],
                        pressure=out["main"]["pressure"],
                        humidity=out["main"]["humidity"],
                        wind=out["wind"]["speed"],
                        clouds=out["clouds"]["all"],
                        name=out["name"]))
    except:
        pass
        
print(len(raw_data))
448

import pandas as pd

df_weather = pd.DataFrame(raw_data)
df_weather.to_csv("Weather_Raw_Data.csv")
df_weather

	clouds	humidity	lat	lon	name	pressure	temp	wind
0	0	27	24.63	46.72	Riyadh	1011.00	299.15	1.16
1	32	25	-33.21	138.60	Jamestown	1022.93	292.60	4.27
2	0	46	16.42	-3.66	Goundam	1008.27	304.50	6.21
3	100	94	71.64	128.87	Tiksi	1018.92	277.10	4.59
4	100	57	-21.57	165.50	Bourail	1018.00	294.60	2.25
5	8	56	-17.60	-67.51	Eucaliptus	1018.84	284.00	2.29
6	75	62	22.08	-159.32	Kapaa	1012.00	301.66	3.60
7	20	94	6.80	-58.16	Georgetown	1010.00	298.15	2.10
8	1	66	42.65	-73.75	Albany	1023.00	283.51	2.60
9	100	68	70.62	147.90	Chokurdakh	1018.09	279.80	7.25
10	40	80	-54.81	-68.31	Ushuaia	992.00	277.15	1.33
11	26	64	71.97	114.09	Saskylakh	1020.77	276.80	3.29
12	44	77	-3.66	152.44	Namatanai	1010.63	300.00	3.00
13	90	81	-42.48	-73.76	Castro	1022.00	280.15	2.60
14	1	87	45.36	-73.48	Saint-Philippe	1024.00	283.70	2.10
15	75	65	19.71	-155.08	Hilo	1013.00	297.84	4.60
16	40	88	51.21	-102.46	Yorkton	1000.00	292.15	3.60
17	0	58	29.28	82.18	Jumla	1018.32	288.90	1.07
18	90	100	62.45	-114.38	Yellowknife	1005.00	279.65	4.10
19	19	53	-21.21	-159.78	Avarua	1012.00	297.15	5.70
20	92	59	13.64	4.03	Dogondoutchi	1009.09	300.80	1.48
21	57	84	11.54	-72.91	Riohacha	1010.20	300.00	0.77
22	100	95	10.65	-9.88	Kouroussa	1012.54	293.60	1.58
23	0	75	-9.80	-139.03	Atuona	1011.38	299.40	5.37
24	20	78	13.07	-59.53	Oistins	1012.00	301.15	6.20
25	0	70	-16.48	-151.75	Faanui	1010.94	299.60	1.51
26	0	24	-23.58	149.07	Bluff	1016.33	301.00	2.13
27	98	65	-23.12	-134.97	Rikitea	1018.28	293.20	6.75
28	37	70	-0.60	73.08	Hithadhoo	1011.38	301.40	1.62
29	96	92	-30.17	-50.22	Cidreira	1010.32	288.00	3.19
...	...	...	...	...	...	...	...	...
418	19	84	-35.17	173.16	Ahipara	1027.00	290.93	9.60
419	98	95	13.52	35.76	Doka	1011.37	294.50	5.74
420	0	53	38.20	44.77	Salmas	1018.00	284.15	3.10
421	90	77	-21.15	55.28	Saint-Leu	1019.00	292.44	8.70
422	75	71	55.15	-119.14	Wembley	1008.00	284.15	2.10
423	0	65	31.42	31.81	Damietta	1014.00	299.15	4.10
424	0	66	49.10	21.10	Sabinov	1014.00	280.51	1.00
425	100	71	59.70	150.17	Arman	1011.29	282.10	1.14
426	0	12	-17.07	15.73	Ondjiva	1013.97	290.80	3.49
427	20	77	29.06	-13.56	Teguise	1016.00	294.15	3.60
428	75	87	63.59	-135.90	Mayo	1006.00	283.15	1.50
429	99	39	-18.50	-54.75	Coxim	1007.36	298.90	2.52
430	45	53	-22.30	-53.27	Bataipora	1006.88	297.90	1.05
431	75	83	17.01	54.10	Salalah	1008.00	300.15	2.60
432	40	87	41.28	20.71	Poum	1017.00	282.15	1.00
433	75	78	24.86	121.82	Toucheng	1012.00	299.38	2.60
434	0	25	38.42	77.24	Shache	1023.50	294.30	4.89
435	100	77	6.37	126.17	Pundaguitan	1012.36	300.60	7.01
436	0	62	-34.68	-56.22	Progreso	1008.00	285.41	3.10
437	0	31	34.16	77.58	Leh	1031.45	271.70	1.64
438	75	81	67.67	12.69	Sorland	1008.00	281.15	5.70
439	100	76	70.00	135.55	Ust-Kuyga	1014.58	280.40	3.67
440	11	44	-2.68	111.62	Pangkalanbuun	1012.74	306.30	2.47
441	100	95	60.37	93.04	Severo-Yeniseyskiy	1007.87	282.40	5.04
442	66	83	50.57	-111.89	Brooks	1006.00	284.26	4.59
443	0	82	41.28	47.83	Kurush	1015.00	290.15	5.10
444	0	28	40.77	114.88	Zhangjiakou	1028.35	285.80	0.98
445	62	16	32.38	48.40	Dezful	1008.95	303.70	2.79
446	100	92	7.53	-12.50	Bonthe	1011.28	297.80	3.38
447	100	98	53.13	132.90	Tokur	1002.56	277.20	2.91
448 rows × 8 columns

plt.scatter(df_weather["lat"], df_weather["temp"])
plt.title('Temperature vs Latitude')
plt.xlabel('Latitude')
plt.ylabel('Temperature')
plt.show()

plt.scatter(df_weather["lat"], df_weather["humidity"])
plt.title('Humidity vs Latitude')
plt.xlabel('Latitude')
plt.ylabel('Humidity')
plt.show()

plt.scatter(df_weather["lat"], df_weather["clouds"])
plt.title('Cloudiness vs Latitude')
plt.xlabel('Latitude')
plt.ylabel('Cloudiness')
plt.show()

plt.scatter(df_weather["lat"], df_weather["wind"])
plt.title('Wind Speed vs Latitude')
plt.xlabel('Latitude')
plt.ylabel('Wind Speed')
plt.show()