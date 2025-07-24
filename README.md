# 🌦️ Power BI Real-Time Weather Dashboard using WeatherAPI

Create a real-time, dynamic weather dashboard in **Power BI** using **WeatherAPI** — complete with live temperature, humidity, wind data, and **Air Quality Index (AQI)** indicators.

---

## 📌 Features

* 🔄 Real-time weather data using WeatherAPI
* 📍 Location-based filtering for cities
* 🌡️ Weather indicators: temperature, humidity, wind speed, etc.
* 🧪 Air Quality Index (AQI) color codes, statuses & suggestions
* 🌐 Map visuals and dynamic user interactivity

---

## 🛠️ Prerequisites

Before you begin, make sure you have:

* ✅ A [WeatherAPI.com](https://www.weatherapi.com/) account (Free or Paid)
* ✅ Installed **Power BI Desktop**
* ✅ Basic knowledge of Power BI (data loading, visuals, DAX)

---

## 🔑 Step 1: Get Your API Key

1. Sign up at [WeatherAPI.com](https://www.weatherapi.com/).
2. Go to your profile and **copy your API key**.

---

## 🌐 Step 2: Build the API URL

Use the following URL to fetch **current weather data**:

```bash
https://api.weatherapi.com/v1/current.json?key=YOUR_API_KEY&q=CITY_NAME
```

Replace:

* `YOUR_API_KEY` with your actual API key
* `CITY_NAME` with the location (e.g., London, New York)

---

## 🔗 Step 3: Connect Power BI to WeatherAPI

1. Open **Power BI Desktop**
2. Go to **Home > Get Data > Web**
3. Paste the WeatherAPI URL
4. Click **OK**

---

## 🔄 Step 4: Transform JSON Data in Power Query

1. Expand the `current` record
2. Expand sub-records like `condition`, `air_quality`
3. Rename columns for clarity
4. Click **Close & Apply**

---

## 📊 Step 5: Design the Weather Dashboard

Use visuals like:

* ✅ **Cards** – Temperature, humidity, condition text
* ✅ **Gauges** – Wind speed, pressure
* ✅ **Line/Bar Charts** – Hourly/daily trends
* ✅ **Map Visual** – Plot city locations
* ✅ **Slicers** – Filter data by city

---

## 🎨 Step 6: Add AQI Indicators using DAX

WeatherAPI provides AQI data in the `current.air_quality` object. You can create dynamic indicators using DAX.

### ✅ AQI Color Template

```DAX
AQI Color =
VAR AQI = ROUND(SELECTEDVALUE('Current'[current.air_quality.COLUMN_NAME]), 0)
RETURN
SWITCH(
    TRUE(),
    AQI <= 50, "#43d946",
    AQI <= 100, "#fff570",
    AQI <= 150, "#ff9800",
    AQI <= 200, "#d99343",
    AQI <= 300, "#ff5b0f",
    "#d95243"
)
```

### ✅ AQI Suggestion Template

```DAX
AQI Suggestion =
VAR AQI = ROUND(SELECTEDVALUE('Current'[current.air_quality.COLUMN_NAME]), 0)
RETURN
SWITCH(
    TRUE(),
    AQI <= 50, "Air is clean and healthy",
    AQI <= 100, "Acceptable air quality, stay active",
    AQI <= 150, "Sensitive groups should reduce outdoor time",
    AQI <= 200, "Limit prolonged outdoor exertion",
    AQI <= 300, "Avoid outdoor activity if possible",
    "Stay indoors, wear a mask if outside"
)
```

### ✅ AQI Status Template

```DAX
AQI Status =
VAR AQI = ROUND(SELECTEDVALUE('Current'[current.air_quality.COLUMN_NAME]), 0)
RETURN
SWITCH(
    TRUE(),
    AQI <= 50, "Good",
    AQI <= 100, "Moderate",
    AQI <= 150, "Unhealthy for Sensitive",
    AQI <= 200, "Unhealthy",
    AQI <= 300, "Very Unhealthy",
    "Hazardous"
)
```

> 🔁 Replace `COLUMN_NAME` with your pollutant of interest: `pm2_5`, `no2`, `co`, `o3`, etc.

---

## 💡 Tips

* Keep DAX templates reusable for different pollutants
* Use conditional formatting for color-coded visuals
* Create bookmarks to switch between cities or pollutant views

---

## 📸 Example Preview (Optional)

Add screenshots here showing your dashboard layout and visual elements.

---

## 🎉 Conclusion

Integrating **WeatherAPI** with **Power BI** helps you build smart, responsive dashboards with real-time weather and air quality insights. These DAX patterns make it easy to scale and personalize your reports.

Happy Dashboarding! 🌦️📊


