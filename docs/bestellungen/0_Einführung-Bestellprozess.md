title: Einführung Bestellprozess

# Einführung Bestellprozess

Auf dieser Seite findest Du mehrere Varianten wie Du Bestellprozesse mit uns umsetzen kannst.

## Iframe Shopintegration

Der schnellste Weg mit minimalem Aufwand für dich: Du integrierst eine fertigen Webshop via HTML Iframe auf deiner Website. Konfiguration und komplette Abwicklung läuft über uns.

[Weiter zu den Details](1_Iframe-Shopintegration.md)

[![Der Shop](shopui.png)](shopui.png)

## Iframe Shopintegration mit eigenem Warenkorb

Du benötigst mehr Kontrolle über den Bestellprozess und möchtest zeitgleich einen fertigen Webshop nutzen? Dann ist unsere hybride Lösung genau das richtige für dich. Du integrierst wie bei der Iframe Shopintegrtion einen fertigen Webshop via HTML Iframe. Nach Abschluss der Bestellung kannst Du via [Warenkorb API](https://apim-jvb-we-prod.developer.azure-api.net/api-details#api=v0&operation=ruft-offene-warenk-rbe-aus-dem-shop-ab) die Bestellung Abrufen und in deinen individuellen Bestellprozess übernehmen.

[Weiter zu den Details](2_Iframe-Shopintegration-hybrid.md)

## API Only Integration

Du hast bereits einen eigenen Shop und möchtest diesen für die Außenwerbung erweitern? Dann ist unsere API Only Anbindung genau das richtige für dich. Über unsere [Stammdaten API](https://apim-jvb-we-prod.developer.azure-api.net/api-details#api=weischer-stammdaten-api-v3&operation=get-api-v3-grossflaechen-stellenart-stellenart) integrierst Du die Medien in dein System. Abgeschlossene Bestellungen in deinem Shop übergibst Du uns anschließend an unsere [Bestellungen API](https://apim-jvb-we-prod.developer.azure-api.net/api-details#api=order-api-v2&operation=get-api-v2-tenant-callback-bestellungen-bestellnummer).

Alternativ zu unseren REST Schnittstellen ist auch eine Anbindung via Messagebus möglich. Sprich uns gerne darauf an.

[Weiter zu den Details](3_API-only-integration.md)