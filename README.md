# weather-app- 
import requests
import json

def get_weather(api_key, location):
    base_url = "http://api.openweathermap.org/data/2.5/weather"
    params = {
        'q': location,
        'appid': api_key,
        'units': 'metric'  # You can use 'imperial' for Fahrenheit
    }

    try:
        response = requests.get(base_url, params=params)
        data = response.json()

        if response.status_code == 200:
            return data
        else:
            print(f"Error: {data['message']}")
            return None
    except Exception as e:
        print(f"Error: {e}")
        return None

def display_weather(weather_data):
    if weather_data:
        print(f"\nCurrent Weather in {weather_data['name']}, {weather_data['sys']['country']}:")
        print(f"Temperature: {weather_data['main']['temp']}°C")
        print(f"Humidity: {weather_data['main']['humidity']}%")
        print(f"Weather Conditions: {weather_data['weather'][0]['description']}")
    else:
        print("\nUnable to fetch weather data.")

if __name__ == "__main__":
    # Replace 'YOUR_API_KEY' with your OpenWeatherMap API key
    api_key = '289e9dd7f4c47ff8207e565f7ad47bdb'
    
    # Get user input for the location (city or ZIP code)
    location = input("Enter a city or ZIP code: ")

    # Fetch weather data
    weather_data = get_weather(api_key, location)

    # Display weather information
    display_weather(weather_data)
