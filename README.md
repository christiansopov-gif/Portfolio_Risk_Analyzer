# Portfolio Risk Analyzer

## Projektbeskrivning

Portfolio Risk Analyzer är en webbapplikation utvecklad i Python och Streamlit inom kursen Prompt Engineering och generativ AI för utvecklare.

Appen analyserar en fiktiv fondportfölj och använder OpenAI API för att tolka portföljens risker.

Grundprincip: Python utför de finansiella beräkningarna medan AI tolkar resultaten och genererar analyser och rapporter.

## Funktioner

Appen innehåller:

- Inläsning och validering av CSV-filer.
- Beräkning av portföljvärde och fondvikter.
- Beräkning av land- och regionexponering.
- Beräkning av sektorexponering.
- Identifiering av koncentrationsrisk.

Tre separata AI-funktioner:

1. **AI-riskanalys:** Identifierar möjliga koncentrationsrisker i portföljen.
2. **Förslag på riskminskning:** Ger tre möjliga åtgärder för att minska riskkoncentration.
3. **AI-genererad portföljrapport:** Skapar en sammanfattande rapport som kan laddas ner som textfil.

## Teknik och bibliotek

- Python 3.13
- Streamlit – webbgränssnitt
- pandas – datainläsning och beräkningar
- OpenAI API – AI-genererade analyser
- python-dotenv – hantering av API-nyckeln

AI-modell: `gpt-4.1-mini`

## Installation

1. Installera Python.
2. Packa upp projektets zip-fil.
3. Öppna projektmappen i VS Code eller en terminal.
4. Skapa en virtuell Pythonmiljö:

```powershell
python -m venv .venv
```

5. Installera projektets bibliotek:

```powershell
.\.venv\Scripts\python.exe -m pip install -r requirements.txt
```

6. Skapa en fil med namnet `.env` i projektmappen, med samma variabelnamn som i `.env.example`:

```dotenv
OPENAI_API_KEY=din_egen_api_nyckel
```

En egen giltig OpenAI API-nyckel med tillgängliga API-krediter krävs för AI-funktionerna.

## Starta appen

Kör följande kommando från projektmappen:

```powershell
.\.venv\Scripts\python.exe -m streamlit run app.py
```

Öppna den lokala adress som visas i terminalen, exempelvis:

`http://localhost:8501`

Portnumret kan variera.

## CSV-filer

Fiktiva testdata finns i mappen `data/`.

**portfolio.csv**

- `Fond` – fondens namn
- `Varde_Sek` – investerat belopp i SEK

**exposures.csv**

- `Fond` – fondens namn
- `Land` – land eller region
- `Sektor` – ekonomisk sektor
- `Vikt %` – exponeringens procentuella vikt inom fonden

Varje fonds exponeringsvikter ska summera till 100 %. Fondnamnen måste matcha mellan CSV-filerna.

## Säkerhet och felhantering

Applikationen innehåller flera skydd:

- API-nyckeln lagras i `.env`, inte i Pythonkoden.
- Promptarna skiljer instruktioner från portföljdata med särskilda avgränsare.
- Python begränsar mängden data som kan skickas till AI.
- Textfält kontrolleras mot vissa misstänkta instruktionsfraser och för långa värden.
- CSV-filer valideras innan beräkningarna utförs.
- Fel vid API-anrop hanteras med begripliga meddelanden.

Skydden minskar vissa risker men kan inte garantera att alla promptinjektioner upptäcks.

## Tester

Följande tester har genomförts under utvecklingen:

- Verifiering av portföljvikter och totala exponeringar.
- Test med felaktiga exponeringsvikter.
- Test av begränsning av datamängd.
- Test av misstänkt instruktion i ett CSV-fondnamn.
- Test av saknad API-nyckel.
- Test av samtliga tre AI-funktioner.

## Begränsningar

Appen använder fiktiva data och hämtar inte automatiskt fondinformation från Avanza eller andra dataleverantörer.

Analysen omfattar fondvikter och förenklade exponerings- och koncentrationsmått. Den beräknar inte volatilitet, Value at Risk, korrelationer eller avkastningsprognoser.

AI-genererade svar kan innehålla felaktiga tolkningar och behöver granskas av användaren.

**Appen är ett utbildningsprojekt och ska inte användas som personlig investeringsrådgivning.**