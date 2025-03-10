title: API only Integration

# Asynchrone Messagebus Integration

Die Kommunikation läuft über einen Servicebus. Über den Bus können Bestellungen angelegt, Motive können Flächen zugeordnet und Flächen einer Bestellung können storniert werden. Je nachdem um welche der genannten Aktionen es sich handelt, wird in den Custom Properties der Nachricht ein entsprechender MessageType übergeben (Order, MotifInstruction, OrderCancelRequest)

## Abschicken einer Bestellung

Die Nachricht muss den MessageType "Order" und folgende Struktur haben:


```json
{
  "Bestellung": {
    "BestellnummerClient": "12345",
    "HaendlerIdClient": "H123",
    "Jahr": 2025,
    "Email": "example@weischer.com",
    "Firma": "Weischer",
    "Strasse": "Musterstraße 1",
    "Laenderkennzeichen": "DE",
    "Plz": "12345",
    "Ort": "Hamburg",
    "Ansprechpartner": "Max Mustermann",
    "BestelltAm": "2023-10-01T12:00:00Z",
    "Flaechenbuchungen": [
      {
        "FlaechenbuchungsIDClient": 1,
        "AnbieterNr": 222,
        "StandortNr": 1232132,
        "StellenNr": 1,
        "Termin": 1,
        "ErsatzFlaeche": false,
        "Motiv": {
          "MotivIdClient": "M123",
          "MotivBezeichnung": "Werbung",
          "PdfDownloadLink": "http://example.com/motiv.pdf",
          "FormatKey": "30"
        }
      }
    ],
    "MetaData": {
      "baseUrl": "https://client-url.de",
      "environment": "test"
    }
  }
}

```

## Zuweisung von Motiven

Die Nachricht muss den MessageType "MotifInstruction" und folgende Struktur haben:

```json
{
  "Bestellung": {
    "BestellnummerClient": "12345",
    "FlaechenbuchungsIDClient": "1",
    "Motiv": {
      "MotivIdClient": "M123",
      "MotivBezeichnung": "Werbung",
      "PdfDownloadLink": "http://example.com/motiv.pdf",
      "FormatKey": "30"
    }
  }
}
```

## Stornierung von Flächen

Die Nachricht muss den MessageType "OrderCancelRequest" und folgende Struktur haben:

```json
{
  "Bestellung": {
    "BestellnummerClient": "12345",
    "FlaechenbuchungsIdClients": [
      "1",
      "2",
      "3"
    ]
  }
}
```

## Rückantwort bei Statusänderungen zur Bestellung

Bei Statusänderungen wird eine Nachricht mit dem MessageType "OrderConfirmation" und folgender Struktur auf den Servicebus gelegt:

```json
{
  "BestellnummerClient": "12345",
  "FlaechenbuchungsIDClient": "1",
  "Buchungsstatus": "Confirmed"
}
```

Der Buchungsstatus kann "Confirmed" oder "Loss" sein.

## Rückantwort wenn ein Motiv einer Fläche zugeordnet wurde

Bei Zuordnung eines Motivs wird eine Nachricht mit dem MessageType "MotifInstructionConfirmation" und folgender Struktur auf den Servicebus gelegt:

```json
{
  "BestellnummerClient": "12345",
  "MotifAssignmentConfirmations": [
    {
      "FlaechenbuchungsIDClient": "1",
      "PICNumber": "PIC123"
    }
  ]
}
```

## Storno

Wenn der Client Flächen einer Bestellung storniert hat, kommt die Rückmeldung nicht als OrderConfirmation, sondern es wird eine Nachricht mit dem MessageType "OrderCancelRequestConfirmation" und folgender Struktur auf den Servicebus gelegt:

```json
{
  "PurchaserOrderId": "12345",
  "PurchaserItemIds": [
    "1",
    "2",
    "3"
  ]
}
```