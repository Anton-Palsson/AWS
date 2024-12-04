# AWS IoT Core HUM/TEMP Sensor Projekt

Detta projekt syftar till att skapa en robust IoT-lösning för övervakning av inomhustemperatur och luftfuktighet. Med hjälp av ESP32-enheter och AWS-molntjänster erbjuder lösningen säker och skalbar hantering av data. Användare får tillgång till en användarvänlig React-baserad frontend för visualisering, samt ett notifieringssystem via Telegram som håller dem uppdaterade vid avvikelser. Lösningen är designad för att möta både tekniska och användarbehov, med hög säkerhet och stöd för framtida expansion.

---

## Arkitekturöversikt
![Systemarkitektur](pictures/AWSArchitecture.png)


### Komponenter och Funktioner

1. **ESP32 med DHT-sensor**:
   - Insamling av temperatur- och luftfuktighetsdata från omgivningen.
   - Kommunikation med AWS IoT Core via MQTT för säker och tillförlitlig dataöverföring.

2. **AWS IoT Core**:
   - Central hubb för att hantera datainsamling från flera IoT-enheter.
   - Stödjer skalbar tillväxt för fler sensorer och ökande datavolymer.

3. **AWS Rules Engine**:
   - Hanterar och dirigerar dataflöden till olika tjänster baserat på regler.

4. **DynamoDB**:
   - Lagrar sensordata för snabb åtkomst och sökbarhet.
   - Passar för lösningar som kräver hög tillgänglighet och skalbarhet.
  
5. **S3 Bucket**:
   - Lagrar rå sensordata för långsiktig lagring och säkerhetskopiering.
   - Idealisk för lösningar som kräver skalbar och kostnadseffektiv lagring av stora datamängder.

6. **AWS Lambda**:
   - Exponerar API:er för frontend och bearbetar inkommande data.
   - Hanterar notifieringar genom integration med Telegram.

7. **EventBridge**:
   - Triggar notifieringar baserat på specifika händelser, klockslag eller tröskelvärden.

8. **AWS Amplify med React**:
   - Användargränssnitt för att visa realtids- och historiska data.
   - Flexibel visualisering som stöder både grafer och tabeller.

9. **Telegram Bot**:
   - Ger användaren omedelbara notifieringar vid avvikelser, events eller kritiska händelser.

---

## Arbetsflöde och Skalbarhet

1. **Datainsamling och kommunikation**:
   - ESP32 samlar kontinuerligt in temperatur- och luftfuktighetsdata.
   - Publicerar datan till AWS IoT Core via MQTT, vilket möjliggör säker och stabil överföring även vid nätverksvariationer.

2. **Datalagring och hantering**:
   - DynamoDB används för att lagra sensordata med snabb åtkomst.
   - Rådata kan också arkiveras i en S3-bucket för långsiktig lagring och aggregerad analys.

3. **Visualisering och analys**:
   - Frontenden byggd med AWS Amplify och React erbjuder en skalbar lösning för att visa både realtids- och historiska data.
   - Möjligheten att använda både direktdata och aggregerade data säkerställer flexibilitet för olika användningsfall.

4. **Notifieringar och säkerhet**:
   - EventBridge triggar notifieringar vid fördefinierade tröskelvärden, till exempel för hög temperatur.
   - Med Telegram-integration kan användaren omedelbart informeras om avvikelser.
   - Säkerhet hanteras genom krypterad kommunikation, certifikathantering och rollbaserad åtkomstkontroll.

---

## Användarcentrerad Design

Lösningen har designats för att möta användarnas behov av säker och pålitlig övervakning:

- **Utgångspunkt i behov och verksamhet**:
   - Fokus ligger på att ge användaren realtidsdata och historiska analyser för att kunna agera på temperatur- eller fuktighetsavvikelser.
   - Telegram-notifieringar möjliggör snabb respons, oavsett var användaren befinner sig.

- **Skalbar och säker infrastruktur**:
   - Lösningen kan enkelt byggas ut för att stödja flera sensorer eller fler användare.
   - Säkerhet är integrerad i alla nivåer, från enhetskommunikation till användaråtkomst.

- **Flexibel datavisualisering**:
   - Historisk data kan analyseras för att upptäcka trender, medan realtidsdata ger omedelbar insikt i aktuella förhållanden.
   - Kombinationen av DynamoDB för snabb dataåtkomst och S3 för långsiktig lagring möjliggör olika analysmetoder.

---

## Framtida Utvecklingsmöjligheter

1. **Prediktiv analys med maskininlärning**:
   - Med AWS SageMaker kan lösningen använda historisk data för att förutse trender och avvikelser.

2. **Utökning till fler enheter**:
   - Skalbarheten i AWS IoT Core och DynamoDB gör det möjligt att integrera fler sensorer och datatyper, till exempel CO2- eller ljusnivåmätare.

3. **Avancerade notifieringar**:
   - Användare kan få möjlighet att definiera egna notifieringsgränser och välja hur de vill bli informerade.

4. **Integrering med externa system**:
   - Export av data till verktyg som Power BI eller Google Sheets kan ge ytterligare analysmöjligheter.

---

## Sammanfattning

Detta projekt kombinerar säkerhet, skalbarhet och användarvänlighet för att skapa en robust IoT-lösning som möter både tekniska och praktiska krav. Med stöd för framtida expansion och avancerade analysmöjligheter är lösningen väl lämpad för att tillgodose både dagens och morgondagens behov.

