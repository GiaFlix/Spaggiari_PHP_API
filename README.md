# Spaggiari_PHP_API
Esempi PHP per usare le API di Spaggiari / Classeviva

Benvenuti nella mia prima repository di Github :)
Qui vi spiego il sistema api Ufficiale, presumo visto che va a usare i server di spaggiari direttamente.

in primis per poter usare le api dovrete fare login e quindi autenticarvi a spaggiari con le vostre credenziali.

# autenticazione tramite API Spaggiari / Classeviva

Esempio di codice PHP per fare login e autenticarsi alle API di Spaggiari / Classeviva. Il codice utilizza cURL per inviare una richiesta di login all'API e decodifica la risposta JSON per verificare se il login è stato effettuato con successo.

```
// URL dell'API di ClasseViva
$url = "https://web.spaggiari.eu/rest/v1/auth/login";

// Dati di login
$username = "XYYYYYYYZ";
$password = "PASSWORD";

// Intestazioni richieste
$headers = array(
    'Content-Type: application/json',
    'Z-Dev-ApiKey: +zorro+',
    'User-Agent: zorro/1.0'
);

// Dati da inviare come corpo della richiesta
$data = array(
    "ident" => null,
    "pass" => $password,
    "uid" => $username
);

// Inizializza la sessione cURL
$ch = curl_init();

// Imposta le opzioni di cURL
curl_setopt($ch, CURLOPT_URL, $url);
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
curl_setopt($ch, CURLOPT_POST, true);
curl_setopt($ch, CURLOPT_POSTFIELDS, json_encode($data));
curl_setopt($ch, CURLOPT_HTTPHEADER, $headers);

// Esegue la richiesta e ottiene la risposta
$response = curl_exec($ch);

// Chiude la sessione cURL
curl_close($ch);

// Analizza la risposta JSON
$json_response = json_decode($response, true);

// Verifica se la richiesta è andata a buon fine
if ($json_response !== null) {
    echo "Login riuscito\n";
    print_r($json_response);
} else {
    // Login fallito Abbastanza improbabile visto che questo accade solo in caso di assenza di internet
    echo "Login fallito.";
}
```

Spero abbiate capito cosa modificare.
Comunque copiatevi il token che ci servirà per far funzionare le altre funzionalità

# Altre Funzionalità

Trovate tutto sulla documentazione di michelangelomo: https://github.com/michelangelomo/Classeviva-Official-Endpoints
in base a quella documentazione, dopo aver fatto login, dovremmo usare il token precedentemente copiato per poter eseguire tutte le altre funzionalità.
ecco un esempio:

```
// URL dell'API di ClasseViva
$url = "https://web.spaggiari.eu/rest/v1/students/{IDSTUDENTE}/documents";

// Token
$token= "";

// Intestazioni richieste
$headers = array(
    'Content-Type: application/json',
    'Z-Dev-ApiKey: +zorro+',
    'User-Agent: zorro/1.0',
    'Z-Auth-Token: '.$token,
);

// Inizializza la sessione cURL
$ch = curl_init();

// Imposta le opzioni di cURL
curl_setopt($ch, CURLOPT_URL, $url);
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
curl_setopt($ch, CURLOPT_POST, true);
curl_setopt($ch, CURLOPT_HTTPHEADER, $headers);

// Esegue la richiesta e ottiene la risposta
$response = curl_exec($ch);

// Chiude la sessione cURL
curl_close($ch);

// Analizza la risposta JSON
$json_response = json_decode($response, true);

// Verifica se la richiesta è andata a buon fine
if ($json_response !== null) {
    echo "La richiesta è andata a buon fine.\n";
    print_r($json_response);
} else {
    // richiesta fallita, gestisci l'errore
    echo "Richiesta fallita.";
}
```

# Attenzione
- Alcune richieste richiedono di essere in forma GET, Quindi al posto di ```CURLOPT_POST``` mettete ```CURLOPT_HTTPGET```
- Ricordo che le sessioni scadono ogni 2 ore da quando vi siete autenticati, quindi se state usando questo sistema per controllare se è uscita la vostra pagella o per sapere se il voto che stavate aspettando sia arrivato, dovrete fare un'altra autenticazione.
Ora non saprei come aiutarvi visto che questa API potreste usarla in modo diverso dal mio.
- Ricordo che se come me siete qua per cercare bug di spaggiari.. beh sappiate che non funziona con altri codici esterni :)

Detto questo, se sei arrivato fin qui, ti chiedo di lasciare una stella in alto a destra, in caso di problemi mi trovi via mail su ```giasin@giaflix.it```

Ciaoo!
