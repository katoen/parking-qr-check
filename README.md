# Parking QR-check

Scantool voor stewards aan de inrit van een parking. De steward kiest zijn parking en scant de QR-code van de reservatie. De tool zegt meteen **OK**, **al gebruikt**, **verkeerde parking** of **onbekend**. Elke scan wordt bewaard op het toestel.

- Scantool: `https://katoen.github.io/parking-qr-check/?e=<event>`
- Demo: `https://katoen.github.io/parking-qr-check/?e=demo` (testcodes per parking in `testcodes/`)
- Codelijst maken: `https://katoen.github.io/parking-qr-check/maak-lijst.html`

## Werkwijze per event

1. Exporteer de geldige reservaties uit het reservatieplatform (CSV met minstens een kolom QR-code en een kolom parking).
2. Open `maak-lijst.html`, laad de CSV, kies de kolommen en klik op **Maak codelijst**. Je krijgt `<event>.json`.
3. Zet dat bestand in de map `events/` van deze repository.
4. Stuur de stewards de link `…/?e=<event>`. Ze kiezen hun parking bij de eerste keer openen.

Een rechtstreekse link per parking kan ook: `…/?e=<event>&p=<parking-id>`. De parking-id's staan in het JSON-bestand.

## Wat staat er online

- `events/*.json` bevat **geen codes**, enkel hashes: PBKDF2-SHA256, 100.000 rondes, met een willekeurige salt per event. Uit het bestand kan je geen geldige code afleiden of een QR namaken.
- De codes uit de CSV verlaten de browser niet bij het maken van de lijst.
- Scans en de log staan enkel in de browser van het toestel (localStorage), per event en per parking. Er is geen server en geen centrale databank.

## Beperkingen

- Eén steward per parking. Twee toestellen op dezelfde parking weten niet van elkaars scans.
- Browsergegevens wissen of een privévenster gebruiken = log kwijt. Exporteer de log na het event.
- De hashing beschermt de lijst zolang de codes zelf lang en willekeurig zijn. Korte, voorspelbare codes zijn met genoeg rekenkracht te raden.
- `voorbeeld-export.csv`, `testcodes.png` en `testcodes/` horen bij het demo-event en zijn bewust publiek.

Gebruikt [jsQR](https://github.com/cozmo/jsQR) (Apache-2.0) als QR-lezer wanneer de browser er zelf geen heeft.
