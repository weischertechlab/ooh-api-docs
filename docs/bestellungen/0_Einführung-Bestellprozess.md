title: Einführung Bestellprozess

# Einführung Bestellprozess

## Iframe Shopintegration

Du integrierst eine fertigen Webshop via HTML Iframe auf deiner Website. Konfiguration und komplette Abwicklung läuft über uns.

## Iframe Shopintegration mit eigenem Warenkorb

Du integrierst einen fertigen Webshop via HTML Iframe. Zum Abschluss der Bestellung übernimmst du den Warenkorb aus unserem Shop und integrierst ihn in den Warenkorb deiner eigenen Website.

## API Only Integration

Du hast eine eigene Shopüberfläche und übergibst Bestellungen via API Aufruf.


``` mermaid
---
title:
---

gitGraph
   commit
   commit
   branch develop
   checkout develop
   commit id: "L1 Ticket 1"
   commit id: "L1 Ticket 2"
   checkout main
   merge develop
   commit id: "L1 Release" tag: "v1.0.0"
   checkout develop
   commit id: "L1 Hotfix 1"
   branch L2-Release
   checkout L2-Release
   commit id: "L2 Ticket 1"
   commit id: "L2 Ticket 2"
   checkout develop
   commit id: "L1 Hotfix 2"
   
   
```