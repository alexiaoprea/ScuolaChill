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
Il _Direttore_ può gestire docenti, studenti e classi; i _Docenti_ possono mettere a disposizione il loro materiale e creare verifiche; gli _Studenti_ possono studiare, svolgere le verifiche e controllare i propri voti

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

| ID     | Storia                            | AC aggiunti dal team | Note                                                                                         |
| ------ | --------------------------------- | -------------------- | -------------------------------------------------------------------------------------------- |
| DIR-01 | Creare account docente            | AC-04                | Utilizzo del link di attivazione                                                             |
| DIR-02 | Creare account studente           | AC-04                | Gestione delle omonimie                                                                      |
| DIR-03 | Creare classi e comporle          | AC-04 · AC-05        | Unicità dela classe nell'anno scolastico · Eliminazione di una classe con studenti assegnati |
| DIR-04 | Vedere tutto                      | AC-04                | Assenza di voti registrati                                                                   |
| DOC-01 | Caricare materiale didattico      | AC-04                | Protezione dei file                                                                          |
| DOC-02 | Creare le proprie verifiche       | AC-04                | Validare domande e risposte di una verifica                                                  |
| DOC-03 | Assegnare i voti                  | AC-04                | Modifica voto                                                                                |
| STU-01 | Consultare il materiale didattico | AC-03 · AC-04        | Informazioni sul materiale didattico · Ordinamento del materiale didattico                   |
| STU-02 | Svolgere una verifica             | AC-04                | Rispetto della finestra temporale                                                            |
| STU-03 | Consultare i propri voti          | AC-03                | Informazioni sulla valutazione                                                               |

**Direttore (ARC - 01)**

**DIR-01 · Creare account docente**

_USER STORY_

> Come direttore voglio creare gli account dei docenti così da dare al personale l'accesso al sistema con il ruolo corretto.

_ACCEPTANCE CRITERIA_

- AC-01 · Dato che sono autenticato come Direttore, Quando creo un docente con dati validi, Allora l'account viene creato con ruolo Docente e compare nell'elenco dei docenti.
- AC-02 · Dato che esiste già un utente con la stessa email, Quando provo a crearne un altro, Allora ricevo un errore chiaro e nessun account viene creato.
- AC-03 · Dato che sono autenticato come Docente o Studente, Quando provo a creare un docente, Allora l'operazione viene negata.
- AC-04 · Dato che un Docente disponde di un link di attivazione valido, Quando completa correttamente l'attivazione, Allora l'account diventa attivo e lo stesso link non può essere usato nuovamente

**DIR-02 · Creare account studente**

_USER STORY_

> Come Direttore voglio creare gli account degli studenti così da permettere a ogni iscritto di usare l'applicazione.

_ACCEPTANCE CRITERIA_

- AC-01 · Dato che sono autenticato come Direttore, Quando creo uno studente con dati validi, Allora l'account viene creato con ruolo Studente.
- AC-02 · Dato che invio dati incompleti o non validi, Quando confermo la creazione, Allora ricevo l'indicazione puntuale dei campi errati e nessun account viene creato.
- AC-03 · Dato che sono autenticato come Docente o Studente, Quando provo a creare uno studente, Allora l'operazione viene negata.
- AC-04 · Dato che esiste già uno Studente con lo stesso nome e cognome, Quando il sistema genera l'indirizzo email del nuovo Studente, Allora aggiunge un elemento distintivo e garantisce che l'indirizzo sia univoco

**DIR-03 · Creare classi e comporle**

_USER STORY_

> Come Direttore voglio creare le classi e assegnarvi studenti e docenti con le rispettive materie così da riprodurre l'organizzazione reale della scuola.

_ACCEPTANCE CRITERIA_

- AC-01 · Dato che sono autenticato come Direttore, Quando creo una classe e vi assegno studenti, Allora ogni studente risulta appartenere a quella classe.
- AC-02 · Dato che una classe esiste, Quando vi assegno un docente per una materia, Allora il docente vede quella classe fra le proprie e può operarvi solo per quella materia.
- AC-03 · Dato che uno studente è già assegnato a una classe, Quando provo ad assegnarlo a una seconda classe, Allora il sistema lo impedisce o gestisce il trasferimento in modo esplicito (la scelta va documentata nel PRD).
- AC-04 · Dato che esiste già una classe con un determinato nome nello stesso anno scolastico, Quando il Direttore tenta di creare un'altra classe con lo stesso nome, Allora il sistema segnala il conflitto e impedisce la duplicazione.
- AC-05 · Dato che una classe contiene ancora Studenti assegnati, Quando il Direttore tenta di eliminarla, Allora il sistema impedisce l'eliminazione finchè gli studenti non sono stati trasferiti o riassegnati.

**DIR-04 · Vedere tutto**

_USER STORY_

> Come Direttore voglio una vista complessiva su classi, docenti, studenti e voti così da monitorare l'andamento della scuola senza entrare in ogni singola pagina.

_ACCEPTANCE CRITERIA_

- AC-01 · Dato che sono autenticato come Direttore, Quando apro la vista complessiva, Allora vedo i dati aggregati della scuola (classi con numero di studenti, docenti con materie, andamento dei voti).
- AC-02 · Dato che gli elenchi superano la dimensione di una pagina, Quando li consulto, Allora i risultati sono paginati.
- AC-03 · Dato che sono autenticato come Docente o Studente, Quando provo ad accedere alla vista complessiva, Allora l'operazione viene negata.
- AC-04 · Dato che nella scuola non sono ancora presenti voti, Quando il Direttore apre la dashboard, Allora il sistema mostra chiaramente che non sono disponibili valutazioni senza presentare statistiche fuorvianti.

**Docente (ARC - 02)**

**DOC-01 · Creare materiale didattico**

_USER STORY_

> Come Docente voglio caricare il materiale didattico per le mie materie e classi così da metterlo a disposizione degli studenti in un posto solo.

_ACCEPTANCE CRITERIA_

- AC-01 · Dato che sono autenticato come Docente e assegnato a una classe per una materia, Quando carico un materiale per quella classe e materia, Allora gli studenti della classe lo vedono nell'elenco della materia.
- AC-02 · Dato che non sono assegnato a una classe, Quando provo a caricarvi materiale, Allora l'operazione viene negata.
- AC-03 · Dato che ho caricato un materiale, Quando lo modifico o lo elimino, Allora l'operazione riesce solo se il materiale è mio.
- AC-04 · Dato che il materiale è accessibile soltanto agli Studenti di una determinata classe, Quando un utente non autorizzato tenta di scaricarlo direttamente tramite il suo indirizzo, Allora il sistema gli nega l'accesso al file.

**DOC-02 · Creare le proprie verifiche**

_USER STORY_

> Come Docente voglio creare verifiche per le mie classi così da valutare gli studenti sulle mie materie.

_ACCEPTANCE CRITERIA_

- AC-01 · Dato che sono autenticato come Docente e assegnato a una classe per una materia, Quando creo una verifica con titolo, materia, data e contenuto, Allora la verifica risulta visibile agli studenti di quella classe.
- AC-02 · Dato che una verifica è mia, Quando la modifico prima della data di svolgimento, Allora le modifiche sono salvate; le regole dopo lo svolgimento vanno definite e documentate nel PRD.
- AC-03 · Dato che una verifica appartiene a un altro docente, Quando provo a modificarla, Allora l'operazione viene negata.
- AC-04 · Dato che inserisco una domanda a risposta singola o multipla, Quando tento di salvare la verifica senza aver configurato le opzioni di risposta necessarie, Allora il sistema mi segnala la domanda incompleta e impedisce il salvataggio.

**DOC-03 · Assegnare voti**

_USER STORY_

> Come Docente voglio assegnare i voti delle mie verifiche così da registrare formalmente la valutazione di ogni studente.

_ACCEPTANCE CRITERIA_

- AC-01 · Dato che uno studente ha svolto una mia verifica, Quando gli assegno un voto valido, Allora il voto è registrato e lo studente può vederlo fra i propri.
- AC-02 · Dato che inserisco un voto fuori dalla scala prevista, Quando confermo, Allora ricevo un errore e il voto non viene registrato.
- AC-03 · Dato che la verifica appartiene a un altro docente, Quando provo ad assegnare un voto, Allora l'operazione viene negata.
- AC-04 · Dato che una consegna l'ho già valutata, Quando registro una nuova valutazione per la stessa consegna, Allora il voto viene aggiornato alla valutazione più recente

**Studente (ARC - 03)**

**STU-01 · Consultare il materiale didattico**

_USER STORY_

> Come Studente voglio consultare il materiale caricato da ogni docente delle mie materie così da avere tutto ciò che serve per studiare in un unico posto.

_ACCEPTANCE CRITERIA_

- AC-01 · Dato che sono autenticato come Studente, Quando apro una materia della mia classe, Allora vedo il materiale caricato dal docente di quella materia.
- AC-02 · Dato che un materiale appartiene a una classe diversa dalla mia, Quando provo ad accedervi, Allora l'operazione viene negata.
- AC-03 · Dato che come Studente visualizzo l'elenco dei materiali di una materia, Quando il portale mostra i risultati, Allora ogni elemento riporta almeno il titolo, il nome del Docente che l'ha caricato e la data di pubblicazione.
- AC-04 · Dato che una materia contiene più materiali didattici, Quando apro l'elenco, Allora i materiali vengono ordinati dal più recente al meno recente.

**STU-02 · Svolgere una verifica**

_USER STORY_

> Come Studente voglio svolgere le verifiche assegnate alla mia classe così da essere valutato sulle materie che seguo.

_ACCEPTANCE CRITERIA_

- AC-01 · Dato che una verifica è disponibile per la mia classe, Quando la svolgo e consegno, Allora le mie risposte sono salvate e la verifica risulta consegnata.
- AC-02 · Dato che ho già consegnato una verifica, Quando provo a svolgerla di nuovo, Allora l'operazione viene negata.
- AC-03 · Dato che la verifica appartiene a un'altra classe, Quando provo ad accedervi, Allora l'operazione viene negata.
- AC-04 · Dato che a una verifica sono associati una data di disponibilità e una scadenza, Quando tento di iniziare la verifica prima della disponibilità o di consegnarla dopo la scadenza, Allora il sistema impedisce l'operazione salvo eventuali prorooghe autorizzate dal Docente.

**STU-03 · Consultare i propri voti**

_USER STORY_

> Come Studente voglio consultare i miei voti raggruppati per materia così da sapere come sto andando in ciascuna.

_ACCEPTANCE CRITERIA_

- AC-01 · Dato che ho voti registrati, Quando apro la pagina dei voti, Allora li vedo raggruppati per materia con l'indicazione della verifica di provenienza.
- AC-02 · Dato che sono autenticato come Studente, Quando provo a consultare i voti di un altro studente, Allora l'operazione viene negata.
- AC-03 · Dato che sto visualizzando i miei voti, Quando apro il dettaglio di una valutazione, Allora mi vengono mostrate anche la data in cui è stata svolta la verifica, il titolo della verifica e il nome del Docente che ha inserito quella valutazione.

### Le decisioni lasciate aperte dalla traccia

**FR-DOC-01 · Scala dei voti**

> Collegata a: DOC-03 — Assegnare i voti.

_DECISIONE_

I voti vengono spressi su una scala da 1 a 10 con incrementi di 0,5. Non sono ammessi simboli come '+' o '-' o valori al di fuori della scala prevista.

_MOTIVAZIONE_

-> Una scala numerica definita ermette di validare i voti in modo uniforme, impedisce l'inserimento i valori non consentiti e semplifica visualizzazione dei risultati

**FR-DIR-01 · Trasferimento di uno studente**

> Collegata a: DIR-03 — Creare classi e comporle.

_DECISIONE_

Uno studente può appartenere a una sola classe attiva alla volta. Il Direttore può trasferirlo in un'altra classe: il sistema chiude l'associazione precedente e registra quella nuova. I voti e le verifiche svolte prima del trasferimento vengono conservati. Dopo il trasferimento, lo studente accede ai materiali della nuova classe, mentre i risultati precedenti rimangono disponibili nella propria carriera scolastica.

_MOTIVAZIONE_

-> Questa soluzione rappresenta i trasferimenti reali senza duplicare gli studenti o perdere lo storico delle valutazioni.

**FR-DOC-02 · Modifica di una verifica dopo lo svolgimento**

> Collegata a: DOC-02 — Creare le proprie verifiche; STU-02 — Svolgere una verifica.

_DECISIONE_

Prima che uno studente inizi la verifica, il Docente può modificarne liberamente il contenuto. Dal momento in cui almeno uno studente inizia a svolgerla, le domande, le opzioni di risposta, la materia e la classe non possono più essere modificate. Il Docente può invece correggere il titolo e la descrizione. La scadenza può essere prorogata dal Docente, ma non anticipata quando ciò impedirebbe agli studenti di rispettare il termine precedentemente comunicato. Le modifiche alla scadenza vengono registrate.

_MOTIVAZIONE_

-> Modificare le domande dopo l'inizio della verifica potrebbe compromettere la correttezza delle risposte già fornite e rendere non confrontabili i risultati degli studenti.

**FR-STU-01 · Connessione che cade durante una verifica**

> Collegata a: STU-02 — Svolgere una verifica.

_DECISIONE_

Durante lo svolgimento, il sistema salva progressivamente le risposte sul server. Le risposte non ancora sincronizzate vengono conservate temporaneamente nel browser e inviate nuovamente quando la connessione viene ripristinata. La verifica viene considerata consegnata solamente quando il server conferma la registrazione. Se la connessione viene ripristinata prima della scadenza, lo studente può completare la consegna. Se la scadenza è già trascorsa, la consegna richiede un'eventuale proroga autorizzata dal Docente.

_MOTIVAZIONE_

-> La perdita temporanea della connessione non deve cancellare le risposte già salvate. La conferma del server permette inoltre di distinguere una consegna effettiva da un tentativo di invio non completato.

**FR-SYS-01 · Fallimento servizio esterno**

> Collegata a: DIR-01 — Creare account docente; DIR-02 — Creare account studente.

_DECISIONE_

Se il servizio esterno di posta elettronica non è disponibile, l'account viene comunque creato e assume lo stato "_PENDING_ACTIVATION_". Il sistema registra l'errore e tenta nuovamente l'invio dell'email fino a tre volte, con intervalli crescenti. Se tutti i tentativi falliscono, il Direttore può richiedere un nuovo invio.

_MOTIVAZIONE_

-> Un problema temporaneo di un servizio esterno non deve impedire al Direttore di creare gli account. La gestione dello stato di attivazione consente di distinguere gli account creati da quelli effettivamente attivati.

**FR-DIR-02 · Convenzione e unicità degli indirizzi mail**

> Collegata a: DIR-01 — Creare account docente; DIR-02 — Creare account studente.

_DECISIONE_

Il sistema genera gli indirizzi istituzionali secondo queste convenzioni:

- Docenti: nome.cognome.doc@scuolachill.com
- Studenti: nome.cognome.stud@scuolachill.com

In caso di omonimia, il sistema aggiunge un elemento distintivo, come un'iniziale o il secondo nome. Se necessario, aggiunge un breve codice alfanumerico generato automaticamente. L'indirizzo finale deve essere univoco e il database impedisce che venga assegnato a più account.

_MOTIVAZIONE_

-> Una convenzione uniforme rende gli indirizzi riconoscibili e distingue gli utenti con lo stesso nome. Il controllo di unicità evita conflitti durante la creazione degli account.

**FR-DOC-03 · Tipologie di domande supportate**

> Collegata a: DOC-02 — Creare le proprie verifiche; STU-02 — Svolgere una verifica.

_DECISIONE_

La prima versione supporta tre tipologie di domanda:

- risposta singola
- risposta multipla
- risposta testuale libera

Il sistema salva le risposte fornite dagli studenti. Il Docente assegna il voto finale della verifica, anche quando alcune risposte potrebbero essere corrette automaticamente.

_MOTIVAZIONE_

-> Queste tipologie permettono di realizzare verifiche sufficientemente varie senza introdurre un sistema di valutazione automatica troppo complesso per la prima versione.

**FR-DOC-04 · Formati e dimensioni dei materiali didattici**

> Collegata a: DOC-01 — Caricare materiale didattico; STU-01 — Consultare il materiale didattico.

_DECISIONE_

I materiali possono essere caricati nei seguenti formati:

- PDF
- DOCX
- PPTX
- XLSX
- PNG
- JPG

La dimensione massima consentita per un singolo file è di 25 MB. Formato e dimensione vengono verificati dal backend, non soltanto dall'interfaccia. I file sono accessibili esclusivamente agli utenti autorizzati.

_MOTIVAZIONE_

-> Limitare i formati e la dimensione riduce i problemi di compatibilità, semplifica la gestione dello spazio di archiviazione e riduce i rischi derivanti dal caricamento di file non previsti.

**FR-STU-02 · Disponibilità e scadenza delle verifiche**

> Collegata a: DOC-02 — Creare le proprie verifiche; STU-02 — Svolgere una verifica.

_DECISIONE_

Ogni verifica può avere una data e un orario di apertura e una scadenza. Lo studente può iniziare la verifica solamente durante il periodo di disponibilità e deve consegnarla entro la scadenza.
Gli orari vengono interpretati nel fuso orario Europe/Rome. Il backend applica i controlli temporali, indipendentemente dall'orologio del dispositivo dello studente. Il Docente può prorogare la scadenza secondo le regole stabilite nel progetto.

_MOTIVAZIONE_

-> Regole temporali esplicite impediscono interpretazioni diverse delle scadenze e riducono la possibilità di iniziare o consegnare verifiche fuori dal periodo consentito.

**FR-STU-03 · Una sola consegna per verifica**

> Collegata a: STU-02 — Svolgere una verifica.

_DECISIONE_

Ogni studente può effettuare una sola consegna definitiva per ciascuna verifica. Dopo la conferma del server, le risposte vengono bloccate e non possono essere modificate dallo studente.
Se la richiesta di consegna viene inviata più volte, ad esempio da due schede del browser, il sistema registra una sola consegna.
Le risposte possono essere aggiornate durante lo svolgimento, fino alla consegna definitiva.

_MOTIVAZIONE_

-> Questa regola evita consegne duplicate e garantisce che il Docente valuti una sola versione definitiva delle risposte per ogni studente.

**FR-DIR-03 · Disattivazione degli account e conservazione dello storico**

> Collegata a: DIR-01 — Creare account docente; DIR-02 — Creare account studente; DIR-03 — Creare classi e comporle.

_DECISIONE_

Quando un utente non deve più accedere a ScuolaChill, il Direttore può disattivarne l'account. Un account disattivato non può autenticarsi, ma i dati didattici già registrati, come voti e verifiche consegnate, rimangono associati all'utente.
Una classe che contiene ancora studenti attivi o dati didattici collegati non può essere eliminata definitivamente: deve prima essere svuotata oppure archiviata.

_MOTIVAZIONE_

-> La disattivazione permette di revocare l'accesso senza compromettere lo storico didattico. L'archiviazione delle classi riduce il rischio di eliminare dati necessari alla consultazione dei risultati precedenti.

---

## Requisiti non funzionali

Ogni requisito ha una soglia, una condizione e un modo per verificarlo. Ed è collegato ad almeno una user story.

| ID     | Famiglia       | Requisito                     | Soglia e condizione                                                                                                                                                                               | Come si verifica                                           | Storie collegate                               |
| ------ | -------------- | ----------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------- | ---------------------------------------------- |
| NFR-01 | Prestazioni    | Rapidità delle API            | Almeno il 95% delle richieste principali deve ricevere risposta entro 2 secondi, con 300 utenti concorrenti nel test di carico.                                                                   | Test di carico                                             | DIR-04, DOC-01, STU-02, STU-03                 |
| NFR-02 | Sicurezza      | Autenticazione delle API      | Il 100% degli endpoint privati deve richiedere un'autenticazione valida.                                                                                                                          | Test API con Postman                                       | Tutte                                          |
| NFR-03 | Usabilità      | Interfaccia responsive        | Le funzioni principali devono essere utilizzabili su smartphone con larghezza di 375 px e su PC senza scroll orizzontale dell'intera pagina.                                                      | Test manuali su dispositivi differenti                     | STU-01, STU-03                                 |
| NFR-04 | Disponibilità  | Accessibilità del sistema     | Obiettivo di disponibilità mensile pari almeno al 99%, escluse le manutenzioni programmate.                                                                                                       | Monitoraggio automatico della raggiungibilità              | Tutte                                          |
| NFR-05 | Ambientale     | Uso efficiente delle risorse  | Il sistema deve utilizzare servizi cloud e dimensionare le risorse in base al carico stimato, evitando infrastrutture dedicate non necessarie.                                                    | Revisione dell'architettura e del dimensionamento          | Tutte                                          |
| NFR-06 | Supporto       | Diagnostica degli errori      | Ogni errore interno al server deve generare un log con codice dell'errore e identificativo della richiesta, senza registrare password o token completi.                                           | Verifica dei log e test degli errori                       | Tutte                                          |
| NFR-07 | Interazione    | Feedback delle operazioni     | Ogni operazione che richiede attesa deve mostrare uno stato di caricamento e un esito comprensibile, positivo o negativo.                                                                         | Test di usabilità                                          | DIR-01, DOC-01, DOC-02, DOC-03, STU-02         |
| NFR-08 | Conformità     | Protezione dei dati personali | Il sistema deve raccogliere solo i dati necessari alle funzionalità previste e impedire l'accesso ai dati personali da parte di utenti non autorizzati.                                           | Revisione dei permessi e test di sicurezza                 | DIR-01, DIR-02, DIR-04, STU-03                 |
| NFR-09 | Scalabilità    | Gestione dei picchi           | L'architettura deve consentire di aumentare le risorse del backend o il numero di istanze senza modificare le funzionalità applicative.                                                           | Test di carico e prova di scaling                          | DIR-04, STU-02                                 |
| NFR-10 | Sicurezza      | Comunicazioni cifrate         | Tutte le comunicazioni tra browser e backend in Production devono utilizzare HTTPS.                                                                                                               | Verifica del certificato e test delle connessioni          | Tutte                                          |
| NFR-11 | API            | Documentazione delle API      | Tutti gli endpoint principali devono essere descritti in OpenAPI/Swagger e verificabili tramite una collezione Postman.                                                                           | Revisione Swagger ed esecuzione della collezione           | Tutte                                          |
| NFR-12 | API            | Paginazione degli elenchi     | Gli endpoint che restituiscono collezioni devono supportare la paginazione, con una dimensione massima di 100 elementi per pagina.                                                                | Test API con Postman                                       | DIR-01, DIR-02, DIR-04, DOC-01, STU-01, STU-03 |
| NFR-13 | Affidabilità   | Gestione degli errori         | Tutti gli errori delle API devono utilizzare un formato uniforme e codici HTTP coerenti con il tipo di errore.                                                                                    | Test automatici degli endpoint                             | Tutte                                          |
| NFR-14 | Configurazione | Separazione degli ambienti    | Devono esistere almeno gli ambienti Development e Production, con configurazioni separate e nessun segreto inserito nel codice sorgente.                                                          | RRevisione della configurazione e scansione del repository | Tutte                                          |
| NFR-15 | Affidabilità   | Protezione dei dati salvati   | Dopo la conferma del server, una risposta di verifica o un voto registrato deve rimanere disponibile anche dopo una nuova autenticazione o un riavvio dell'applicazione.                          | Test di integrazione sul database                          | DOC-03, STU-02, STU-03                         |
| NFR-16 | Sicurezza      | Riservatezza dei voti         | Ogni studente può consultare esclusivamente i propri voti. Il 100% dei tentativi non autorizzati deve essere respinto dal backend.                                                                | Test di autorizzazione con Postman                         | STU-03                                         |
| NFR-17 | Interazione    | Modificabilità delle risposte | Durante lo svolgimento di una verifica, lo studente deve poter modificare le risposte prima della consegna definitiva. Dopo la consegna, le risposte non devono più essere modificabili.          | Test funzionali e test dell'interfaccia                    | STU-02                                         |
| NFR-18 | Interazione    | Conferma delle operazioni     | Ogni operazione di caricamento o salvataggio deve mostrare una conferma soltanto dopo la registrazione corretta sul server. In caso di errore, deve essere visualizzato un messaggio esplicativo. | Test manuali e test delle risposte API                     | DOC-01, DOC-02, DOC-03, STU-02                 |
| NFR-19 | Supporto       | Recupero dell'accesso         | Deve essere disponibile una procedura per recuperare una password dimenticata tramite un canale verificato. Il sistema non deve mai mostrare o inviare la password esistente in chiaro.           | Test del flusso di recupero e revisione della sicurezza    | Tutte                                          |

### Requisiti impliciti

Prima di chiudere questa sezione, intervista per dieci minuti un ragazzo del primo anno. La domanda è una sola. _"Cosa daresti per scontato che un'app di questo tipo faccia sempre, o non faccia mai?"_

| Chi avete intervistato | Cosa ha detto                                                                     | Requisito che ne avete ricavato |
| ---------------------- | --------------------------------------------------------------------------------- | ------------------------------- |
| _nome o iniziali_      | Non voglio che gli altri studenti possano vedere i miei voti                      | NFR-16                          |
| _nome o iniziali_      | Se sbaglio a inserire una risposta, voglio poterla correggere prima di consegnare | NFR-17                          |
|                        | Voglio sapere se il materiale che sto caricando è stato salvato davvero.          | NFR-18                          |
|                        | Se dimentico la password, voglio poter recuperare l'accesso.                      | NFR-19                          |

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
