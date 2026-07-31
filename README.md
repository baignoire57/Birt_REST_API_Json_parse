# Birt_REST_API_Json_parse

Tutoriel : comment consommer une **API REST/JSON** comme source de données dans un rapport **BIRT** (Business Intelligence and Reporting Tools, Eclipse), en utilisant l'API publique de Bittrex (tickers de marchés crypto) comme exemple.

BIRT ne propose pas de connecteur REST/JSON natif simple : ce tutoriel montre comment le faire via une **Scripted Data Source** (JavaScript/Rhino intégré au report designer).

## Étapes

### 1. Créer la Data Source
"New Data Source" → laisser vide.

### 2. Créer le Data Set et ses colonnes de sortie

![Data Set](https://github.com/baignoire57/Birt_REST_API_Json_parse/assets/57708917/911fd0d9-1293-4cbf-979e-62dbd018ce2f)

### 3. Script "Open" — ouverture de la connexion HTTP et parsing du JSON

![Script Open](https://github.com/baignoire57/Birt_REST_API_Json_parse/assets/57708917/783c6c46-8583-4c21-96c8-01125e9c79a4)

```javascript
importPackage(Packages.java.io);
importPackage(Packages.java.net);
var inStream = new URL("https://api.bittrex.com/v3/markets/tickers").openStream();
var inStreamReader = new InputStreamReader(inStream);
var bufferedReader = new BufferedReader(inStreamReader);
var line;
var result = "";
while ((line = bufferedReader.readLine()) != null)
  result += line;
inStream.close();
json = JSON.parse(result);
count = 0;
```

### 4. Script "Fetch" — itération ligne par ligne sur le JSON

![Script Fetch](https://github.com/baignoire57/Birt_REST_API_Json_parse/assets/57708917/fd1f0a9d-084e-4aea-a55f-57212c8f9dce)

```javascript
if (count >= Number(Object.keys(json).length))
  return false;
row["symbol"] = json[count].symbol;
row["bidRate"] = json[count].bidRate;
row["askRate"] = json[count].askRate;
count++;
return true;
```

### 5. Résultat

![Résultat](https://github.com/baignoire57/Birt_REST_API_Json_parse/assets/57708917/cef9bf7f-13da-4801-878d-303a6f172499)
