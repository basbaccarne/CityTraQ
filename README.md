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
