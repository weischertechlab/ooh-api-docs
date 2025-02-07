title: API only Integration

# API only Integration

## Abschicken einer Bestellung

- Beschreibung der wichtigen Felder tetnant und baseUrl

Happy Case:

``` mermaid
sequenceDiagram
    Client->>API: POST /bestellung/
    API-->>Client: 200 OK
```

Error Case:


## Rückantwort bei Statusänderungen zur Bestellung

- Bestätigung
- Storno

## Zuweisung von Motiven

- Jpeg wenn der Druck anders von jemand anderem als Weischer gehandelt wird, ansonsten PDF nötig
- Zurückgesendet wird die PIC Nummer

## Fristen

- Motive bis X
- Stornierung bis Y