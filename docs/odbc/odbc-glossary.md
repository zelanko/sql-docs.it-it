---
title: Glossario ODBC - Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC [ODBC], glossary
- glossary [ODBC]
ms.assetid: e8227000-1944-42e5-a881-1f549e1ff9d1
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ac454a8c57fe6e2f12724440dc37c3a1953e4c85
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302902"
---
# <a name="odbc-glossary"></a>Glossario di ODBC
## <a name="a"></a>Una  
 **piano di accesso**  
 Piano generato dal motore di database per eseguire un'istruzione SQL. Equivalente al codice eseguibile compilato da un linguaggio di terza generazione, ad esempio C.  
  
 **funzione di aggregazione**  
 Funzione che genera un singolo valore da un gruppo di valori, spesso utilizzata con le clausole **GROUP BY** e **HAVING.** Le funzioni di aggregazione includono **AVG**, **COUNT**, **MAX**, **MIN**e **SUM**. Noto anche come *funzioni set*. *Vedere anche* funzione scalare.  
  
 **ANSI**  
 American National Standards Institute. L'API ODBC è basata sull'interfaccia a livello di chiamata ANSI.  
  
 **APD**  
 *Vedere* descrittore di parametri dell'applicazione (APD).  
  
 **API**  
 Interfaccia di programmazione dell'applicazione. Set di routine utilizzate da un'applicazione per richiedere ed eseguire servizi di livello inferiore. L'API ODBC è composta dalle funzioni ODBC.  
  
 **applicazione**  
 Programma eseguibile che chiama funzioni nell'API ODBC.  
  
 **descrittore di parametro dell'applicazione (APD)**  
 Descrittore che descrive i parametri dinamici utilizzati in un'istruzione SQL prima di qualsiasi conversione specificata dall'applicazione.  
  
 **descrittore di riga dell'applicazione (ARD)**  
 Descrittore che rappresenta i metadati e i dati della colonna nei buffer dell'applicazione, che descrive una riga di dati dopo qualsiasi conversione di dati specificata dall'applicazione.  
  
 **Ard**  
 *Vedere* descrittore di riga dell'applicazione (ARD).  
  
 **modalità di commit automatico**  
 Modalità di commit della transazione in cui viene eseguito il commit delle transazioni immediatamente dopo l'esecuzione.  
  
## <a name="b"></a>b  
 **cambiamento comportamentale**  
 Modifica di determinate funzionalità dal comportamento di ODBC *3.x* al comportamento ODBC *2.x* o viceversa. Causato dalla modifica dell'attributo di ambiente SQL_ATTR_ODBC_VERSION.  
  
 **Oggetto binario di grandi dimensioni (BLOB)Binary large object (BLOB)**  
 Qualsiasi dato binario su un determinato numero di byte, ad esempio 255. In genere molto più a lungo. Tali dati vengono in genere inviati e recuperati dall'origine dati in parti. Noto anche come *dati lunghi*.  
  
 **Associazione**  
 Come verbo, atto di associare una colonna in un set di risultati o un parametro in un'istruzione SQL con una variabile di applicazione. Come sostantiva, l'associazione.  
  
 **offset di rilegatura**  
 Valore aggiunto agli indirizzi del buffer di dati e agli indirizzi del buffer di lunghezza/indicatore per tutti i dati di colonna o parametro associati, producendo nuovi indirizzi.  
  
 **cursore rettangolare**  
 Cursore in grado di recuperare più di una riga di dati alla volta.  
  
 **buffer**  
 Parte della memoria dell'applicazione utilizzata per passare i dati tra l'applicazione e il driver. I buffer sono spesso a coppie: un *buffer di dati* e un buffer di lunghezza dei *dati.*  
  
 **byte**  
 Otto bit o un ottetto. *Vedere anche* ottetto.  
  
## <a name="c"></a>C  
 **Tipo di dati C**  
 Il tipo di dati di una variabile in un programma C, in questo caso l'applicazione.  
  
 **Catalogo**  
 Set di tabelle di sistema in un database che descrive la forma del database. Noto anche come *schema* o *dizionario dei dati*.  
  
 **funzione di catalogo**  
 Funzione ODBC utilizzata per recuperare informazioni dal catalogo del database.  
  
 **CLI**  
 *Vedere vedi* Api.  
  
 **client/server**  
 Strategia di accesso al database in cui uno o più client accedono ai dati tramite un server. I client in genere implementano l'interfaccia utente mentre il server controlla l'accesso al database.  
  
 **Colonna**  
 Contenitore per un singolo elemento di informazioni in una riga. Noto anche come *campo*.  
  
 **Commettere**  
 Per rendere permanenti le modifiche in una transazione.  
  
 **Concorrenza**  
 La capacità di più transazioni di accedere agli stessi dati contemporaneamente.  
  
 **livello di conformità**  
 Set discreto di funzionalità supportate da un driver o da un'origine dati. ODBC definisce i livelli di conformità API e i livelli di conformità SQL.  
  
 **Connessione**  
 Istanza particolare di un driver e di un'origine dati.  
  
 **navigazione della connessione**  
 Ricerca nella rete per le origini dati a cui connettersi. L'esplorazione della connessione potrebbe richiedere diversi passaggi. Ad esempio, l'utente potrebbe prima sfogliare la rete per i server e quindi sfogliare un server specifico per un database.  
  
 **handle di connessione**  
 Handle per una struttura di dati che contiene informazioni su una connessione.  
  
 **riga corrente**  
 Riga attualmente a cui punta il cursore. Le operazioni posizionate agiscono sulla riga corrente.  
  
 **Cursore**  
 Componente software che restituisce righe di dati all'applicazione. Probabilmente chiamato dopo il cursore lampeggiante su un terminale di computer; così come il cursore indica la posizione corrente sullo schermo, un cursore su un set di risultati indica la posizione corrente nel set di risultati.  
  
## <a name="d"></a>D  
 **buffer di dati**  
 Buffer utilizzato per passare i dati. Spesso associato a un buffer di dati è un buffer di *lunghezza dei dati.*  
  
 **dizionario dei dati**  
 *Vedere* catalogo.  
  
 **buffer di lunghezza dei dati**  
 Buffer utilizzato per passare la lunghezza del valore in un *buffer di dati*corrispondente. Il buffer di lunghezza dei dati viene utilizzato anche per archiviare gli indicatori, ad esempio se il valore dei dati è con terminazione null.  
  
 **origine dati**  
 I dati a cui l'utente desidera accedere e il sistema operativo associato, DBMS e piattaforma di rete (se presente).  
  
 **tipo di dati**  
 Tipo di un dato. ODBC definisce i tipi di dati C e SQL. *Vedere anche* indicatore di tipo.  
  
 **colonna data-at-execution**  
 Colonna per cui i dati vengono inviati dopo la chiamata a **SQLSetPos.** Così denominato perché i dati vengono inviati in fase di esecuzione anziché essere inseriti in un buffer di set di righe. I dati lunghi vengono in genere inviati in parti in fase di esecuzione.  
  
 **Parametro data-at-execution**  
 Parametro per il quale i dati vengono inviati dopo la chiamata a **SQLExecute** o **SQLExecDirect.** Così denominato perché i dati vengono inviati quando viene eseguita l'istruzione SQL anziché essere inseriti in un buffer di parametri. I dati lunghi vengono in genere inviati in parti in fase di esecuzione.  
  
 **Database**  
 Raccolta discreta di dati in un DBMS. Anche un DBMS.  
  
 **motore di database**  
 Il software in un DBMS che analizza ed esegue istruzioni SQL e accede ai dati fisici.  
  
 **Dbms**  
 Sistema di gestione di database. Livello del software tra il database fisico e l'utente. Il sistema DBMS gestisce tutte le operazioni di accesso al database.  
  
 **Driver basato su DBMS**  
 Driver che accede ai dati fisici tramite un motore di database autonomo.  
  
 **DDL**  
 Linguaggio di definizione dei dati. Le istruzioni in SQL che definiscono, invece di manipolare, i dati. Ad esempio, **CREATE TABLE**, **CREATE INDEX**, **GRANT**e **REVOKE**.  
  
 **identificatore delimitato**  
 Identificatore racchiuso tra virgolette identificatore in modo che possa contenere caratteri speciali o parole chiave corrispondenti (noto anche come identificatore tra virgolette).  
  
 **Descrittore**  
 Struttura di dati che contiene informazioni sui dati delle colonne o sui parametri dinamici. La rappresentazione fisica del descrittore non è definita; applicazioni ottenere l'accesso diretto a un descrittore solo modificando ne i campi chiamando le funzioni ODBC con l'handle del descrittore.  
  
 **database desktop**  
 Un DBMS progettato per essere eseguito su un personal computer. In genere, questi DBSMO non forniscono un motore di database autonomo e devono essere accessibili tramite un driver basato su file. I motori in questi driver in genere hanno ridotto il supporto per SQL e le transazioni. Ad esempio, dBASE, Paradox, Btrieve o Microsoft® FoxPro®.  
  
 **Diagnostica**  
 Record contenente informazioni diagnostiche sull'ultima funzione chiamata che utilizzava un handle specifico. I record di diagnostica sono associati agli handle di ambiente, connessione, istruzione e descrittore.  
  
 **DML**  
 Linguaggio di manipolazione dei dati. Le istruzioni in SQL che modificano, anziché definire, i dati. Ad esempio **INSERT**, **UPDATE**, **DELETE**e **SELECT**.  
  
 **autista**  
 Libreria di routine che espone le funzioni nell'API ODBC. I driver sono specifici di un singolo DBMS.  
  
 **Gestione driver**  
 Libreria di routine che gestisce l'accesso ai driver per l'applicazione. Gestione Driver carica e scarica (o si connette e si disconnette da) driver e passa le chiamate alle funzioni ODBC per il driver corretto.  
  
 **DLL di installazione del driver**  
 DLL che contiene funzioni di installazione e configurazione specifiche del driver.  
  
 **cursore dinamico**  
 Cursore scorrevole in grado di rilevare le righe aggiornate, eliminate o inserite nel set di risultati.  
  
 **SQL dinamico**  
 Tipo di SQL incorporato in cui le istruzioni SQL vengono create e compilate in fase di esecuzione. *Vedere anche* SQL statico.  
  
## <a name="e"></a>E  
 **SQL incorporato**  
 Le istruzioni SQL incluse direttamente in un programma scritto in un altro linguaggio, ad esempio COBOL o C. ODBC, non utilizzaNO CODICE SQL incorporato. *Vedere anche* SQL statico *e* SQL dinamico.  
  
 **Ambiente**  
 Un contesto globale in cui accedere ai dati; associati all'ambiente è qualsiasi informazione di natura globale, ad esempio un elenco di tutte le connessioni in tale ambiente.  
  
 **maniglia dell'ambiente**  
 Handle per una struttura di dati che contiene informazioni sull'ambiente.  
  
 **clausola di escape**  
 Clausola in un'istruzione SQL.  
  
 **Eseguire**  
 Per eseguire un'istruzione SQL.  
  
## <a name="f"></a>F  
 **cursore grasso**  
 *Vedere* cursore a blocchi.  
  
 **Prendere**  
 Per recuperare una o più righe da un set di risultati.  
  
 **Campo**  
 *Vedere* la colonna.  
  
 **driver basato su file**  
 Driver che accede direttamente ai dati fisici. In questo caso, il driver contiene un motore di database e funge da driver e origine dati.  
  
 **origine dati file**  
 Origine dati per la quale le informazioni di connessione vengono archiviate in un file DSN.  
  
 **chiave esterna**  
 Una o più colonne in una tabella che corrispondono alla chiave primaria di un'altra tabella.  
  
 **cursore forward-only**  
 Cursore che può spostarsi solo in avanti nel set di risultati e in genere recupera solo una riga alla volta. La maggior parte dei database relazionali supporta solo cursori forward-only.  
  
## <a name="h"></a>H  
 **Gestire**  
 Valore che identifica in modo univoco un elemento, ad esempio un file o una struttura di dati. Gli handle sono significativi solo per il software che li crea e li utilizza, ma vengono passati da altri software per identificare le cose. ODBC definisce gli handle per ambienti, connessioni, istruzioni e descrittori.  
  
## <a name="i"></a>I  
 **descrittore del parametro di implementazione (IPD)**  
 Descrittore che descrive i parametri dinamici utilizzati in un'istruzione SQL dopo qualsiasi conversione specificata dall'applicazione.  
  
 **descrittore di riga di implementazione (IRD)**  
 Descrittore che descrive una riga di dati prima di qualsiasi conversione specificata dall'applicazione.  
  
 **DLL del programma di installazione**  
 DLL che installa i componenti ODBC e configura le origini dati.  
  
 **Struttura di miglioramento dell'integrità**  
 Sottoinsieme di SQL progettato per mantenere l'integrità di un database.  
  
 **livello di conformità dell'interfaccia**  
 Livello dell'interfaccia ODBC 3.7 supportata da un driver. può essere Core, Livello 1 o Livello 2.  
  
 **Interoperabilità**  
 La capacità di un'applicazione di utilizzare lo stesso codice quando si accede ai dati in DBS diversi.  
  
 **IPD**  
 *Vedere vedi* Descrittore del parametro di implementazione (IPD).  
  
 **Ird**  
 *Vedere vedi* Descrittore di riga di implementazione (IRD).  
  
 **ISO/IEC**  
 Organizzazione internazionale degli standard/Commissione elettrotecnica internazionale. L'API ODBC è basata sull'interfaccia a livello di chiamata ISO/IEC.  
  
## <a name="j"></a>J  
 **Unirsi**  
 Operazione in un database relazionale che collega le righe di due o più tabelle facendo corrispondere i valori nelle colonne specificate.  
  
## <a name="k"></a>K  
 **Chiave**  
 Colonna o colonne i cui valori identificano una riga. *Vedere anche* chiave esterna *e* chiave primaria.  
  
 **Keyset**  
 Set di tasti utilizzati da un cursore misto o basato su keyset per recuperare le righe.  
  
 **cursore gestito da keyset**  
 Cursore scorrevole che rileva le righe aggiornate ed eliminate utilizzando un keyset.  
  
## <a name="l"></a>L  
 **Letterale**  
 Rappresentazione di caratteri di un valore di dati effettivo in un'istruzione SQL.  
  
 **Blocco**  
 Processo mediante il quale un DBMS limita l'accesso a una riga in un ambiente multiutente. Il DBMS in genere imposta un bit su una riga o la pagina fisica contenente una riga che indica che la riga o la pagina è bloccata.  
  
 **dati lunghi**  
 Qualsiasi dati binari o di tipo carattere di lunghezza superiore a una determinata lunghezza, ad esempio 255 byte o caratteri. In genere molto più a lungo. Tali dati vengono in genere inviati e recuperati dall'origine dati in parti. Noto anche come *BLOB*s o *CLOB*s.  
  
## <a name="m"></a>M  
 **origine dati macchina**  
 Origine dati per la quale le informazioni di connessione vengono archiviate nel sistema, ad esempio il Registro di sistema.  
  
 **modalità di commit manuale**  
 Modalità di commit delle transazioni in cui è necessario eseguire il commit esplicito delle transazioni chiamando **SQLTransact**.  
  
 **Metadati**  
 Dati che descrivono un parametro in un'istruzione SQL o in una colonna in un set di risultati. Ad esempio, il tipo di dati, la lunghezza in byte e la precisione di un parametro.  
  
 **driver a più livelli**  
 *Vedere vedi* Driver basato su DBMS.  
  
## <a name="n"></a>N  
 **Valore NULL**  
 Non è stato assegnato in modo esplicito alcun valore. In particolare, un valore NULL è diverso da zero o vuoto.  
  
## <a name="o"></a>O  
 **Ottetto**  
 Otto bit o un byte. *Vedere anche* byte.  
  
 **lunghezza dell'ottetto**  
 Lunghezza in ottetti di un buffer o dei dati in esso contenuti.  
  
 **ODBC**  
 Aprire Connettività database. Specifica per un'API che definisce un set standard di routine con cui un'applicazione può accedere ai dati in un'origine dati.  
  
 **Amministratore ODBC**  
 Programma eseguibile che chiama la DLL del programma di installazione per configurare le origini dati.  
  
 Apri gruppo  
 Una società che pubblica gli standard. In particolare, pubblica gli standard DEL gruppo di accesso SQL (SAG).  
  
 **concorrenza ottimistica**  
 Strategia per aumentare la concorrenza in cui le righe non sono bloccate. Invece, prima di essere aggiornati o eliminati, un cursore controlla se sono stati modificati dopo l'ultima lettura. In tal caso, l'aggiornamento o l'eliminazione non riesce. *Vedere anche* concorrenza pessimistica.  
  
 **join esterno**  
 Join in cui vengono restituite sia le righe corrispondenti che non corrispondenti. I valori di tutte le colonne della tabella non corrispondente nelle righe non corrispondenti sono impostati su NULL.  
  
 **Proprietario**  
 Il proprietario di un tavolo.  
  
## <a name="p"></a>P  
 **Parametro**  
 Variabile in un'istruzione SQL, contrassegnata con un indicatore di parametro o un punto interrogativo (?). I parametri sono associati alle variabili di applicazione e ai relativi valori recuperati quando viene eseguita l'istruzione.  
  
 **descrittore di parametro**  
 Descrittore che descrive i parametri di runtime utilizzati in un'istruzione SQL, prima di qualsiasi conversione specificata dall'applicazione (un descrittore di parametri dell'applicazione o APD) o dopo qualsiasi conversione specificata dall'applicazione (un descrittore di parametro di implementazione o IPD).  
  
 **matrice di operazioni di parametri**  
 Matrice contenente valori che un'applicazione può impostare per indicare che il parametro corrispondente deve essere ignorato in un'operazione **SQLExecDirect** o **SQLExecute.**  
  
 **matrice di stato dei parametri**  
 Matrice contenente lo stato di un parametro dopo una chiamata a **SQLExecDirect** o **SQLExecute**.  
  
 **concorrenza pessimistica**  
 Strategia per l'implementazione della serializzabilità, in cui le righe sono bloccate in modo che altre transazioni non possano modificarle. *Vedere anche* concorrenza ottimistica *e* serializzabilità.  
  
 **funzionamento posizionato**  
 Qualsiasi operazione che agisce sulla riga corrente. Ad esempio, le istruzioni di aggiornamento ed eliminazione posizionate, **SQLGetData**e **SQLSetPos**.  
  
 **istruzione di aggiornamento posizionato**  
 Istruzione SQL utilizzata per aggiornare i valori nella riga corrente.  
  
 **istruzione delete posizionata**  
 Istruzione SQL utilizzata per eliminare la riga corrente.  
  
 **Preparare**  
 Per compilare un'istruzione SQL. Un piano di accesso viene creato preparando un'istruzione SQL.  
  
 **chiave primaria**  
 Colonna o colonne che identificano in modo univoco una riga in una tabella.  
  
 **Procedura**  
 Gruppo di una o più istruzioni SQL precompilate archiviate come oggetto denominato in un database.  
  
 **colonna procedura**  
 Argomento in una chiamata di routine, valore restituito da una routine o colonna in un set di risultati creato da una routine.  
  
## <a name="q"></a>Q  
 **Qualificatore**  
 Database che contiene una o più tabelle.  
  
 **Query**  
 Un'istruzione SQL. A volte utilizzato per indicare un'istruzione **SELECT.**  
  
 **quoted identifier**  
 Identificatore racchiuso tra virgolette identificatore in modo che possa contenere caratteri speciali o parole chiave corrispondenti (noto anche in SQL-92 come identificatore delimitato).  
  
## <a name="r"></a>R  
 **Radix**  
 La base di un sistema numerico. Di solito 2 o 10.  
  
 **Registrazione**  
 *Vedi* riga.  
  
 **set di risultati**  
 Set di righe create eseguendo un'istruzione **SELECT.**  
  
 **codice di ritorno**  
 Valore restituito da una funzione ODBC.  
  
 **rollback**  
 Per riportare i valori modificati da una transazione allo stato originale.  
  
 **Riga**  
 Set di colonne correlate che descrivono un'entità specifica. Noto anche come *record*.  
  
 **descrittore di riga**  
 Descrittore che descrive le colonne di un set di risultati, prima di qualsiasi conversione specificata dall'applicazione (un descrittore di riga di implementazione o IRD) o dopo qualsiasi conversione specificata dall'applicazione (un descrittore di riga dell'applicazione o ARD).  
  
 **matrice di operazioni di riga**  
 Matrice contenente i valori che un'applicazione può impostare per indicare che la riga corrispondente deve essere ignorata in un'operazione **SQLSetPos.**  
  
 **matrice di stato delle righe**  
 Matrice contenente lo stato di una riga dopo una chiamata a **SQLFetch**, **SQLFetchScroll**o **SQLSetPos**.  
  
 **Righe**  
 Set di righe restituito in un singolo recupero da un cursore a blocchi.  
  
 **buffer di set di righeRowset buffers**  
 I buffer associati alle colonne di un set di risultati e in cui vengono restituiti i dati per un intero set di righe.  
  
## <a name="s"></a>S  
 **Sag**  
 *Vedere vedi* SQL Access Group (SAG).  
  
 **funzione scalare**  
 Funzione che genera un singolo valore da un singolo valore. Ad esempio, una funzione che modifica le maiuscole/minuscole dei dati di tipo carattere.  
  
 **Schema**  
 *Vedere* catalogo.  
  
 **cursore scorrevole**  
 Cursore che può spostarsi avanti o indietro nel set di risultati.  
  
 **serializzabilità**  
 Se due transazioni in esecuzione contemporaneamente producono un risultato che è uguale all'esecuzione seriale (o sequenziale) di tali transazioni. Le transazioni serializzabili sono necessarie per mantenere l'integrità del database.  
  
 **database del server**  
 Un DBMS progettato per essere eseguito in un ambiente client/server. Questi DBSMO forniscono un motore di database autonomo che fornisce supporto completo per SQL e le transazioni. È possibile accedervi tramite driver basati su DBMS. Ad esempio, Oracle, Informix, DB/2 o Microsoft® SQL Server.  
  
 **set (funzione)**  
 *Vedere* funzione di aggregazione.  
  
 **DLL di installazione**  
 *Vedere* DLL di installazione del driver *e* DLL di installazione del convertitore.  
  
 **driver a livello singolo**  
 *Vedere* Driver basato su file.  
  
 **SQL**  
 Linguaggio di query strutturato. Linguaggio utilizzato dai database relazionali per eseguire query, aggiornare e gestire i dati.  
  
 **Gruppo di accesso SQL (SAG)SQL Access Group (SAG)**  
 Un consorzio di settore di aziende che si occupano di DBS SQL. L'interfaccia a livello di chiamata del gruppo aperto si basa sul lavoro eseguito originariamente dal gruppo di accesso SQL.  
  
 **Livello di conformità SQL**  
 Livello di grammatica SQL-92 supportato da un driver; può essere Entry, FIPS Transitional, Intermediate o Full.  
  
 **Tipo di dati SQL**  
 Tipo di dati di una colonna o di un parametro archiviato nell'origine dati.  
  
 **SQLSTATE**  
 Valore di cinque caratteri che indica un errore specifico.  
  
 **Istruzione SQL**  
 Una frase completa in SQL che inizia con una parola chiave e descrive completamente un'azione da intraprendere. Ad esempio, SELECT e FROM Orders. Le istruzioni SQL non devono essere confuse con le istruzioni.  
  
 **Stato**  
 Condizione ben definita di un elemento. Ad esempio, una connessione ha sette stati, tra cui dati non allocati, allocati, connessi e necessari. Alcune operazioni possono essere eseguite solo quando un elemento si trova in uno stato particolare. Ad esempio, una connessione può essere liberata solo quando si trova in uno stato allocato e non, ad esempio, quando è in uno stato connesso.  
  
 **transizione di stato**  
 Il movimento di un elemento da uno stato all'altro. ODBC definisce transizioni di stato rigorose per ambienti, connessioni e istruzioni.  
  
 **affermazione**  
 Contenitore per tutte le informazioni relative a un'istruzione SQL. Le istruzioni non devono essere confuse con le istruzioni SQL.  
  
 **handle di istruzione**  
 Handle a una struttura di dati che contiene informazioni su un'istruzione.  
  
 **cursore statico**  
 Cursore scorrevole che non è in grado di rilevare aggiornamenti, eliminazioni o inserimenti nel set di risultati. Di solito implementato creando una copia del set di risultati.  
  
 **SQL statico**  
 Tipo di SQL incorporato in cui le istruzioni SQL vengono hardcoded e compilate quando viene compilato il resto del programma. *Vedere anche* SQL dinamico.  
  
 **stored procedure**  
 *Vedere* la procedura.  
  
## <a name="t"></a>T  
 **tavolo**  
 Raccolta di righe.  
  
 **Thunk**  
 Conversione di indirizzi a 16 bit in indirizzi a 32 bit, o viceversa, quando le applicazioni a 16 bit vengono utilizzate con driver ODBC a 32 bit.  
  
 **Transazione**  
 Unità di lavoro atomica. Il lavoro in una transazione deve essere completato nel suo complesso. Se qualsiasi parte della transazione non riesce, l'intera transazione avrà esito negativo.  
  
 **isolamento delle transazioni**  
 L'atto di isolare una transazione dagli effetti di tutte le altre transazioni.  
  
 **livello di isolamento delle transazioni**  
 Misura dell'isolamento di una transazione. Esistono cinque livelli di isolamento delle transazioni: Lettura senza commit, Lettura committed, Lettura ripetibile, Serializable e Controllo delle versioni.  
  
 **DLL traduttore**  
 DLL utilizzata per convertire i dati da un set di caratteri a un altro.  
  
 **DLL di installazione del traduttore**  
 DLL che contiene funzioni di installazione e configurazione specifiche del convertitore.  
  
 **commit in due fasi**  
 Processo di commit di una transazione distribuita in due fasi. Nella prima fase, il processore delle transazioni verifica che sia possibile eseguire il commit di tutte le parti della transazione. Nella seconda fase viene eseguito il commit di tutte le parti della transazione. Se una parte qualsiasi della transazione indica nella prima fase che non è possibile eseguire il commit, la seconda fase non viene eseguita. ODBC non supporta i commit in due fasi.  
  
 **indicatore di tipo**  
 Valore integer passato o restituito da una funzione ODBC per indicare il tipo di dati di una variabile di applicazione, di un parametro o di una colonna. ODBC definisce gli indicatori di tipo per entrambi i tipi di dati C e SQL.  
  
## <a name="v"></a>V  
 **Mostra**  
 Un modo alternativo di esaminare i dati in una o più tabelle. Una vista viene in genere creata come sottoinsieme delle colonne di una o più tabelle. In ODBC, le viste sono in genere equivalenti alle tabelle.
