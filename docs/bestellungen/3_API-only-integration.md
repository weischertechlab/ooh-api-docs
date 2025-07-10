title: API only Integration

# API only Integration

## Abschicken einer Bestellung

- Neben den Bestelldaten muss verpflichtend der Tenant angegeben werden. Dies ist die von uns eindeutig vergebene Bezeichnung des Clients. Anhand dieser wird entschieden, an wen Status Rückmeldungen der Bestellung gesendet werden.
- Damit unser System die Callbacks an dein System zurücksenden kann, muss das Feld 'metaData' mit dem Wert 'baseUrl' befüllt werden. 
 Beispiel metaData für Request [Neue Bestellung anlegen]([https://](https://apim-jvb-we-prod.developer.azure-api.net/api-details#api=order-api-v2&operation=post-api-v2-bestellung)):

```
"metaData": {
    "environment": "dev",
    "baseUrl:" : "https://deine-callback-url.de"
}
```

##### Happy Case:

``` mermaid
sequenceDiagram
    Client->>API: POST /bestellung/
    API->>Client: PATCH Cancel nicht gebuchte Flächen
    API-->>Client: 201 Created
```

Die Bestellung wird angelegt und Flächen, welche nicht gebucht werden konnten, werden als Storno an den Client zurückgemeldet.



##### Error Case:

``` mermaid
sequenceDiagram
    Client->>API: POST /bestellung/
    API->>Client: PATCH Cancel alle Flächen
    API-->>Client: 201 Created
```

## Zuweisung von Motiven

``` mermaid
sequenceDiagram
    Client->>API: PATCH /bestellung/{}
    API-->>Client: 200 OK(PIC)
```

Ein bestehendes oder neues Motiv wird einer Flächenbuchung zugeordnet. Wenn der Druck bei Weischer gemacht werden soll, muss das Motiv als PDF gesendet werden, sonst geht auch jpg. Außerdem muss für das Format ein FormatKey übergeben werden, welcher aus den Stammdaten entnommen werden kann.
Bei Erfolgreicher Zuweisung, wird die PIC Nummer zurückgegeben.

## Stornierung von Flächen

Bei einer bestehenden Bestellung können beliebig viele Flächen storniert werden.

``` mermaid
sequenceDiagram
    Client->>API: DELETE /bestellung/{bestellnummerClient}
    API-->>Client: 200 OK
```

## Abrufen der Flächenbuchungen einer Bestellung

Zu einer Bestellung können die gebuchten Flächen mit ihren Status abgerufen werden.

``` mermaid
sequenceDiagram
    Client->>API: GET /bestellung/{bestellnummer}
    API-->>Client: 200 OK(Bestellung)
```


## Rückantwort bei Statusänderungen zur Bestellung

Wenn ein Status einer Flächenbuchung innerhalb einer Bestellung geändert wird, wird der Client anhand der mitgelieferten BaseUrl per PATCH benachrichtigt.

##### Bestätigung

``` mermaid
sequenceDiagram 
    API->>Client: PATCH {baseUrl}/callback/bestellungen/{bestellnummer}/{flaechenNummer}/confirm
    Client-->>API: 200 OK
```

##### Storno

``` mermaid
sequenceDiagram
    API->>Client: PATCH {baseUrl}/callback/bestellungen/{bestellnummer}/{flaechenNummer}/cancel
    Client-->>API: 200 OK
```

## Fristen

- Motive bis X
- Stornierung bis Y