---
title: Glossario ODBC | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 33116adaf74ed2d3fc52fec460859a7672ce2d0a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63057783"
---
# <a name="odbc-glossary"></a>Glossario di ODBC
## <a name="a"></a>A  
 **piano di accesso**  
 Un piano generato dal motore di database per eseguire un'istruzione SQL. Equivalente a codice eseguibile compilato da un linguaggio di terza generazione, ad esempio C.  
  
 **Funzione di aggregazione**  
 Una funzione che genera un singolo valore da un gruppo di valori, spesso abbinata **GROUP BY** e **HAVING** clausole. Includono le funzioni di aggregazione **AVG**, **conteggio**, **MAX**, **MIN**, e **somma**. Noto anche come *funzioni set*. *Vedere anche* funzione scalare.  
  
 **ANSI**  
 American National Standards Institute. L'API ODBC si basa sull'interfaccia ANSI a livello di chiamata.  
  
 **APD**  
 *Vedere* descrittore del parametro dell'applicazione (APD).  
  
 **API**  
 Application Programming Interface. Un set di routine che un'applicazione utilizza per richiedere e svolgere servizi di livello inferiore. L'API ODBC è costituita da funzioni di ODBC.  
  
 **application**  
 Un programma eseguibile che chiama le funzioni dell'API ODBC.  
  
 **descrittore del parametro dell'applicazione (APD)**  
 Un descrittore che descrive i parametri dinamici in un'istruzione SQL prima di qualsiasi conversione specificato dall'applicazione.  
  
 **descrittore della riga di applicazione (ARD)**  
 Un descrittore che rappresenta i metadati di colonna e i dati nei buffer dell'applicazione, che descrive una riga di dati dopo qualsiasi conversione di dati specificato dall'applicazione.  
  
 **ARD**  
 *Vedere* descrittore delle righe dell'applicazione (ARD).  
  
 **la modalità autocommit**  
 Una modalità di commit delle transazioni in cui vengono eseguito il commit delle transazioni immediatamente dopo che vengono eseguite.  
  
## <a name="b"></a>B  
 **Modifica comportamentale**  
 Una modifica determinate funzionalità da ODBC 3 *. x* comportamento a ODBC 2. *x* comportamento, o viceversa. Generato modificando l'attributo di ambiente SQL_ATTR_ODBC_VERSION.  
  
 **Oggetto binario di grandi dimensioni (BLOB)**  
 Qualsiasi dato binario in un determinato numero di byte, ad esempio 255. In genere molto più tempo. Questo tipo di dati è in genere inviato da e recuperato dall'origine dei dati in parti. Noto anche come *dati di tipo long*.  
  
 **binding**  
 Descrive un'operazione, l'atto di associazione di una colonna in un set di risultati o un parametro in un'istruzione SQL con una variabile di applicazione. Come sostantivo, l'associazione.  
  
 **offset di associazione**  
 Un valore aggiunto per gli indirizzi di buffer di lunghezza/indicatore e gli indirizzi di buffer dei dati per tutti associata a una colonna o parametro nuovi indirizzi dei dati, che produce.  
  
 **cursore a blocchi**  
 Un cursore in grado di recuperare più righe di dati alla volta.  
  
 **buffer**  
 Una parte della memoria dell'applicazione usata per passare dati tra le applicazioni e driver. I buffer sono spesso in coppie: una *buffer di dati* e una *buffer di lunghezza dati*.  
  
 **byte**  
 Otto bit o a un ottetto. *Vedere anche* ottetto.  
  
## <a name="c"></a>c  
 **Tipo di dati C**  
 Il tipo di dati di una variabile in un programma C, in questo caso l'applicazione.  
  
 **catalog**  
 Il set di tabelle di sistema in un database che descrivono la forma del database. Noto anche come un *schema* oppure *dizionario dei dati*.  
  
 **funzione di catalogo**  
 Una funzione ODBC consente di recuperare informazioni dal catalogo del database.  
  
 **CLI**  
 *Vedere* API.  
  
 **client/server**  
 Una strategia di accesso del database in cui uno o più client di accedere ai dati tramite un server. I client in genere implementano l'interfaccia utente mentre i controlli server di accesso al database.  
  
 **column**  
 Il contenitore per un singolo elemento di informazioni in una riga. Noto anche come *campo*.  
  
 **commit**  
 Per rendere permanenti le modifiche in una transazione.  
  
 **concurrency**  
 La possibilità di più transazioni accedono agli stessi dati nello stesso momento.  
  
 **Livello di conformità**  
 Un set discreto di funzionalità supportate da un'origine dati o driver. ODBC definisce i livelli di conformità API e i livelli di conformità SQL.  
  
 **connection**  
 Un'istanza specifica di un driver e l'origine dati.  
  
 **connessione di esplorazione**  
 La ricerca della rete per le origini dati a cui connettersi. Esplorazione di connessione possono includere diversi passaggi. Ad esempio, l'utente potrebbe esplorare innanzitutto la rete per i server e quindi selezionare un server specifico per un database.  
  
 **handle di connessione**  
 Handle a una struttura di dati che contiene informazioni su una connessione.  
  
 **Riga corrente**  
 La riga a cui punta il cursore. Operazioni posizionate agiscono sulla riga corrente.  
  
 **cursor**  
 Un componente software che restituisce righe di dati all'applicazione. Probabilmente denominata dopo il cursore lampeggia in un computer terminal; come tale cursore indica la posizione corrente nella schermata, un cursore su un set di risultati indica la posizione corrente nel set di risultati.  
  
## <a name="d"></a>D  
 **buffer dei dati**  
 Buffer usato per passare i dati. Spesso associato con dati di un buffer è un *buffer di lunghezza dati*.  
  
 **dizionario dei dati**  
 *Vedere* catalogo.  
  
 **buffer di lunghezza dei dati**  
 Un buffer utilizzato per passare la lunghezza del valore di un oggetto corrispondente *buffer dei dati*. Il buffer di lunghezza dei dati viene usato anche per archiviare gli indicatori, ad esempio se il valore dei dati è con terminazione null.  
  
 **Origine dati**  
 I dati che l'utente desidera l'accesso e la relativa del sistema operativo associati, DBMS e piattaforma di rete (se presente).  
  
 **Tipo di dati**  
 Il tipo di una porzione di dati. ODBC definisce tipi di dati C e SQL. *Vedere anche* indicatore del tipo.  
  
 **colonna data-at-execution**  
 Una colonna per cui i dati vengono inviati dopo **SQLSetPos** viene chiamato. Così chiamati perché i dati vengono inviati in fase di esecuzione anziché inserite in un buffer di righe. Dati Long in genere vengono inviati in parti in fase di esecuzione.  
  
 **parametro data-at-execution**  
 Un parametro per il quale i dati vengono inviati dopo **SQLExecute** oppure **SQLExecDirect** viene chiamato. Così chiamati perché i dati vengono inviati quando viene eseguita l'istruzione SQL anziché essere inserito in un buffer del parametro. Dati Long in genere vengono inviati in parti in fase di esecuzione.  
  
 **database**  
 Raccolta discreta di dati in un sistema DBMS. Anche un DBMS.  
  
 **Motore di database**  
 Il software in un sistema DBMS che analizza ed esegue istruzioni SQL e accede ai dati fisici.  
  
 **DBMS**  
 Sistema di gestione di database. Livello del software tra il database fisico e l'utente. Il sistema DBMS gestisce tutte le operazioni di accesso al database.  
  
 **Driver basati su DBMS**  
 Un driver che accede ai dati fisici tramite un motore di database autonomo.  
  
 **DDL**  
 Data Definition Language. Tali istruzioni SQL che definiscono, in contrapposizione per manipolare i dati. Ad esempio, **CREATE TABLE**, **CREATE INDEX**, **GRANT**, e **revocare**.  
  
 **identificatore delimitato**  
 Un identificatore che è racchiuso tra virgolette identificatore in modo che può contenere caratteri speciali o corrispondere a parole chiave (nota anche come un identificatore con virgolette).  
  
 **descriptor**  
 Una struttura di dati che contiene informazioni sui dati delle colonne o parametri dinamici. La rappresentazione fisica del descrittore non è definita; le applicazioni accedono diretto a un descrittore solo modificando i campi chiamando le funzioni ODBC con l'handle descrittore.  
  
 **database desktop**  
 Un DBMS progettato per essere eseguito su un personal computer. Questi DBMS in generale, non si fornisce un motore di database autonoma e deve essere accessibile tramite un driver basati su file. I motori di questi driver in genere hanno ridotto il supporto per SQL e le transazioni. Ad esempio, dBASE, Paradox, Btrieve o Microsoft® FoxPro.  
  
 **diagnostic**  
 Un record contenente informazioni diagnostiche sull'ultima funzione chiamata che è usato un handle specifico. I record di diagnostica associati all'ambiente, connessione, istruzione e gli handle di descrittore.  
  
 **DML**  
 Data Manipulation Language. Tali istruzioni SQL che modificano, anziché per definire, i dati. Ad esempio, **inserire**, **UPDATE**, **Elimina**, e **selezionare**.  
  
 **driver**  
 Una routine della libreria che espone le funzioni dell'API ODBC. I driver sono specifici di un singolo DBMS.  
  
 **Driver Manager**  
 Una libreria di routine che gestisce l'accesso al driver per l'applicazione. Gestione Driver carica e scarica (o si connette a e si disconnette dalla) i driver e passa le chiamate a funzioni ODBC per il driver corretto.  
  
 **DLL di installazione di driver**  
 Una DLL che contiene funzioni di installazione e configurazione specifiche del driver.  
  
 **cursore dinamico**  
 Un cursore scorrevole è in grado di rilevare le righe aggiornate, eliminate o inserite nel set di risultati.  
  
 **SQL dinamico**  
 Un tipo di embedded SQL SQL le istruzioni vengono create e compilate in fase di esecuzione. *Vedere anche* SQL statico.  
  
## <a name="e"></a>E  
 **Embedded SQL**  
 Le istruzioni SQL che sono inclusi direttamente in un programma scritto in un altro linguaggio, ad esempio COBOL o ODBC C. non usare SQL incorporato. *Vedere anche* SQL statico *e* istruzioni SQL dinamiche.  
  
 **environment**  
 Un contesto globale in cui si desidera accedere ai dati; associato all'ambiente sono le informazioni che sono globale in natura, ad esempio un elenco di tutte le connessioni in quell'ambiente.  
  
 **handle di ambiente**  
 Handle a una struttura di dati che contiene informazioni sull'ambiente.  
  
 **clausola di escape**  
 Una clausola in un'istruzione SQL.  
  
 **execute**  
 Per eseguire un'istruzione SQL.  
  
## <a name="f"></a>F  
 **cursore a blocchi**  
 *Vedere* cursore a blocchi.  
  
 **fetch**  
 Per recuperare uno o più righe da un set di risultati.  
  
 **field**  
 *Vedere* colonna.  
  
 **driver basati su file**  
 Un driver che accede ai dati fisici direttamente. In questo caso, il driver contiene un motore di database e funge da origine dati e del driver.  
  
 **origine dati file**  
 Un'origine dati per la connessione che informazioni vengono archiviate in un file DSN.  
  
 **Chiave esterna**  
 Una o più colonne in una tabella che corrispondono alla chiave primaria in un'altra tabella.  
  
 **cursore forward-only**  
 Un cursore che può solo avanzare attraverso il set di risultati e in genere viene recuperato solo una riga alla volta. La maggior parte dei database relazionali supportano solo i cursori forward-only.  
  
## <a name="h"></a>H  
 **handle**  
 Un valore che identifica in modo univoco un elemento, ad esempio una struttura di dati o file. Gli handle sono significativi solo per il software che consente di creare e li Usa, ma viene passato da un altro software per identificare le cose. ODBC definisce gli handle per gli ambienti, le connessioni, le istruzioni e i descrittori.  
  
## <a name="i"></a>I  
 **Descrizione del parametro di implementazione (IPD)**  
 Un descrittore che descrive i parametri dinamici in un'istruzione SQL dopo la conversione specificata dall'applicazione.  
  
 **descrittore della riga di implementazione (IRD)**  
 Un descrittore che descrive una riga di dati prima di qualsiasi conversione specificato dall'applicazione.  
  
 **DLL di installazione**  
 Una DLL che vengono installati i componenti ODBC e configura le origini dei dati.  
  
 **Funzionalità di miglioramento dell'integrità**  
 Un sottoinsieme di SQL è progettato per mantenere l'integrità di un database.  
  
 **livello di conformità di interfaccia**  
 Il livello dell'interfaccia ODBC 3.7 supportata da un driver; può essere Core, livello 1 o 2 di livello.  
  
 **interoperability**  
 La capacità di un'applicazione per usare lo stesso codice quando accede ai dati in diversi DBMS.  
  
 **IPD**  
 *Vedere* descrizione del parametro di implementazione (IPD).  
  
 **IRD**  
 *Vedere* descrittore delle righe di implementazione (IRD).  
  
 **ISO/IEC**  
 Organizzazione/International Electrotechnical Commission standard internazionali. L'API ODBC si basa sull'interfaccia ISO/IEC a livello di chiamata.  
  
## <a name="j"></a>J  
 **join**  
 Un'operazione in un database relazionale che collega le righe in due o più tabelle associando i valori nelle colonne specificate.  
  
## <a name="k"></a>K  
 **key**  
 Una o più colonne i cui valori identificano una riga. *Vedere anche* chiave esterna *e* chiave primaria.  
  
 **keyset**  
 Un set di chiavi utilizzata da un cursore gestito da keyset o misto recuperi nuovamente le righe.  
  
 **cursore gestito da keyset**  
 Un cursore scorrevole che consente di rilevare le righe aggiornate ed eliminate tramite un set di chiavi.  
  
## <a name="l"></a>L  
 **literal**  
 Una rappresentazione di caratteri di un valore effettivo dei dati in un'istruzione SQL.  
  
 **locking**  
 Il processo mediante il quale un DBMS limita l'accesso a una riga in un ambiente multiutente. Il sistema DBMS in genere imposta un bit su una riga o pagina fisica che contiene una riga che indica la riga o una pagina viene bloccata.  
  
 **dati di tipo Long**  
 Tutti i dati caratteri o binari in una determinata lunghezza, ad esempio 255 byte o caratteri. In genere molto più tempo. Questo tipo di dati è in genere inviato da e recuperato dall'origine dei dati in parti. Noto anche come *BLOB*s oppure *CLOB*s.  
  
## <a name="m"></a>M  
 **zdroj dat macchina**  
 Un'origine dati per la connessione che informazioni vengono archiviate nel sistema (ad esempio, il Registro di sistema).  
  
 **Commit manuale**  
 Una modalità di commit delle transazioni in cui devono essere in modo esplicito il commit delle transazioni chiamando **SQLTransact**.  
  
 **metadata**  
 Dati che descrivono un parametro in un'istruzione SQL o una colonna in un set di risultati. Ad esempio, il tipo di dati, lunghezza in byte e precisione di un parametro.  
  
 **driver a più livelli**  
 *Vedere* driver basati su DBMS.  
  
## <a name="n"></a>N  
 **Valore NULL**  
 Non avere alcun valore assegnato in modo esplicito. In particolare, un valore NULL è diverso da zero o uno spazio vuoto.  
  
## <a name="o"></a>O  
 **octet**  
 Otto bit o un byte. *Vedere anche* byte.  
  
 **lunghezza dell'ottetto**  
 La lunghezza in ottetti di dati in che essa contenuti o un buffer.  
  
 **ODBC**  
 Apre la connettività di Database. Specifica per un'API che definisce un set standard di routine con cui un'applicazione può accedere ai dati in un'origine dati.  
  
 **Amministratore ODBC**  
 Un programma eseguibile che chiama la DLL per configurare le origini dati di installazione.  
  
 Apri gruppo  
 Una società che pubblica gli standard. In particolare, pubblica gruppo di accesso SQL (SAG) standard.  
  
 **concorrenza ottimistica**  
 Una strategia per aumentare la concorrenza in cui le righe non bloccate. Al contrario, prima di essere aggiornati o eliminati, un cursore controlla se sono state modificate dall'ultima lettura. In questo caso, update o delete ha esito negativo. *Vedere anche* concorrenza pessimistica.  
  
 **outer join**  
 Un join in cui vengono restituite le righe senza corrispondenza e corrispondenti. I valori di tutte le colonne della tabella non corrispondenti nelle righe non corrispondenti vengono impostati su NULL.  
  
 **owner**  
 Il proprietario di una tabella.  
  
## <a name="p"></a>P  
 **parameter**  
 Una variabile in un'istruzione SQL, contrassegnata con un marcatore di parametro o un punto interrogativo (?). I parametri sono associati a variabili di applicazione e i relativi valori recuperati quando viene eseguita l'istruzione.  
  
 **descrittore del parametro**  
 Un descrittore che descrive i parametri di runtime usati in un'istruzione SQL, sia prima di qualsiasi conversione specificata dall'applicazione (un descrittore di parametri dell'applicazione o APD) o dopo qualsiasi conversione specificato dall'applicazione (un'implementazione descrittore del parametro o IPD).  
  
 **Matrice di parametri operazione**  
 Matrice contenente i valori che un'applicazione può impostare per indicare che il parametro corrispondente deve essere ignorato un' **SQLExecDirect** oppure **SQLExecute** operazione.  
  
 **Matrice di stato di parametro**  
 Matrice che contiene lo stato di un parametro dopo una chiamata a **SQLExecDirect** oppure **SQLExecute**.  
  
 **concorrenza pessimistica**  
 Una strategia per l'implementazione la serializzabilità è infatti, in cui le righe vengono bloccate in modo che altre transazioni non è possibile modificarle. *Vedere anche* la concorrenza ottimistica *e* serializzabilità.  
  
 **operazione posizionata**  
 Qualsiasi operazione che influenza sulla riga corrente. Ad esempio, posizionato update ed eliminare le istruzioni **SQLGetData**, e **SQLSetPos**.  
  
 **istruzione di aggiornamento posizionato**  
 Un'istruzione SQL utilizzata per aggiornare i valori nella riga corrente.  
  
 **istruzione delete posizionate**  
 Un'istruzione SQL utilizzata per eliminare la riga corrente.  
  
 **prepare**  
 Per compilare un'istruzione SQL. Viene creato un piano di accesso per la preparazione di un'istruzione SQL.  
  
 **Chiave primaria**  
 Una o più colonne che identifica in modo univoco una riga in una tabella.  
  
 **procedure**  
 Un gruppo di uno o più precompilata di istruzioni SQL che vengono archiviate come un oggetto denominato in un database.  
  
 **colonna di procedure**  
 Un argomento nella chiamata di routine, il valore restituito da una routine o una colonna in un set di risultati creato da una procedura.  
  
## <a name="q"></a>Q  
 **qualifier**  
 Un database che contiene una o più tabelle.  
  
 **query**  
 Un'istruzione SQL. A volte usato per indicare una **seleziona** istruzione.  
  
 **quoted identifier**  
 Un identificatore che è racchiuso tra virgolette identificatore in modo che può contenere caratteri speciali o corrispondere a parole chiave (note anche in SQL-92 come un identificatore delimitato da virgole).  
  
## <a name="r"></a>R  
 **radix**  
 La base di un sistema di numeri. In genere 2 o 10.  
  
 **record**  
 *Vedere* riga.  
  
 **set di risultati**  
 Il set di righe creati tramite l'esecuzione di un **seleziona** istruzione.  
  
 **Codice restituito**  
 Il valore restituito da una funzione ODBC.  
  
 **eseguire il rollback**  
 Per restituire i valori modificati da una transazione allo stato originale.  
  
 **row**  
 Un set di colonne correlate che descrivono un'entità specifica. Noto anche come un *record*.  
  
 **descrittore delle righe**  
 Un descrittore che descrive le colonne di un set di risultati, sia prima di qualsiasi conversione specificata dall'applicazione (un descrittore delle righe di implementazione o IRD) o dopo qualsiasi conversione specificato dall'applicazione (un descrittore riga dell'applicazione o ARD).  
  
 **matrice delle operazioni sulle righe**  
 Matrice contenente i valori che un'applicazione può impostare per indicare che deve essere ignorata la riga corrispondente un **SQLSetPos** operazione.  
  
 **Matrice di stato riga**  
 Matrice che contiene lo stato di una riga dopo una chiamata a **SQLFetch**, **SQLFetchScroll**, o **SQLSetPos**.  
  
 **rowset**  
 Il set di righe restituite in un'unica operazione di recupero da un cursore a blocchi.  
  
 **buffer di righe**  
 I buffer associati alle colonne di un set di risultati in cui vengono restituiti i dati per un intero set di righe.  
  
## <a name="s"></a>S  
 **SAG**  
 *Vedere* gruppo di accesso SQL (SAG).  
  
 **funzione scalare**  
 Una funzione che genera un singolo valore da un singolo valore. Ad esempio, una funzione che modifica il case di dati di tipo carattere.  
  
 **schema**  
 *Vedere* catalogo.  
  
 **con cursori scorrevoli**  
 Un cursore che può spostarsi avanti o indietro tra il set di risultati.  
  
 **serializability**  
 Se due transazioni simultaneamente producono un risultato che è quello utilizzato per l'esecuzione seriale (o sequenziale) di tali transazioni. Le transazioni serializzabili sono tenute a mantenere l'integrità del database.  
  
 **database del server**  
 Un DBMS è progettato per essere eseguito in un ambiente client/server. Questi DBMS fornisce un motore di database autonomo che fornisce supporto avanzato per SQL e le transazioni. Sono accessibili attraverso i driver basati su DBMS. Ad esempio, Oracle, Informix, DB/2 o Microsoft® SQL Server.  
  
 **funzione sui set**  
 *Vedere* funzione di aggregazione.  
  
 **DLL di installazione**  
 *Visualizzare* DLL di installazione driver *e* DLL di installazione di Microsoft translator.  
  
 **driver a un solo livello**  
 *Vedere* driver basati su file.  
  
 **SQL**  
 Structured Query Language. Linguaggio utilizzato dai database relazionali per eseguire una query, aggiornare e gestire i dati.  
  
 **Gruppo di accesso SQL (SAG)**  
 Un consorzio di settore di società in questione con DBMS di SQL. A livello di chiamata interfaccia apertura del gruppo è basato su lavoro svolto originariamente dal gruppo di accesso SQL.  
  
 **Livello di conformità SQL**  
 Il livello di grammatica SQL-92 supportata da un driver; può essere voce, FIPS transitorio, intermedio o Full.  
  
 **Tipo di dati SQL**  
 Il tipo di dati di una colonna o parametro perché viene archiviato nell'origine dati.  
  
 **SQLSTATE**  
 Un valore composto da cinque caratteri che indica un errore specifico.  
  
 **Istruzione SQL**  
 Una frase completa in SQL che inizia con una parola chiave e una descrizione completa un'azione da intraprendere. Ad esempio, selezionare * FROM Orders. Le istruzioni SQL non devono essere confuso con le istruzioni.  
  
 **state**  
 Una condizione ben definita di un elemento. Ad esempio, una connessione ha sette stati, inclusi i dati non allocati, allocati, connessi e tenere sotto controllo. Alcune operazioni possono essere eseguite solo quando un elemento è in uno stato specifico. Ad esempio, una connessione può essere liberata solo quando si trova in uno stato allocato e non, ad esempio, quando è in uno stato di connessione.  
  
 **transizione di stato**  
 Lo spostamento di un elemento da uno stato a altro. ODBC definisce le transizioni di stato rispetto delle rigorose per gli ambienti, connessioni e le istruzioni.  
  
 **istruzione**  
 Un contenitore per tutte le informazioni correlate a un'istruzione SQL. Le istruzioni non va confuso con istruzioni SQL.  
  
 **handle di istruzione**  
 Handle a una struttura di dati che contiene informazioni su un'istruzione.  
  
 **cursore statico**  
 Un cursore scorrevole che non è in grado di rilevare gli aggiornamenti, Elimina o inserisce nel set di risultati. In genere implementato mediante la copia del set di risultati.  
  
 **SQL statico**  
 Un tipo di embedded SQL SQL le istruzioni sono impostate come hardcoded e compilate quando viene compilato il resto del programma. *Vedere anche* istruzioni SQL dinamiche.  
  
 **stored procedure**  
 *Vedere* procedure.  
  
## <a name="t"></a>T  
 **table**  
 Una raccolta di righe.  
  
 **thunking**  
 La conversione di 16 bit punta agli indirizzi a 32 bit o viceversa, quando vengono utilizzate applicazioni a 16 bit con driver ODBC a 32 bit.  
  
 **transaction**  
 Unità atomica di lavoro. Il lavoro in una transazione deve essere completato nel suo complesso; Se qualsiasi parte della transazione non riesce, l'intera transazione ha esito negativo.  
  
 **isolamento delle transazioni**  
 L'atto di isolamento di una transazione dagli effetti di tutte le altre transazioni.  
  
 **Livello di isolamento delle transazioni**  
 Una misura della come una transazione è isolata. Esistono cinque livelli di isolamento delle transazioni: Read Uncommitted, leggere Committed, Repeatable Read, Serializable e il controllo delle versioni.  
  
 **Microsoft Translator DLL**  
 Una DLL utilizzato per convertire i dati da un set di caratteri da un altro.  
  
 **DLL di installazione di Microsoft Translator**  
 Una DLL che contiene funzioni di installazione e configurazione specifiche del convertitore.  
  
 **commit in due fasi**  
 Il processo di commit di una transazione distribuita in due fasi. Nella prima fase, l'elaborazione delle transazioni controlla che tutte le parti della transazione possono essere eseguito il commit. Nella seconda fase, tutte le parti della transazione vengono eseguito il commit. Se qualsiasi parte della transazione indica che non può essere eseguito il commit nella prima fase, la seconda fase non viene eseguito. ODBC non supporta commit a due fasi.  
  
 **Indicatore del tipo**  
 Valore intero passato a o restituito da una funzione ODBC per indicare il tipo di dati di una variabile di applicazione, un parametro o una colonna. ODBC sono definiti gli indicatori di tipo per tipi di dati C sia SQL.  
  
## <a name="v"></a>V  
 **view**  
 Un modo alternativo per visualizzare i dati in una o più tabelle. Una vista in genere viene creata un subset delle colonne da una o più tabelle. In ODBC le visualizzazioni sono generalmente equivalenti alle tabelle.
