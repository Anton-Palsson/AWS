# AWS IoT Core HUM/TEMP Sensor Projekt

Detta projekt övervakar temperatur och luftfuktighet med hjälp av en ESP32-enhet. Systemet använder AWS-tjänster för att hantera datainsamling, bearbetning, lagring och aviseringar. Användargränssnittet tillhandahålls via en React-frontend byggd med AWS Amplify.

Use Case: Att från mitt hem mäta inhomhustemperaturen och fuktigheten, spara detta i Dynamo för att sedan kunna skicka det till telegram för att få en notis så att jag även när jag inte är hemma kan ta reda på temp/hum samt få en överblick på datan i en Amplify frontend. 

---

## Arkitekturöversikt

### Komponenter

1. **ESP32 med DHT temperatur- och fuktighetssensor**:
   - Samlar in temperatur- och luftfuktighetsdata från omgivningen.
   - Publicerar datan till AWS IoT Core med MQTT-protokollet.

2. **AWS IoT Core**:
   - Fungerar som en central hubb för att ta emot telemetridata från ESP32.
   - Bearbetar inkommande MQTT-meddelanden och triggar regler baserade på meddelandets innehåll.

3. **AWS Rules Engine**:
   - Dirigerar bearbetade meddelanden till olika AWS-tjänster, såsom DynamoDB och S3.

4. **DynamoDB**:
   - Lagrar telemetridata för sökningar och analys.

5. **S3 Bucket**:
   - Lagrar bearbetad eller aggregerad data för arkivering eller vidare analys. Behövs nödväntigvis 

6. **Amplify React-frontend**:
   - Hämtar data via ett HTTP GET API som körs på AWS Lambda.
   - Visar realtids- och historisk data för användaren.

7. **Amazon EventBridge**:
   - Triggar händelser baserade på specifika regler eller villkor (t.ex. temperaturtröskelvärden).
   - Skickar notifikationer eller larm.

8. **AWS Lambda**:
   - Hanterar inkommande HTTP-begäranden från Amplify-frontenden.
   - Gör HTTP GET-begäranden till tredjeparts-API:er eller andra backend-tjänster.

9. **Telegram Bot Integration**:
   - Skickar larm eller notifikationer till en Telegram-chatt baserat på definierade triggrar.

---

## Arbetsflöde

1. **Datainsamling**:
   - ESP32 samlar in temperatur- och luftfuktighetsdata från sensorer.
   - Datan skickas till AWS IoT Core via MQTT.

2. **Datarouting**:
   - AWS IoT Core använder Rules Engine för att:
     - Spara data i DynamoDB för sökningar.
     - Lagra rå- eller bearbetad data i en S3-bucket för säkerhetskopiering eller analys.

3. **Frontend-integration**:
   - Amplify React hämtar telemetridata via en Lambda-funktion som exponerar ett HTTP GET-API.
   - Visar datan i ett användarvänligt gränssnitt.

4. **Notifikationssystem**:
   - Amazon EventBridge lyssnar efter specifika villkor (t.ex. hög temperatur).
   - Triggar en Lambda-funktion som skickar notifikationer via en Telegram Bot.

---

## Använda tjänster

| Tjänst               | Syfte                                       |
|-----------------------|---------------------------------------------|
| **ESP32**            | Insamling av sensordata och MQTT-publicering |
| **AWS IoT Core**     | Central hubb för IoT-data                   |
| **DynamoDB**         | Lagring av telemetridata                   |
| **S3 Bucket**        | Arkivering av data                         |
| **Amplify React**    | Användargränssnitt för datavisualisering    |
| **EventBridge**      | Regelbaserad händelsehantering             |
| **AWS Lambda**       | Backend-bearbetning för API och notifikationer |
| **Telegram Bot**     | Leverans av notifikationer                 |

---

## Huvudfunktioner

- **Realtidsövervakning**: Samlar in och visar aktuella temperatur- och luftfuktighetsdata.
- **Dataarkivering**: Lagrar historisk data i DynamoDB och S3.
- **Händelsedrivna larm**: Skickar larm via Telegram baserat på specifika villkor.
- **Skalbar frontend**: Ett React-baserat gränssnitt för att visualisera data.

---

## Implementeringssteg

1. **Konfigurera ESP32**:
   - Ladda upp firmware till ESP32 för att skicka data via MQTT till AWS IoT Core.

2. **Konfigurera AWS IoT Core**:
   - Skapa IoT Thing och ladda upp certifikat.
   - Definiera regler för att dirigera meddelanden till DynamoDB, S3 eller EventBridge.

3. **Distribuera Lambda-funktioner**:
   - Utveckla och distribuera Lambda-funktioner för:
     - Databearbetning.
     - Frontend-API.
     - Telegram-notifikationer.

4. **Skapa Amplify-app**:
   - Bygg en React-app med AWS Amplify.
   - Integrera appen med API:et för att hämta data.

5. **Konfigurera EventBridge**:
   - Definiera regler för specifika telemetriförhållanden.

6. **Testa och övervaka**:
   - Validera arbetsflödet från början till slut och säkerställ dataintegritet.
   - Övervaka larm och notifikationer via Telegram.

---

## Framtida förbättringar

- **Integration av maskininlärning**:
  - Använd AWS SageMaker för prediktiv analys baserat på historisk data.
- **Stöd för flera sensorer**:
  - Utöka stödet till fler sensorer och enheter.
- **Anpassade larm**:
  - Låt användare konfigurera personliga tröskelvärden för notifikationer.

---

## Diagram

![Arkitekturdiagram](AWS%20Architecture.png)

---

## Licens

Detta projekt är licensierat under [Ditt licensnamn].
