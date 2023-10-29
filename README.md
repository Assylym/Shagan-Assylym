import java.util.Scanner;import org.json.JSONObject;
import org.json.JSONArray;import org.json.JSONException;
import java.io.IOException;import java.net.URL;
import java.nio.charset.Charset;
public class WeatherApp {
private static String readJsonFromUrl(String url) throws IOException, JSONException {
   try (java.io.InputStream is = new URL(url).openStream()) {         
   java.util.Scanner scanner = new java.util.Scanner(is, Charset.forName("UTF-8").name());
   String jsonString = scanner.useDelimiter("\\A").next();          
   scanner.close();
   return jsonString;        }
  }
    public static void main(String[] args) {      
        Scanner scanner = new Scanner(System.in);
        System.out.print("Введите ваш город: ");      
        String place = scanner.nextLine();
        System.out.print("Введите код вашей страны: ");   
        String country = scanner.nextLine();
        String countryAndPlace = place + ", " + country;
        String apiKey = "1ac243558e0502f0067669513e9ae497";    
        String apiUrl = "http://api.openweathermap.org/data/2.5/weather?q=" + countryAndPlace + "&appid=" + apiKey;
        //This is the main method of the program, where execution begins.
It starts by creating a Scanner for user input and then prompts the user to enter a city and country.
The user input is combined into countryAndPlace, and the OpenWeatherMap API URL is constructed with the API key.//
        try {
            String json = readJsonFromUrl(apiUrl);       
            JSONObject jsonObject = new JSONObject(json);
            JSONObject weather = jsonObject.getJSONArray("weather").getJSONObject(0);      
            JSONObject main = jsonObject.getJSONObject("main");
            JSONObject wind = jsonObject.getJSONObject("wind");
            String status = weather.getString("description");         
            double temp = main.getDouble("temp") - 273.15;
            int humidity = main.getInt("humidity");     
            double windSpeed = wind.getDouble("speed");
            //Inside a try-catch block, it makes an HTTP request to the OpenWeatherMap API using the apiUrl.
It reads the JSON response into the json string.
The JSON response is then parsed using the JSONObject class to extract weather information such as status, temperature, humidity, and wind speed.//
            System.out.println("В городе " + place + " сейчас " + status);
            System.out.println("Температура " + Math.round(temp) + " градусов по Цельсию");    
            System.out.println("Влажность составляет " + humidity + "%");
            System.out.println("Скорость ветра " + windSpeed + " метров в секунду");      
            } catch (IOException | JSONException e) {
            e.printStackTrace();        }
    }}
