# G-Weather-Forecast
G-Weather-Forecast is a simple web application that allows users to search and display current weather information and forecasts for the next four days.

## Detail
+ Frontend: ReactJS, libs (Axios, Material UI, Boostrap). [https://github.com/TaiTai3006/Weather-Forecast-client](https://github.com/TaiTai3006/Weather-Forecast-client)
+ Backend: Django. [https://github.com/TaiTai3006/Weather-Forecast-server](https://github.com/TaiTai3006/Weather-Forecast-server)
+ API: [Weather API](https://weatherapi.com/), [db-ip](https://db-ip.com/api/), [ninjas](https://api-ninjas.com/)

## Feature

+ Search for a city or country and display weather information:
  + Show the weather includes temperature, wind speed, humidity... for present day.
  + Show forecast 4 days later.

<img width="1514" alt="Ảnh màn hình 2024-07-27 lúc 21 36 09" src="https://github.com/user-attachments/assets/7e0f4bb8-cad9-4b98-ab57-588a7334b874">

+ Save temporary weather information history and allow display again during the day: All searched keywords will be displayed in the input suggestion bar, with data temporarily stored in cookies for one day.

<img width="532" alt="Ảnh màn hình 2024-07-27 lúc 21 12 10" src="https://github.com/user-attachments/assets/d87a275e-f3e3-4aa0-b6b3-574af187f21e">
<img width="834" alt="Ảnh màn hình 2024-07-27 lúc 21 12 42" src="https://github.com/user-attachments/assets/c99ea4d4-10c6-45c3-9f57-5634e0d54a51">

+ There is a function to register and unsubscribe to receive daily weather forecast information via email address.

<img width="1060" alt="Ảnh màn hình 2024-07-27 lúc 21 15 25" src="https://github.com/user-attachments/assets/f953a97f-5a26-4707-9df0-55f9fac22f38">
<img width="539" alt="Ảnh màn hình 2024-07-27 lúc 21 38 39" src="https://github.com/user-attachments/assets/64351c42-4b4c-4b08-88f4-db773650d9b9">

+ The G-Weather-Forecast application allows retrieving the user's current location to display the weather for that location. **If the user does not grant permission to use their location in the browser, the system will use two APIs, db-ip and ninjas, to determine the user's approximate location based on their IP address**.

```python
def getLocationByCityName(name):
    print(name)
    try:
        url = f'https://api.api-ninjas.com/v1/geocoding?city={name}'
        headers = {
            'X-Api-Key': 'sycEOmug3GpUajiEHTFeUw==pSeXtHtQGiOYhBHS',
        }

        response = requests.get(url, headers=headers)
        # response.raise_for_status() 

        print(response.json())

        data = response.json()
        if data:
            coordinates = {
                'lat': data[0]['latitude'],
                'lng': data[0]['longitude']
            }
            return f'{coordinates["lat"]},{coordinates["lng"]}'
        else:
            print("No data found for the city.")
            return None
    except requests.exceptions.HTTPError as http_err:
        print(f"HTTP error occurred: {http_err}")
    except Exception as err:
        print(f"Other error occurred: {err}")

@api_view(['GET'])
def getLocationByIP(request):
    cityname = requests.get('https://api.db-ip.com/v2/free/self').json()
    print(cityname)
    return Response(getLocationByCityName(cityname['city']))
```

+ Responsive design (desktops, tablets & mobile phones).

<img width="1512" alt="Ảnh màn hình 2024-07-27 lúc 21 48 25" src="https://github.com/user-attachments/assets/d8716e89-9a21-4b05-8dea-6f2314cad9a8">
<img width="512" alt="Ảnh màn hình 2024-07-27 lúc 21 48 40" src="https://github.com/user-attachments/assets/1367660b-df15-41e5-94bb-976b2432948b">
<img width="317" alt="Ảnh màn hình 2024-07-27 lúc 21 48 49" src="https://github.com/user-attachments/assets/e91b90f4-15fb-44d8-a631-b0c992fd5221">

## Build Notes

``` bash
# Clone frontend
git clone [https://github.com/LuxionRob/weTube.git](https://github.com/TaiTai3006/Weather-Forecast-client.git)
# Install dependencies
npm i
# Run
npm start
# Or build
npm run build


# Clone frontend
git clone [https://github.com/TaiTai3006/Weather-Forecast-server.git](https://github.com/TaiTai3006/Weather-Forecast-server.git)
# Run
python manage.py runserver

```


## Wed demo
[https://weather-woad-psi.vercel.app/](https://weather-forecast-client-nine.vercel.app/)

