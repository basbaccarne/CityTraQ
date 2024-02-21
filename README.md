# CityTraQ
This repo is the working directory for the CityTraQ project in which we visualize air quality data to increase awareness regarding the impact of interventions

## tests
### API & Protopie integration demo
This test provides a template to work with air quality API data in Protopie and is meant as a starting point for cocreation & concept development.
* The demo uses data from openweathermap.org
* Create an account to get a key
* You'll need [ProtoPie Connect](https://www.protopie.io/download#connect-download) for this demo (only works with *pro or enterprise* license)
* In Protopie Connect, set-up the API plugin as follows (replace lat, lon & API key):
    * Method: `GET`
    * URL: `http://api.openweathermap.org/data/2.5/air_pollution?lat={lat}&lon={lon}&appid={API key})`
* In Protopie Studio, you can extract data from the JSOn response using `parseJson(JSON_response,"list.0.components.no2")` (see [demo file](/tests/CityTraQ%20demo.pie))

![demo](/tests/demo1.gif)
