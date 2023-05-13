# Birt_REST_API_Json_parse
Create "New Data Source" leave empty.

Create "Data Set" and go tab "script"
Create Output columns 

Symbol
bidRate
askRate

Script Open :
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

if (count >= Number(Object.keys(json).length))
return false;
row["symbol"] = json[count].symbol;
row["bidRate"] = json[count].bidRate;
row["askRate"] = json[count].askRate;
count++;
return true;
