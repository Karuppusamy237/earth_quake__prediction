# earth_quake__prediction
for naan mudhalavan
import requests

def get_earthquake_data():
    # Define the URL for the USGS Earthquake API
    url = "https://earthquake.usgs.gov/fdsnws/event/1/query"

    # Define parameters for the API request
    params = {
        "format": "geojson",
        "starttime": "2023-01-01",
        "endtime": "2023-12-31",
        "minmagnitude": 4.0,  # Adjust the minimum magnitude as needed
        "orderby": "time",
    }

    # Send an HTTP GET request to the API
    response = requests.get(url, params=params)

    # Check if the request was successful
    if response.status_code == 200:
        earthquake_data = response.json()
        return earthquake_data
    else:
        print("Error fetching earthquake data")
        return None

def main():
    # Fetch earthquake data
    earthquake_data = get_earthquake_data()

    if earthquake_data:
        # Print information about recent earthquakes
        features = earthquake_data["features"]
        print(f"Found {len(features)} earthquakes in the selected time range:")
        for feature in features:
            properties = feature["properties"]
            magnitude = properties["mag"]
            place = properties["place"]
            time = properties["time"]
            print(f"Magnitude {magnitude} earthquake at {place} on {time}")

if __name__ == "__main__":
    main()
