# Shagan-Assylym
import org.json.JSONObject;
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.net.HttpURLConnection;
import java.net.URL;

public class WeatherApp {
    public static void main(String[] args) {
        try {
            String apiKey = "Ваш_API_ключ";
            String city = "Ваш_город";
            String date = "2023-10-28";

            String apiUrl = "http://api.openweathermap.org/data/2.5/forecast?q=" + city + "&appid=" + apiKey;
            URL url = new URL(apiUrl);

            HttpURLConnection connection = (HttpURLConnection) url.openConnection();
            connection.setRequestMethod("GET");


            BufferedReader reader = new BufferedReader(new InputStreamReader(connection.getInputStream()));
            StringBuilder response = new StringBuilder();
            String line;

            while ((line = reader.readLine()) != null) {
                response.append(line);
            }
            reader.close();
            JSONObject json = new JSONObject(response.toString());

            System.out.println("Погода в городе " + city + " на " + date + ":");


        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
