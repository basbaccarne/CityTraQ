# CityTraQ
This repo is the working directory for the CityTraQ project in which we visualize air quality data to increase awareness regarding the impact of interventions

## tests
### API & Protopie integration demo
This test provides a template to work with air quality API data in Protopie and is meant as a starting point for cocreation & concept development.
* The demo uses data from openweathermap.org
* Create an account to get a key
* You'll need [ProtoPie Connect](https://www.protopie.io/download#connect-download) for this demo (only works with *pro or enterprise* license)
* Get lattitude & longitude (for Toverberg: `lat=51.059357&lon=3.749582`)
* In Protopie Connect, set-up the API plugin as follows (replace lat, lon & API key):
    * Method: `GET`
    * URL: `http://api.openweathermap.org/data/2.5/air_pollution?lat={lat}&lon={lon}&appid={API key})`
* In Protopie Studio, you can extract data from the JSOn response using `parseJson(JSON_response,"list.0.components.no2")` (see [demo file](/tests/CityTraQ%20demo.pie))

![demo](/tests/demo1.gif)

### Telraam & Protopie demo
There is a [telraam](https://telraam.net/) sensor in the [Schoolstraat](https://telraam.net/nl/location/9000004115). We can access this data in Protopie in the same way.
* Create a telraam [account](https://telraam.net/en/register) to get an API key (`account > API tokens`)
* In Protopie Connect, set-up the API plugin as follows:
    * Method: `POST`
    * URL: `https://telraam-api.net/v1/reports/traffic`
    * Header: `{"X-Api-Key": "Your personal API key"}`
    * Body:
      ```
      {
      "id":"9000004115",
      "time_start":"2024-02-20 00:00:00Z",
      "time_end":"2024-02-21 00:00:00Z",
      "level":"segments",
      "format":"per-hour"
      }
      ```
* You can add more complex data interactions using components, parsing and Protopie send/receive function (see [example](tests/Telraam%20demo.pie))

  ![demo2](/tests/demo2.gif)

### Kunak API
VMM placed Kunak sensors at different locations in Ghent. VMM will build their own API in time, but the Kunak data can also be accessed directly.
#### notes on the API
- All the timestamps in this API use the UTC zone
- Follow URL encoding (spaces are %20)
- Request limit: Max 15.000 calls / month & max 10 calls / second
- Auth: Authorization: Basic (aka: in the HTTP header: This is the Base64 codification of the string "user:password")
- Base url: `https://kunakcloud.com/openAPIv0/v1/rest/`
#### relevant API calls
- userdata: `https://kunakcloud.com/openAPIv0/v1/rest/users/VMMBELGIUM/info`
- sensor overview (incl. IDs): `https://kunakcloud.com/openAPIv0/v1/rest/devices/list/VMMBELGIUM`
- what is measured by a sensor: `https://kunakcloud.com/openAPIv0/v1/rest/devices/0423440199/elementsDetails`
- live measurement: `https://kunakcloud.com/openAPIv0/v1/rest/devices/0423440199/elements/NO2%20GC/info`
- interval measurement: `https://kunakcloud.com/openAPIv0/v1/rest/devices/0423440199/elements/NO2%20GC/reads/fromTo?startTs=1700735563000&endTs=1700735885000`
#### notes on the data
Measurements ('elements'):
- `NO2 GC`: NO2 meting (gaschromatochrafie) in ppb (parts per billion) in een sample van 300 seconden (5 min.)
- `NO2 GCc`: NO2 meting (gaschromatochrafie?) in ppb (parts per billion) in een sample van 300 seconden (5 min.)
- `NO2 GCc AVG1H`: NO2 meting in een sample van 3600 seconden (1 uur)
- `NO2 GCc AVG24H`: NO2 meting in een sample van 3600 seconden > hoe wordt dit berekend?

