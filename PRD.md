# PRD di ScuolaChill · Team [aleopre]

## Informazioni sul documento

|              |              |
| ------------ | ------------ |
| **Prodotto** | ScuolaChill  |
| **Team**     | aleopre      |
| **Autori**   | Alexia Oprea |
| **Versione** | 1.0          |
| **Data**     | 07/10/2026   |
| **Stato**    | _Bozza_      |

### Storico delle versioni

| Versione | Data       | Autore       | Cosa è cambiato e perché |
| -------- | ---------- | ------------ | ------------------------ |
| 1.0      | 07/10/2026 | Alexia Oprea | Prima stesura            |
|          |            |              |                          |

---

# Prima parte · Il cosa

## Scopo e perimetro

### Perché esiste ScuolaChill

**Dal lato business.**

> ScuolaChill nasce dalla necessità di gestire alcune delle principali attività didattiche in un'unica soluzione web\
> I ruoli principali sono 3:

- **Direttore** che può amministrare utenti, classi e l'organizzazione della vita scolastica
- **Docenti** che possono gestire materiali, verifiche e valutazioni
- **Studenti** che possono consultare materiali didattici, svolgere verifiche e controllare i propri voti

**Dal lato tecnico.**

ScuolaChill è un'applicazione full stack composta da un frontend _React_ e da un backend _REST_ realizzato in _C#_ (con ASP.NET Core)\
Frontend e Backend comunicano tra loro tramite _HTTPS_ mentre i dati vengono salvati in un Database relazionale _MySQL_
Le API principali sono documentate con _OpenAPI/Swagger_ e coperte da una collezione _Postman_ usata come verifica.\
Il sistema è deployato su _Microsoft Azure_

### Cosa è incluso

**Per il Direttore**

- Creazione e gestione delle classi
- Gestione di Docenti e Studenti
- Assegnazioni degli Studenti alle classi
- Assegnazione dei Docenti alle rispettive materie e alle classi
- Visualizzazione della panoramica della scuola (classi, docenti, studenti, andamento dei voti)

**Per i Docenti**

- Caricamento, modifica e cancellazione del materiale didattico
- Creazione e gestione delle verifiche
- Assegnazione dei voti
- (?) Assegnazione presenze - assenze - uscite anticipate - entrate in ritardo
- Possibilità di rifare la verifica per gli Studenti assenti

**Per gli Studenti**

- Svoglimento e consegna delle verifiche
- Panoramica dei propri voti per materia e media dei voti (sia per materia che generale)
- (?) Visualizzazione registro presenze

**Generale**

- Uso di _Resend_ per invio email (es. creazione account, reset password)

### Cosa non è incluso

- Gestione delle comunicazioni scuola-famiglia
- Chat interna
- Pagelle ufficiali
- Orario scolastico
- Videolezioni
- Gestione della segreteria
- App nativa per smartphone

---

## Stakeholder

| Stakeholder                 | Cosa fa                                                                                    | Cosa gli interessa                                                                    | Come lo coinvolgete                       |
| --------------------------- | ------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------- | ----------------------------------------- |
| Direttore                   | Gestisce studenti, docenti e classi e supervisiona le attività della scuola                | Poter gestire facilmente utenti e classi e una visione generale e chiara della scuola | Intervista, presentazione e collaudo      |
| Docenti                     | Gestiscono il materiale didattico, creano verifiche e assegnano voti e presenze (?)        | Gestire in modo semplice e veloce le proprie classi e il materiale                    | Intervista e collaudo                     |
| Studenti                    | Consultano il materiale, svolgono verifiche e visualizzano il proprio andamento scolastico | Avere un accesso semplice e veloce alle attività e alle proprie informazioni          | Test di usabilità e collaudo              |
| Docente del corso           | Valida il PRD                                                                              | Correttezza delle scelte progettuali e tecniche                                       | Presentazione e domande                   |
| Collaudatori del primo anno | Usano ScuolaChill come utenti reali                                                        | Semplicità d'uso e corretto funzionamento delle funzionalità principali               | Intervista, collaudo e raccolta feedback  |
| Team di sviluppo (io)       | Progetta, sviluppa, testa e mantiene ScuolaChill                                           | Qualità del codice, testabilità, mantenibilità e rispetto dei requisiti               | Progettazione, sviluppo, test e revisione |

---

## Destinatari e contesto d'uso

### La scuola che avete immaginato

ScuolaChill è progettato per un liceo linguistico di piccole-medie dimensioni situato in Nord-Italia.\
La scuola utilizza ScuolaChill principalmente durante l'orario scolastico ma Docenti e Studenti possono accedervi anche da casa.\
La giornata scolastica si svolge principalmente dalle 8.00 alle 14.00 dal lunedì al venerdì.\
Gli utenti accedono al sistema tramite il WI-FI della scuola, la rete mobile o il WI-FI di casa.
| | Valore |
| ------------------ | --------------------------------------------------------------- |
| Numero di studenti | 150 |
| Numero di docenti | 30 |
| Numero di classi | 6 |
| Orario scolastico | 8:00 – 14:00, dal lunedì al venerdì |
| Connettività | Wi-Fi scolastico condiviso, rete mobile e WI-FI di casa |

### Gli archetipi

| ID      | Archetipo | Contesto d'uso                                                                                                                                   | Competenze digitali | Dispositivo principale            | Frequenza d'uso |
| ------- | --------- | ------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------- | --------------------------------- | --------------- |
| ARC-001 | Direttore | Utilizza ScuolaChill principalmente dal proprio ufficio per gestire utenti, classi e controllare l'andamento dell'istituto                       | Medio-alte          | PC / Laptop                       | Quotidiana      |
| ARC-002 | Docente   | Utilizza ScuolaChill a scuola e da casa per caricare materiali, creare verifiche e assegnare voti e presenze                                     | Medie / Medio-alte  | Laptop / Tablet                   | Quotidiana      |
| ARC-003 | Studente  | Utilizza ScuolaChill durante le lezioni, in laboratorio, a casa o in altri momenti della giornata per consultare il proprio andamento scolastico | Medie / Medio-alte  | PC / Laptop / Tablet / Smartphone | Quotidiano      |

---

## Panoramica e casi d'uso

### ScuolaChill in poche righe

ScuolaChill è una piattaforma online in cui la scuola può organizzare e gestire le principali attività legate alla didattica.\
Il _Direttore_ può gestire docenti, studenti e classi; i _Docenti_ possono mettere a disposizione il loro materiale e creare verifiche; gli _Studenti_ possono studiare, svolgere le verifiche e controllare i propri voti\

**I vantaggi principali sono:**

> - Tutto in un unico posto:\
>   Materiali, verifiche e voti sono facilmente reperibili senza dover utilizzare strumenti diversi;
> - Maggiore organizzazione :\
>   Ogni utente vede le informazioni e le attività che gli competono;
> - Accesso semplice e immediato:\
>   ScuolaChill può essere usato sia a scuola che a casa
> - Risparmio di tempo
>   Direttore e docenti possono gestire le proprie attività in modo più rapido e ordinato
> - Maggiore autonomia per gli studenti:\
>   Possono controllare in autonomia materiali, verifiche e valutazioni

### User flow e scenari

**DIR-01 · Creare account docente**

**User flow**

1. Il direttore accede a ScuolaChill
2. Apre la sezione "_Gestione utenti_"
3. Seleziona "_Docenti_"
4. Seleziona "_Nuovo docente_"
5. Inserisce i dati richiesti (Nome, Cognome, Secondo nome/ cognome, Data di nascita e Materia/e insegnata/e)
6. COnferma la creazione dell'account
7. Il sistema verifica che siano stati inseriti tutti i dati e che siano tutti validi(Data di nascita e email soprattuto)
8. Il sistema crea l'account con ruolo Docente
9. Il nuovo docente compare nell'elenco degli utenti

**Scenario principale.**

Il direttore deve inserire il nuovo docente Mario Rossi.\
Inserisce nome, cognome, data di nascita, materia insegnata e email.\
Il sistema verifica che tutti i dati siano stati inseriti correttamente, valida data di nascita (deve essere maggiorenne) e email (non già in uso), poi salva l'account con il ruolo corretto e mostra Mario Rossi nell'elenco utenti

**Scenari alternativi.**

- Nella scuola c'è un altro docente omonimo del nuovo docente Mario Rossi e quindi la mail sarà uguale per entrambi: "mario.rossi.doc@scuolachill.it".\
  il sistema segnala che la mail è già assocciata a un altro utente e non crea il nuovo account. Se presente, verrà inserito il secondo nome/ cognome del docente.
- Uno o più dati non sono validi, il sistema segnala il problema, evidenzia gli errori e ne impedisce il salvataggio
- Un docente o uno studente tentano di creare un nuovo account utente, il sistema nega l'accesso

**DIR-03 · Creare classi e comporle**

**User flow**

1. Il Direttore accede a ScuolaChill
2. Apre la sezione "_Classi_"
3. Seleziona "_Crea nuova classe_"
4. Inserisce i dati della classe (nome sezione)
5. Conferma la creazione
6. Apre la classe appena creata
7. Seleziona gli studenti da assegnare
8. Assegna i docenti e le rispettive materie
9. Salva la composizione della classe
10. Il sistema aggiorna le informazioni degli utenti coinvolti

**Scenario principale.**

Il direttore crea la classe 1A e vi assegna 24 studenti. Successivamente assegna alla classe un docente di Inglese e un docente di Matematica. Dopo il salvataggio, gli studenti risultano iscritti alla 1A e i docenti assegnati vedono la classe tra quelle di loro competenza.

**Scenari alternativi.**

- Uno studente è assegnato a un'altra classe attiva, il sistema impedisce una seconda assegnazione e propone il trasferimento di sezione
- Un docente viene assegnato a una materia che non gli è stata associata. Il sistema segnala l'errore e l'operazione viene impedita

**DIR-04 · Vedere tutto**

**User flow**

1. Il direttore accede a ScuolaChill
2. Apre la dashboard principale
3. Visualizza il numero di Studenti, Docenti, Classi
4. Consulta l'elenco delle classi
5. Consulta i Docenti e le materie assegnate
6. Visualizza l'andamento generale dei voti

**Scenario principale.**

Il Direttore vuole controllare rapidamente l'andamento dell'istituto prima di una riunione.
Apre la dashboard e visualizza il numero di studenti per classe, le materie assegnate ai docenti e l'andamento generale dei voti senza dover aprire singolarmente ogni classe

**Scenari alternativi.**

- Nessun dato disponibile, la piattaforma è appena stata configurata e non sono ancora presenti studenti, docenti o voti.
  Il sistema mostra le sezioni vuote con un messaggio "_Nessun dato inserito_" invece che lasciare la pagina vuota
- Sessione scaduta, il Direttore rimane inattivo abbastanza a lungo da far scadere la sessione. Quando prova a consultare la dashboard, il sistema richiede l'autenticazione
- Dati non disponibili temporaneamente, il sistema non riesce a recuperare i dati dal database. Viene mostrato un messaggio di errore e permette al Direttore di riprovare

---

## Requisiti funzionali

### Le user story della traccia

| ID     | Storia                            | AC aggiunti dal team | Note |
| ------ | --------------------------------- | -------------------- | ---- |
| DIR-01 | Creare account docente            | _…_                  | _…_  |
| DIR-02 | Creare account studente           | _…_                  | _…_  |
| DIR-03 | Creare classi e comporle          | _…_                  | _…_  |
| DIR-04 | Vedere tutto                      | _…_                  | _…_  |
| DOC-01 | Caricare materiale didattico      | _…_                  | _…_  |
| DOC-02 | Creare le proprie verifiche       | _…_                  | _…_  |
| DOC-03 | Assegnare i voti                  | _…_                  | _…_  |
| STU-01 | Consultare il materiale didattico | _…_                  | _…_  |
| STU-02 | Svolgere una verifica             | _…_                  | _…_  |
| STU-03 | Consultare i propri voti          | _…_                  | _…_  |

<aside>
💡

Gli acceptance criteria della traccia sono il minimo. Puoi aggiungerne, non toglierne. Scrivi quelli nuovi nello stesso formato _Dato che / Quando / Allora_.

</aside>

### Le decisioni lasciate aperte dalla traccia

La traccia lascia alcune scelte a te. Ognuna diventa un requisito con il suo ID. Usa questo formato.

> **FR-[AREA]-[NN] · [Titolo]** (collegato a _ID della storia_)
> _Cosa avete deciso, in modo verificabile.Motivazione:_ _perché avete scelto così._

I punti che devi decidere almeno sono questi.

- [ ] La scala dei voti (DOC-03). Da quanto a quanto, con quale passo, se ammette segni come "+" e "−".
- [ ] Il trasferimento di uno studente fra classi (DIR-03). Si può fare? Cosa succede ai voti?
- [ ] La modifica di una verifica dopo lo svolgimento (DOC-02).
- [ ] La connessione che cade durante una verifica (STU-02).
- [ ] Il fallimento del servizio esterno (per esempio l'email delle credenziali).
- [ ] _Altre decisioni che il team ha scoperto_

---

## Requisiti non funzionali

Ogni requisito ha una soglia, una condizione e un modo per verificarlo. Ed è collegato ad almeno una user story.

| ID     | Famiglia      | Requisito                               | Soglia e condizione                                                         | Come si verifica | Storie collegate |
| ------ | ------------- | --------------------------------------- | --------------------------------------------------------------------------- | ---------------- | ---------------- |
| NFR-01 | Prestazioni   | _es. Apertura della verifica nel picco_ | _es. meno di 2 s per il 95% delle richieste, 75 utenti nello stesso minuto_ | _Test di carico_ | _STU-02_         |
| NFR-02 | Sicurezza     | _…_                                     | _…_                                                                         | _…_              | _…_              |
| NFR-03 | Usabilità     | _…_                                     | _…_                                                                         | _…_              | _…_              |
| NFR-04 | Disponibilità | _…_                                     | _…_                                                                         | _…_              | _…_              |
| NFR-05 | Ambientale    | _…_                                     | _…_                                                                         | _…_              | _…_              |
| NFR-06 | Supporto      | _…_                                     | _…_                                                                         | _…_              | _…_              |
| NFR-07 | Interazione   | _…_                                     | _…_                                                                         | _…_              | _…_              |
| NFR-08 | Conformità    | _…_                                     | _…_                                                                         | _…_              | _…_              |

<aside>
💡

Le famiglie da coprire sono queste. **Prestazioni, disponibilità, scalabilità, sicurezza** e **conformità** vengono dalla lezione sui requisiti funzionali e non funzionali. **Usabilità, ambientali, supporto** e **interazione** vengono dalla lezione sul PRD. Se una famiglia resta vuota, scrivi perché non vi riguarda.

I requisiti trasversali della traccia (HTTPS, paginazione, OpenAPI, errori uniformi, Dev e Prod) sono già obbligatori. Riportali qui con il loro ID.

</aside>

### Requisiti impliciti

Prima di chiudere questa sezione, intervista per dieci minuti un ragazzo del primo anno. La domanda è una sola. _"Cosa daresti per scontato che un'app di questo tipo faccia sempre, o non faccia mai?"_

| Chi avete intervistato | Cosa ha detto                     | Requisito che ne avete ricavato |
| ---------------------- | --------------------------------- | ------------------------------- |
| _nome o iniziali_      | _"Il voto non deve sparire, mai"_ | _NFR-…_                         |
|                        |                                   |                                 |

---

## Assunzioni, vincoli e dipendenze

### Assunzioni

Quello che date per vero senza poterlo garantire.

| ID     | Assunzione                                   | Cosa succede se è falsa         |
| ------ | -------------------------------------------- | ------------------------------- |
| ASS-01 | _es. La scuola ha 800 studenti e 60 docenti_ | _Il dimensionamento va rifatto_ |
|        |                                              |                                 |

### Vincoli

I limiti che non potete cambiare.

| ID     | Vincolo                                             | Da dove viene          |
| ------ | --------------------------------------------------- | ---------------------- |
| VIN-01 | _es. Il budget cloud è quello dei crediti studente_ | _Traccia del progetto_ |
|        |                                                     |                        |

### Dipendenze

Le cose esterne senza cui non potete andare avanti.

| ID     | Dipendenza                              | Serve entro          | Chi se ne occupa |
| ------ | --------------------------------------- | -------------------- | ---------------- |
| DIP-01 | _es. Account attivo sul servizio email_ | _Prima del collaudo_ | _nome_           |
|        |                                         |                      |                  |

---

# Seconda parte · Il come

<aside>
💡

Da qui in poi parli al tuo docente e al tuo team, non al Direttore. Ogni scelta tecnica va motivata e confrontata con almeno un'alternativa. "Lo conosciamo" è una motivazione valida, ma non può essere l'unica.

</aside>

## Stima del carico

### Utenti concorrenti

| Situazione                      | Utenti concorrenti | Da dove viene il numero |
| ------------------------------- | ------------------ | ----------------------- |
| Uso normale durante la giornata | _…_                | _…_                     |
| Picco delle 9:00 (verifiche)    | _…_                | _…_                     |
| Fine quadrimestre (voti)        | _…_                | _…_                     |

### Profilo di carico

| Operazione              | Frequente? | Pesante? | Critica? | Note |
| ----------------------- | ---------- | -------- | -------- | ---- |
| Login                   | _…_        | _…_      | _…_      | _…_  |
| Apertura verifica       | _…_        | _…_      | _…_      | _…_  |
| Consegna verifica       | _…_        | _…_      | _…_      | _…_  |
| Dashboard del Direttore | _…_        | _…_      | _…_      | _…_  |
| Caricamento materiale   | _…_        | _…_      | _…_      | _…_  |

<aside>
💡

I numeri di qui devono essere coerenti con la scuola che avete immaginato e con i requisiti non funzionali. Se dichiarate 800 studenti, non potete dimensionare per 20 utenti senza spiegare perché.

</aside>

---

## Scelte tecnologiche

| Area             | Scelta | Alternativa considerata | Perché avete scelto così |
| ---------------- | ------ | ----------------------- | ------------------------ |
| Backend          | _…_    | _…_                     | _…_                      |
| Frontend         | _…_    | _…_                     | _…_                      |
| Database         | _…_    | _…_                     | _…_                      |
| Provider cloud   | _…_    | _…_                     | _…_                      |
| Servizi cloud    | _…_    | _…_                     | _…_                      |
| Regione          | _…_    | _…_                     | _…_                      |
| Servizio esterno | _…_    | _…_                     | _…_                      |
