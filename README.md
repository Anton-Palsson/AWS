# AWS IoT Core HUM/TEMP Sensor Projekt

Detta projekt syftar till att skapa en robust IoT-lösning för övervakning av inomhustemperatur och luftfuktighet. Med hjälp av ESP32-enheter och AWS-molntjänster erbjuder lösningen säker och skalbar hantering av data. Användare får tillgång till en användarvänlig React-baserad frontend för visualisering, samt ett notifieringssystem via Telegram som håller dem uppdaterade vid avvikelser. Lösningen är designad för att möta både tekniska och användarbehov, med hög säkerhet och stöd för framtida expansion.

---

## Arkitekturöversikt
![Systemarkitektur](Pictures/AWS%20Architecture.png)


### Komponenter och Funktioner

1. **ESP32 med DHT-sensor**:
   - Insamling av temperatur- och luftfuktighetsdata från omgivningen.
   - Kommunikation med AWS IoT Core via MQTT för säker och tillförlitlig dataöverföring.
     ![Systemarkitektur](Pictures/ESP32%20DHT%20Breadboard.png)

2. **AWS IoT Core**:
   - Central hubb för att hantera datainsamling från flera IoT-enheter.
   - Stödjer skalbar tillväxt för fler sensorer och ökande datavolymer.

3. **AWS Rules Engine**:
   - Hanterar och dirigerar dataflöden till olika tjänster baserat på regler.
     ![Systemarkitektur](Pictures/Rule.png)

4. **DynamoDB**:
   - Lagrar sensordata för snabb åtkomst och sökbarhet.
   - Passar för lösningar som kräver hög tillgänglighet och skalbarhet.
     ![Systemarkitektur](Pictures/dynamodb.png)
     
  
5. **S3 Bucket**:
   - Lagrar rå sensordata för långsiktig lagring och säkerhetskopiering.
   - Idealisk för lösningar som kräver skalbar och kostnadseffektiv lagring av stora datamängder.
     ![Systemarkitektur](Pictures/s3.png)

6. **AWS Lambda**:
   - Exponerar API:er för frontend och bearbetar inkommande data.
   - Hanterar notifieringar genom integration med Telegram.
     ![Systemarkitektur](Pictures/lambda.png)

7. **EventBridge**:
   - Triggar lambda baserat på specifika händelser, klockslag eller tröskelvärden.
     ![Systemarkitektur](Pictures/eventbridge.png)

8. **AWS Amplify med React**:
   - Användargränssnitt för att visa realtids- och historiska data.
   - Flexibel visualisering som stöder både grafer och tabeller.
     ![Systemarkitektur](Pictures/Frontend.png)

9. **Telegram Bot**:
   - Ger användaren omedelbara notifieringar vid avvikelser, events eller kritiska händelser.
     ![Systemarkitektur](Pictures/Telegram%20Notis.png)

---

## Arbetsflöde och Skalbarhet

1. **Datainsamling och kommunikation**:
   - ESP32 samlar kontinuerligt in temperatur- och luftfuktighetsdata.
   - Publicerar datan till AWS IoT Core via MQTT, vilket möjliggör säker och stabil överföring även vid nätverksvariationer.

2. **Datalagring och hantering**:
   - DynamoDB används för att lagra sensordata med snabb åtkomst dvs 'Hot Storage'.
   - Rådata kan också arkiveras i en S3-bucket för långsiktig lagring och aggregerad analys dvs 'Warm Storage'.

3. **Visualisering och analys**:
   - Frontenden byggd med AWS Amplify och React erbjuder en skalbar lösning för att visa både realtids- och historiska data.
   - Möjligheten att använda både direktdata och aggregerade data säkerställer flexibilitet för olika användningsfall.

4. **Notifieringar och säkerhet**:
   - EventBridge triggar notifieringar vid fördefinierade tröskelvärden, till exempel för hög temperatur.
   - Med Telegram-integration kan användaren omedelbart informeras om avvikelser.
   - Säkerhet hanteras genom krypterad kommunikation, certifikathantering och rollbaserad åtkomstkontroll.

---

## Use Case

Lösningen är designad för att möta behovet av säker och pålitlig övervakning av lägenhetens temperatur och luftfuktighet:

- **Utgångspunkt i behov och användning**:
   - Systemet levererar realtidsdata och historiska analyser för att ge en tydlig överblick över inomhusklimatet.
   - Telegram-notifieringar skickas regelbundet för att hålla användaren uppdaterad med aktuell temperatur och fuktighet, oavsett var hen befinner sig.

- **Skalbar och säker infrastruktur**:
   - Lösningen är framtidssäker och kan enkelt skalas för att inkludera fler sensorer och användare.
   - Säkerhet är en kärnfunktion och tillämpas genom krypterad kommunikation, certifikathantering och rollbaserad åtkomstkontroll genom AWS.

- **Flexibel datavisualisering**:
   - Realtidsdata ger direkt insikt i aktuella förhållanden, medan historiska data kan användas för att identifiera trender över tid.
   - DynamoDB möjliggör snabb dataåtkomst för analyser, medan S3 används för kostnadseffektiv lagring av stora datamängder och aggregerad analys.

---

## Framtida Utvecklingsmöjligheter

1. **Prediktiv analys med maskininlärning**:
   - Historisk data kan analyseras med AWS SageMaker för att förutse trender eller mönster i temperatur och luftfuktighet.

2. **Utökning till fler enheter**:
   - Lösningen kan skalas för att inkludera fler sensorer och datatyper, exempelvis CO2-nivåer eller ljusmätningar.

3. **Avancerade notifieringar**:
   - Möjligheten att anpassa notifieringar baserat på specifika gränsvärden och preferenser för varje användare.

4. **Integrering med externa system**:
   - Export av data till externa verktyg som Power BI eller Google Sheets för ytterligare analys och rapportering.

---

## Sammanfattning

Projektet kombinerar säkerhet, skalbarhet och användarvänlighet för att skapa en tillförlitlig IoT-lösning. Med regelbundna Telegram-notifieringar och en skalbar design är systemet väl lämpat för både nuvarande behov och framtida utvecklingsmöjligheter. Denna lösning erbjuder en robust och flexibel plattform för övervakning och analys av inomhusklimat.


