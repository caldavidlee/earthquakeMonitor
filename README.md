# 🚨 San Francisco Earthquake Monitor

A real-time earthquake monitoring web application that tracks seismic activity within 200km of San Francisco using data from the USGS (United States Geological Survey) API.

## Features

- **Real-time Monitoring**: Fetches earthquake data from USGS every 30 seconds
- **Interactive Map**: Leaflet-powered map showing earthquake locations with color-coded markers
- **Geographic Filtering**: Focuses on earthquakes within 200km radius of San Francisco
- **Beautiful UI**: Modern, responsive interface with animated alerts
- **Browser Notifications**: Desktop notifications for significant earthquakes (magnitude 3.0+)
- **Detailed Information**: Shows magnitude, location, depth, distance from SF, and felt reports
- **Haversine Distance Calculation**: Accurate distance calculations between earthquake epicenters and San Francisco

## How It Works

### Backend (`main.py`)
- **Flask Web Server**: Serves the web interface and API endpoints
- **USGS API Integration**: Queries the USGS FDSN Event Web Service for recent earthquakes
- **Distance Filtering**: Uses the Haversine formula to calculate precise distances from San Francisco (37.7749°N, 122.4194°W)
- **Data Processing**: Filters earthquakes by magnitude (2.0+) and distance (≤200km), then sorts by magnitude

### Frontend (`templates/index.html`)
- **Interactive Map**: Leaflet.js map with San Francisco marker, 200km radius circle, and color-coded earthquake markers
- **Dynamic Updates**: Auto-refreshes earthquake data and map every 30 seconds
- **Visual Alerts**: Displays animated alerts for significant earthquakes (magnitude 3.0+)
- **Color-Coded Display**: Earthquakes color-coded by magnitude severity (green to dark red)
- **Interactive Elements**: Clickable map markers with popups, hover effects, manual refresh button, and USGS links

## Setup Instructions

### Prerequisites
- Python 3.12+
- WSL Ubuntu (for Windows users) or any Unix-based system

### Environment Setup

1. **Create Virtual Environment**:
```bash
uv venv
```

2. **Check if pip is in your venv**:
```bash
which pip
```

### ESSENTIAL CODE TO HAVE PIP in your VENV

If pip is not available in your virtual environment, run:

```bash
python3 -m ensurepip --upgrade
python -m pip install --upgrade pip
```

### Installation

3. **Install Dependencies**:
```bash
python -m pip install -r requirements.txt
```

This installs:
- Flask 3.0.0 (web framework)
- Requests 2.31.0 (HTTP library for API calls)
- Twilio 8.10.0 (optional, for SMS alerts)

### Running the Application

4. **Start the Server**:
```bash
python main.py
```

The application will be accessible at `http://localhost:8080`

## API Endpoints

### `GET /`
Serves the main web interface

### `GET /api/earthquakes`
Returns JSON data of recent earthquakes:
```json
{
  "count": 3,
  "earthquakes": [
    {
      "magnitude": 3.2,
      "place": "5km NE of San Francisco, CA",
      "time": "2025-11-04 14:23:15 UTC",
      "distance_km": 45.3,
      "depth_km": 8.2,
      "latitude": 37.82,
      "longitude": -122.35,
      "url": "https://earthquake.usgs.gov/...",
      "alert": null,
      "felt": 12,
      "tsunami": 0
    }
  ],
  "last_updated": "2025-11-04 14:25:30 UTC"
}
```

## Configuration

Key parameters in `main.py`:
- `SF_LAT = 37.7749` - San Francisco latitude
- `SF_LON = -122.4194` - San Francisco longitude  
- `RADIUS_KM = 200` - Alert radius in kilometers
- `minmagnitude = 2.0` - Minimum earthquake magnitude to display

## Technologies Used

- **Backend**: Python, Flask
- **API**: USGS FDSN Event Web Service
- **Frontend**: HTML5, CSS3, Vanilla JavaScript
- **Mapping**: Leaflet.js 1.9.4 with OpenStreetMap tiles
- **Math**: Haversine formula for distance calculations

## Data Source

Earthquake data is provided by the [United States Geological Survey (USGS)](https://earthquake.usgs.gov/) Earthquake Hazards Program.