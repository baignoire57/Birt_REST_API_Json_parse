# Birt_REST_API_Json_parse
Create "New Data Source" leave empty.

Create "Data Set" 

Create Output columns

![image](https://github.com/baignoire57/Birt_REST_API_Json_parse/assets/57708917/911fd0d9-1293-4cbf-979e-62dbd018ce2f)

Symbol
bidRate
askRate

Script Open :

![image](https://github.com/baignoire57/Birt_REST_API_Json_parse/assets/57708917/783c6c46-8583-4c21-96c8-01125e9c79a4)

importPackage(Packages.java.io);
importPackage(Packages.java.net);
var inStream = new 
URL("https://api.bittrex.com/v3/markets/tickers").openStream();
var inStreamReader = new InputStreamReader(inStream);
var bufferedReader = new BufferedReader(inStreamReader);
var line;
var result = "";
while ((line = bufferedReader.readLine()) != null)
result += line;
inStream.close();
json = JSON.parse(result);
count = 0;


Script Fecth :
![image](https://github.com/baignoire57/Birt_REST_API_Json_parse/assets/57708917/fd1f0a9d-084e-4aea-a55f-57212c8f9dce)

if (count >= Number(Object.keys(json).length))
return false;
row["symbol"] = json[count].symbol;
row["bidRate"] = json[count].bidRate;
row["askRate"] = json[count].askRate;
count++;
return true;


Result : 

![image](https://github.com/baignoire57/Birt_REST_API_Json_parse/assets/57708917/cef9bf7f-13da-4801-878d-303a6f172499)
