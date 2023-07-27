# QA-Engineer-InternAssignment
import requests

API_URL = "https://samples.openweathermap.org/data/2.5/forecast/hourly?q=London,us&appid=b6907d289e10d714a6e88b30761fae22"

def get_weather_data():
    response = requests.get(API_URL)
    return response.json()

def get_weather_by_date(weather_data, date):
    for forecast in weather_data['list']:
        if date in forecast['dt_txt']:
            return forecast['main']['temp']
    return None

def get_pressure_by_date(weather_data, date):
    for forecast in weather_data['list']:
        if date in forecast['dt_txt']:
            return forecast['main']['pressure']
    return None

def main():
    weather_data = get_weather_data()


    while True:
        print("\nOptions:")
        print("1. Get weather")
        print("2. Get Wind Speed")
        print("3. Get Pressure")
        print("0. Exit")
choice = input("Enter your choice: ")


        if choice == "1":
           date = input("Enetr the date(YYYY-MM-DD HH:MM:SS): ")
           temperature = get_weather_by_date(weather_data, date)
           if temperature:
               print(f"Temperature on {date}: {temperature}°C")
           else:
               print("Date not found in the forecast.")


        elif choice == "2":
            date = input("Enter the date (YYYY-MM-DD HH:MM:SS): ")
            wind_speed = get_wind_speed_by_date(weather_data, date)
            if wind_speed:
                print(f"Wind Speed on {date}: {wind_speed} m/s")
            else:
                print("Date not found in the forecast.")



        elif choice == "3":
            date = input("Enter the date (YYYY-MM-DD HH:MM:SS): ")
            pressure = get_pressure_by_date(weather_data, date)
            if pressure:
                print(f"Pressure on {date}: {pressure} hPa")
            else:
                print("Date not found in the forecast.")

        elif choice == "0":
            print("Exiting the program.")
            break

        else:
            print("Invalid choice. Please try again.")

if __name__ == "__main__":
    main()
        
                
                
