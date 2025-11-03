
Altaelva - Apple / Codemagic Ready
=================================

Dette prosjektet er ferdig konfigurert for å bygge i iOS/App Store ved hjelp av Codemagic.
Følg disse trinnene for å få en .ipa lastet opp til App Store Connect:

1) Last opp prosjektet til et Git-repository (GitHub anbefalt).
   git init
   git add .
   git commit -m "Altaelva Apple-ready"
   git remote add origin <your-git-repo-url>
   git push -u origin main

2) Opprett App Store Connect API Key (Users and Access -> Keys -> Create API Key).
   Noter ned Issuer ID og Key ID, og last ned .p8-filen.

3) Logg inn på https://codemagic.io og "Connect repository" (GitHub).
   I Codemagic -> Settings -> Apple Developer:
   - Add App Store Connect API key: last opp .p8, fyll inn Issuer ID og Key ID.
   - Set credential name to: APP_STORE_CONNECT_API (matches codemagic.yaml)

4) I Codemagic: start workflow "ios-release".
   Codemagic vil:
   - kjøre flutter pub get
   - bygge ipa med export options (ios/ExportOptions.plist)
   - laste opp ipa til App Store Connect ved bruk av App Store Connect API-key

5) I App Store Connect: opprett ny app (My Apps -> + -> New App)
   - Platform: iOS
   - Name: Altaelva
   - Primary language: Norwegian (Bokmål)
   - Bundle ID: no.daisaks.altaelva (må matche codemagic.yaml)
   - SKU: valgfritt
   - Support email: daisaks@gmail.com
   - Privacy Policy URL: (URL til privacy.html)

6) Når build er lastet opp via Codemagic, gå til App Store Connect -> TestFlight for å distribuere til testere.
   Når du er fornøyd, velg build i App Store Connect -> App Store -> Prepare for Submission -> Submit for Review.

Tips:
- Sørg for at privacy.html er publisert via HTTPS (GitHub Pages eller Netlify).
- Hvis du foretrekker å signere manuelt, last opp certificate/provisioning i Codemagic i stedet for API key.
