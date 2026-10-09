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

**DOC-01 · Caricare il materiale didattico**

**User flow**

1. Il Docente accede a ScuolaChill
2. Apre la sezione "_Materiale didattico_"
3. Seleziona una delle proprie classi
4. Seleziona una delle proprie materie
5. Seleziona "_Aggiungi materiale_"
6. Inserisce titolo e descrizione
7. Seleziona un file da caricare
8. COnferma l'operazione
9. Il materiale viene caricato
10. Gli studenti della classe possono visualizzare il materiale caricato

**Scenario principale.**

Il docente Mario Rossi vuole condividere con la classe 1A una presentazione di Inglese\
Seleziona 1A, sceglie Inglese tra le materie a lui assegnate, inserisce il titolo "English Literature" e nella descrizione scrive a che lezione fa riferimento il file e una breve descrizione di quello che si trova al suo interno.\
Importa il file e salva. Il materiale viene pubblicatoe gli studenti della classe possono visualizzarlo

**Scenari alternativi.**

- Il caricamento viene interrotto, il materiale non viene pubblicato ma viene salvato in bozza e il docente può riprovare
- Il file non è valido oppure supera i limiti previsti, il caricamento viene rifiutato
- Titolo mancante, il docente seleziona un file senza inserire il titolo. Il sistema segnala il campo come obbligatorio e impedisce la pubblicazione finchè non viene inserito
- Materiale duplicato, il docente tenta di caricare nuovamente lo stesso materiale per la stessa classe e materia. Il sistema segnala che potrebbe trattarsi di un duplicato e permette di decidere se proseguire

**DOC-02 · Creare le proprie verifiche**

**User flow**

1. Il Docente accede a ScuolaChill
2. Apre la sezione "_Verifiche_"
3. Seleziona una classe
4. Seleziona la materia
5. Seleziona "_Nuova verifica_"
6. Inserisce titolo, data e l'ora in cui verrà svolta la verifica e il tempo disponibile per la consegna
7. Inserisce le domande
8. Controlla i dati inseriti
9. Salva la verifica
10. La verifica diventa disponibile per essere svolta nella data e ora selezionata

**Scenario principale.**

Il docente Luigi Bianchi prepara una verifica di Matematica per la 1A.\
Inserisce il titolo "Equazioni di Primo grado", imposta la data, l'ora e il tempo disponibile per svolgere la verifica e aggiunge le consegne. Dopo aver salvato, il docente vede la verifica tra le "_Verifiche disponibili_"

**Scenari alternativi.**

- Data non valida, il docente inserisce una data di svolgimento precedente alla data corrente. Il sistema segnala l'errore e ne impedisce il salvataggio.
- Errore di salvataggio, la connessione viene interrota mentre il docente salva la verifica. Il sistema comunica che l'operazione non è stata eseguita correttamente e salva una bozza in modo da non dover riscrivere tutto. Permette poi di riprovare l'operazione
- Doppio click su salva, il docente preme 2 volte velocemente il tasto "_Salva_". Il sistema impedisce la creazione di 2 verifiche identiche a causa delle richieste duplicate e pubblica solo 1 copia

**DOC-03 · Assegnare voti**

**User flow**

1. Il docente accede a ScuolaChill
2. Seleziona la classe
3. Apre la sezione Verifiche
4. Apre la sezione "_Verifiche svolte_"
5. Seleziona la verifica
6. Visualizza gli studenti che hanno svolto e consegnato
7. Seleziona uno studente
8. Inserisce il voto
9. IL voto viene registrato
10. Una volta inseriti tutti i voti, salva e li pubblica
11. Il voto può essere visualizzato dallo studente

**Scenario principale.**

Il docente Luigi Bianchi corregge una verifica di Matematica della 1A.\
Seleziona "_Verifiche_", "_Verifiche svolte_", "_Equazioni di primo grado_". Compare l'elenco di chi ha svolto il compito. Seleziona lo studente Luca Verdi e visiona la verifica con le rispettive risposte. Inserisce il voto "7.5" e conferma. Il sistema registra il voto e Luca Bianchi può successivamente visualizzarlo nella propria sezione dedicata.

**Scenari alternativi.**

- Voto non inserito, il docente tenta di confermare le valutazioni inserite senza aver inserito uno o più voti. Il sistema segnala che uno o più campi obbligatori sono mancanti e impedisce il salvataggio
- Modifica di un voto già inserito, il docente si accorge di aver inserito un voto errato e prova a modificarlo. Il nuovo voto viene salvato ed è visibile dallo studente

**STUD-01 · Consultare materiale didattico**

**User flow**

1. Lo Studente accede a ScuolaChill
2. Visualizza le proprie materie
3. Seleziona una materia
4. Visualizza l'elenco dei materiali didattici disponibili
5. Seleziona il materiale
6. Consulta o scarica il contenuto

**Scenario principale.**

Luca Verdi, studente della 1A, deve ripassare Inglese in vista di una verifica. Accede a ScuolaChill, apre la materia e visualizza i materiali resi disponibili dal docente. Seleziona uno dei materiali, consulta titolo e descrizione per verificare che sia ciò che gli serve e scarica il materiale

**Scenari alternativi.**

- Non sono presenti materiali, il sistema mostra un messaggio che comunica che non ci sono ancora contenuti disponibili
- Errore durante il download, lo studente prova a scaricare il documento, ma il download viene interrotto. Il sistema segnala il problema e permette di riprovare

**STUD-02 · Svolgere una verifica**

**User flow**

1. Lo Studente accede a ScuolaChill
2. Apre la sezione "_Verifiche da svolgere_"
3. Seleziona la materia che gli interessa
4. Visualizza le verifiche disponibili per materia
5. Il sistema controlla che la data e l'ora inserita dal docente corrispondano con la data e l'ora corrente
6. Legge le domande
7. Inserisce le proprie risposte
8. Controlla la propria verifica
9. Seleziona "_Consegna_"
10. Le risposte vengono registrate
11. La verifica viene contrassegnata come "_Consegnata_"

**Scenario principale.**

Alle 9:00 di venerdì mattina Luca Bianchi accede a ScuolaChill e trova una verifica di Matematica assegnata alla 1A, la sua classe.\
Dopo l'ok del docente, seleziona la verifica, legge le consegne e svolge gli esercizi. Una volta ricontrollato tutto, clicca "_Consegna_" entro il tempo limite. Il sistema conferma che le risposte sono state registrate e mostra che la verifica è stata consegnata correttamente

**Scenari alternativi.**

- Connessione cade durante lo svolgimento, le risposte già salvate rimangono registrate e il sistema segnala lo stato della connessione
- Il tempo della verifica assegnato dal docente è scaduto, il sistema mostra un banner "_Tempo Scaduto_" e ne obbliga la consegna
- Lo studente apre la verifica in un altra scheda, il sistema impedisce una seconda consegna dopo che la prima è stata registrata

**STUD-03 · Consultare i voti**

**User flow**

1. Lo Studente accede a ScuolaChill
2. Apre la sezione "_Voti_"
3. Il sistema recupera i voti associati allo studente
4. I voti vengono raggrupati per materia
5. Lo studente eventualmente seleziona una materia
6. Visualizza il titolo della verifica, la data in cui è stata svolta e il relativo voto
7. I voti sotto il 5.5 sono visualizzati in rosso, quelli tra il 5.5 e 6- in giallo e i voti tra 6 - 10 in verde

**Scenario principale.**

Luca Bianchi vuole controllare il proprio andamento in Inglese.\
Apre la sezione voti, seleziona Inglese e visualizza tutti i voti e le relative verifiche. Vede anche la media dei voti di Inglese

**Scenari alternativi.**

- Voto non ancora disponibile, lo studente sa di aver svolto la verifica ma il docente non ha ancora registrato la valutazione. Il sistema mostra solo i voti effettivamente registrati quindi la verifica e il relativo voto verranno disponibili quando il docente gli inserirà.
- Ordine dei voti, lo studente modifica la visualizzazione dell'ordine dei voti, per esempio vuole vedere i voti più recenti. Il sistema aggiorna la lista e mostra i voti più recenti suddivisi per materia

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
