# 🌦 Real-Time Weather Analysis Dashboard

# 📌 Introduction
This project is an **interactive real-time weather dashboard** built using **Power BI**, fetching live weather data through an API. It provides **up-to-date weather insights** such as temperature, humidity, wind speed, UV index, air quality, and precipitation probability. The dashboard also includes **7-day weather forecasts**, **air pollution analysis**, and **sunrise/sunset timings** for multiple cities.

**Key Highlights**
- **Live Data Integration** – Weather information auto-updates from API in real-time.  
- **Multi-City Comparison** – Easily switch between cities like Bangkok, Chiang Mai, and Nonthaburi.  
- **Visual Forecasts** – 7-day temperature trends and rain probability charts.  
- **Air Quality Monitoring** – Displays PM levels, NO₂, CO, SO₂, and O₃ values.  
- **User-Friendly Interface** – Dark-themed, visually appealing, and mobile-friendly design.

---

## 🛠 Problem Statement
Weather conditions have a direct impact on **daily life, travel, agriculture, public safety, and environmental health**.  
However, most weather platforms provide **scattered, non-interactive, or delayed updates**, making it difficult for individuals and organizations to:

- Get **accurate real-time weather data** in one place.  
- Monitor **air quality** for health and safety decisions.  
- Track **temperature trends and rainfall probability** for planning outdoor activities or agricultural operations.  
- Compare **multi-city weather** quickly for travel or logistics purposes.  
- Anticipate weather-related **risks and disruptions** before they occur.

This lack of **consolidated, visual, and actionable weather insights** often leads to poor decision-making and increased risks in sectors like transportation, tourism, event planning, and public health.Our **Real-Time Weather Analysis Dashboard** aims to bridge this gap by providing an **interactive, data-rich, and continuously updated weather visualization tool** that empowers users to make **informed, timely decisions** based on reliable data.

## 🎯 Objectives
- Provide **real-time, accurate** weather updates from reliable API sources.  
- Offer **multi-city comparisons** to help with travel and logistics planning.  
- Visualize **7-day weather forecasts** for better preparedness.  
- Display **air quality metrics** to raise environmental and health awareness.  
- Create a **visually appealing, user-friendly** dashboard for easy interpretation of complex data.

## 📊 Features
- **Real-time data integration** using API.  
- **Multi-location weather monitoring**.  
- **Forecast visualization** (temperature trends & rain probability).  
- **Air quality analysis** (PM10, PM2.5, NO₂, CO, SO₂, O₃).  
- **Sunrise and sunset timings**.  
- **Dark-mode modern UI** for better readability.

---

# Data Sourcing

The Dataset used for this analysis was taken from :link:[WeatherAPI](https://www.weatherapi.com/)

For current weather data use, Build the API URL:
   ```bash
   https://api.weatherapi.com/v1/current.json?key=YOUR_API_KEY&q=CITY_NAME
   ```
Replace `YOUR_API_KEY` with your actual API key and `CITY_NAME` with the desired location.

---

# Data Visualization

Data visualization for the datasets was done in Microsoft Power BI Desktop,

![dashboard github](https://github.com/Aryan-chand/Customer-Retention-Analysis/blob/main/customer%20retention_pg1.png)

### Key Performance Indicators and Metrics:

The measure used in visualization are:

- **Calculated measures**
    - For Current Temprature = `Curr_Temp_C = SUM('Current'[current.temp_c])&" °C"`
    - For Forecast Temprature = `For_Temp_C = AVERAGE('Forecast_Day'[forecast.forecastday.day.avgtemp_c])&" °C"`
    - For Current Humidity = `Humidity = SUM('Current'[current.humidity])&" %"`
    - For Current Precipitation = `Precipitation = SUM('Current'[current.precip_mm])&" mm"`
    - For Current Rain chance = `Rain_Chance = 100 - SUM(Forecast_Day[forecast.forecastday.day.daily_chance_of_rain])`
    - For Current Visibility = `Vis = SUM('Current'[current.vis_km])&" Km"`
    - For Current Wind Speed = `Wind_Speed = SUM('Current'[current.wind_kph])&" Kph"`
    - Last Updated Date = `Last_Updated_Date_Curr = "Last Updated, "&FORMAT(FIRSTNONBLANK('Current'[current.last_updated],""),"dd mmm yyyy")`
    
- **Format measures**
    - AQI Color Indicators = `AQI Color TEMPLATE =
        VAR AQI = ROUND(SELECTEDVALUE('Current'[current.air_quality.COLUMN_NAME]),0)
        RETURN
        SWITCH(
        TRUE(),
        AQI <= 50, "#43d946",
        AQI <= 100, "#fff570",
        AQI <= 150, "#ff9800",
        AQI <= 200, "#d99343",
        AQI <= 300, "#ff5b0f",
        "#d95243")`

---

## ⚙️ Tools & Technologies Used
- **Power BI** – Data visualization and dashboard creation  
- **WeatherAPI.com** – Live weather data  
- **JSON API Integration** – For fetching real-time weather and air quality information

---

## 🚀 How to Use
1. Get your API key from **WeatherAPI.com**.  
2. Replace `YOUR_API_KEY` in the API endpoint with your key.  
3. In Power BI, use **Get Data → Web** and paste the endpoint to pull JSON.  
4. Transform fields in **Power Query** (expand nested records, set data types).  
5. Build visuals (cards, line charts, bar charts, gauges) as in the preview.  
6. Configure **scheduled refresh** in Power BI Service (optional) for auto-updates.

---

## 📌 Future Improvements
- Add **hourly forecasts** for more granular data.  
- Integrate **severe weather alerts**.  
- Enable a **mobile app version** for on-the-go access.  
- Add **historical weather analysis** features.

---

# :link: Shareable Link 
You can interact and have fun with the dashboard here:

[Microsoft PowerBI](https://app.powerbi.com/groups/me/reports/67c6a7b3-7a00-4474-8d5e-64b531ab0ae1/ReportSection515eb6e3c03bdcc7c490?experience=power-bi)
