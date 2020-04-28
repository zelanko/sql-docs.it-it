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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ac454a8c57fe6e2f12724440dc37c3a1953e4c85
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81302902"
---
# <a name="odbc-glossary"></a>Glossario di ODBC
## <a name="a"></a>Una  
 **piano di accesso**  
 Piano generato dal motore di database per l'esecuzione di un'istruzione SQL. Equivalente al codice eseguibile compilato da un linguaggio di terze generazioni, ad esempio C.  
  
 **funzione di aggregazione**  
 Funzione che genera un singolo valore da un gruppo di valori, spesso utilizzato con clausole **Group by** e **having** . Le funzioni di aggregazione includono **AVG**, **count**, **Max**, **min**e **Sum**. Note anche come *funzioni set*. *Vedere anche* funzione scalare.  
  
 **ANSI**  
 American National Standards Institute. L'API ODBC è basata sull'interfaccia ANSI a livello di chiamata.  
  
 **APD**  
 *Vedere* descrittore del parametro dell'applicazione (APD).  
  
 **API**  
 Interfaccia di programmazione dell'applicazione. Set di routine utilizzato da un'applicazione per richiedere e svolgere servizi di livello inferiore. L'API ODBC è costituita dalle funzioni ODBC.  
  
 **applicazione**  
 Programma eseguibile che chiama funzioni nell'API ODBC.  
  
 **descrittore del parametro dell'applicazione (APD)**  
 Descrittore che descrive i parametri dinamici utilizzati in un'istruzione SQL prima di qualsiasi conversione specificata dall'applicazione.  
  
 **descrittore di riga dell'applicazione (ARD)**  
 Descrittore che rappresenta i metadati e i dati delle colonne nei buffer dell'applicazione, che descrivono una riga di dati dopo la conversione dei dati specificata dall'applicazione.  
  
 **ARD**  
 *Vedere* Application Row Descriptor (ARD).  
  
 **modalità autocommit**  
 Modalità di commit delle transazioni in cui viene eseguito il commit delle transazioni immediatamente dopo l'esecuzione.  
  
## <a name="b"></a>b  
 **modifica del comportamento**  
 Una modifica apportata a determinate funzionalità dal comportamento ODBC *3. x* al comportamento ODBC *2. x* o viceversa. Causata dalla modifica dell'attributo dell'ambiente SQL_ATTR_ODBC_VERSION.  
  
 **Oggetto binario di grandi dimensioni (BLOB)**  
 Qualsiasi dato binario per un determinato numero di byte, ad esempio 255. In genere, molto più a lungo. Tali dati vengono in genere inviati e recuperati dall'origine dati in parti. Noto anche come *Long Data*.  
  
 **associazione**  
 Come verbo, l'operazione di associazione di una colonna in un set di risultati o di un parametro in un'istruzione SQL con una variabile di applicazione. Come sostantivo, l'associazione.  
  
 **offset binding**  
 Valore aggiunto agli indirizzi del buffer dei dati e agli indirizzi di lunghezza/indicatore del buffer per tutti i dati della colonna o del parametro associati, che producono nuovi indirizzi.  
  
 **cursore rettangolare**  
 Cursore in grado di recuperare più di una riga di dati alla volta.  
  
 **buffer**  
 Una porzione di memoria dell'applicazione usata per passare i dati tra l'applicazione e il driver. I buffer spesso sono coppie: un buffer di *dati* e un *buffer di lunghezza dei dati*.  
  
 **byte**  
 Otto bit o un ottetto. *Vedere anche* ottetto.  
  
## <a name="c"></a>C  
 **Tipo di dati C**  
 Tipo di dati di una variabile in un programma C, in questo caso l'applicazione.  
  
 **Catalogo**  
 Set di tabelle di sistema in un database che descrivono la forma del database. Noto anche come *schema* o *dizionario dei dati*.  
  
 **funzione Catalog**  
 Funzione ODBC utilizzata per recuperare le informazioni dal catalogo del database.  
  
 **CLI**  
 *Vedere* API.  
  
 **client/server**  
 Strategia di accesso al database in cui uno o più client accedono ai dati tramite un server. I client di solito implementano l'interfaccia utente mentre il server controlla l'accesso al database.  
  
 **colonna**  
 Contenitore per un singolo elemento di informazioni in una riga. Noto anche come *campo*.  
  
 **commit**  
 Per rendere permanenti le modifiche in una transazione.  
  
 **concorrenza**  
 Possibilità di più di una transazione di accedere contemporaneamente agli stessi dati.  
  
 **livello di conformità**  
 Set discreto di funzionalità supportate da un driver o da un'origine dati. ODBC definisce i livelli di conformità API e i livelli di conformità SQL.  
  
 **connection**  
 Una particolare istanza di un driver e di un'origine dati.  
  
 **esplorazione della connessione**  
 Ricerca nelle origini dati della rete a cui connettersi. L'esplorazione della connessione può implicare diversi passaggi. È ad esempio possibile che l'utente esplori la rete per individuare i server e quindi esplori un particolare server per un database.  
  
 **handle di connessione**  
 Handle per una struttura di dati che contiene informazioni su una connessione.  
  
 **riga corrente**  
 Riga a cui fa attualmente riferimento il cursore. Le operazioni posizionate agiscono sulla riga corrente.  
  
 **cursor**  
 Componente software che restituisce righe di dati all'applicazione. Probabilmente chiamato dopo il cursore lampeggiante su un terminale del computer; così come il cursore indica la posizione corrente sullo schermo, un cursore in un set di risultati indica la posizione corrente nel set di risultati.  
  
## <a name="d"></a>D  
 **buffer dei dati**  
 Buffer utilizzato per passare i dati. Spesso associato a un buffer di dati è un *buffer di lunghezza dei dati*.  
  
 **dizionario dei dati**  
 *Vedere* Catalog.  
  
 **buffer lunghezza dati**  
 Buffer utilizzato per passare la lunghezza del valore in un *buffer di dati*corrispondente. Il buffer per la lunghezza dei dati viene utilizzato anche per archiviare indicatori, ad esempio se il valore dei dati è con terminazione null.  
  
 **origine dati**  
 I dati a cui l'utente desidera accedere e il sistema operativo, DBMS e la piattaforma di rete associati (se presenti).  
  
 **tipo di dati**  
 Tipo di una porzione di dati. ODBC definisce i tipi di dati C e SQL. *Vedere anche* indicatore di tipo.  
  
 **colonna data-at-execution**  
 Colonna per la quale vengono inviati i dati dopo la chiamata a **SQLSetPos** . Con il nome, perché i dati vengono inviati in fase di esecuzione anziché essere inseriti in un buffer del set di righe. I dati Long vengono in genere inviati in parti in fase di esecuzione.  
  
 **parametro data-at-execution**  
 Parametro per il quale vengono inviati i dati dopo la chiamata a **SQLExecute** o **SQLExecDirect** . Il nome viene così denominato perché i dati vengono inviati quando l'istruzione SQL viene eseguita anziché essere inserita in un buffer di parametri. I dati Long vengono in genere inviati in parti in fase di esecuzione.  
  
 **database**  
 Raccolta discreta di dati in un sistema DBMS. Anche un sistema DBMS.  
  
 **motore di database**  
 Il software in un sistema DBMS che analizza ed esegue istruzioni SQL e accede ai dati fisici.  
  
 **DBMS**  
 Sistema di gestione di database. Livello del software tra il database fisico e l'utente. Il sistema DBMS gestisce tutte le operazioni di accesso al database.  
  
 **Driver basato su DBMS**  
 Driver che accede ai dati fisici tramite un motore di database autonomo.  
  
 **DDL**  
 Linguaggio di definizione dei dati. Tali istruzioni in SQL che definiscono, anziché modificare, i dati. Ad esempio, **Create Table**, **create index**, **Grant**e **Revoke**.  
  
 **identificatore delimitato**  
 Identificatore racchiuso tra virgolette, in modo che possa contenere caratteri speciali o parole chiave di corrispondenza (noto anche come identificatore tra virgolette).  
  
 **descrittore**  
 Struttura di dati che include informazioni sui parametri dinamici o sui dati della colonna. La rappresentazione fisica del descrittore non è definita. le applicazioni ottengono l'accesso diretto a un descrittore solo modificando i campi chiamando le funzioni ODBC con l'handle del descrittore.  
  
 **database desktop**  
 DBMS progettato per essere eseguito in un personal computer. In genere, questi DBMS non forniscono un motore di database autonomo ed è necessario accedervi tramite un driver basato su file. In genere i motori di questi driver hanno ridotto il supporto per SQL e le transazioni. Ad esempio, dBASE, Paradox, Btrieve o Microsoft® FoxPro®.  
  
 **diagnostica**  
 Record contenente le informazioni di diagnostica sull'ultima funzione chiamata che ha utilizzato un handle specifico. I record di diagnostica sono associati a handle di ambiente, connessione, istruzione e descrittore.  
  
 **DML**  
 Linguaggio di manipolazione dei dati. Queste istruzioni in SQL che manipolano, anziché definire, i dati. Ad esempio, **Insert**, **Update**, **Delete**e **Select**.  
  
 **driver**  
 Libreria di routine che espone le funzioni nell'API ODBC. I driver sono specifici di un singolo sistema DBMS.  
  
 **Gestione driver**  
 Libreria di routine che gestisce l'accesso ai driver per l'applicazione. Gestione driver carica e Scarica (oppure si connette e disconnette) i driver e passa le chiamate alle funzioni ODBC al driver corretto.  
  
 **DLL di installazione driver**  
 Una DLL che contiene funzioni di installazione e configurazione specifiche del driver.  
  
 **cursore dinamico**  
 Cursore scorrevole in grado di rilevare le righe aggiornate, eliminate o inserite nel set di risultati.  
  
 **SQL dinamico**  
 Tipo di SQL incorporato in cui le istruzioni SQL vengono create e compilate in fase di esecuzione. *Vedere anche* SQL statico.  
  
## <a name="e"></a>E  
 **SQL incorporato**  
 Le istruzioni SQL incluse direttamente in un programma scritto in un altro linguaggio, ad esempio COBOL o C. ODBC, non utilizzano SQL embedded. *Vedere anche* SQL statico *e* SQL dinamico.  
  
 **ambiente**  
 Contesto globale in cui accedere ai dati. associato all'ambiente sono presenti informazioni globali, ad esempio un elenco di tutte le connessioni in tale ambiente.  
  
 **handle di ambiente**  
 Handle per una struttura di dati che contiene informazioni sull'ambiente.  
  
 **clausola escape**  
 Clausola in un'istruzione SQL.  
  
 **eseguire**  
 Per eseguire un'istruzione SQL.  
  
## <a name="f"></a>F  
 **cursore Fat**  
 *Vedere* cursore a blocchi.  
  
 **prendere**  
 Per recuperare una o più righe da un set di risultati.  
  
 **campo**  
 *Vedere* Column.  
  
 **driver basato su file**  
 Driver che accede direttamente ai dati fisici. In questo caso, il driver contiene un motore di database e funge da driver e origine dati.  
  
 **origine dati file**  
 Origine dati per la quale le informazioni di connessione vengono archiviate in un file con estensione DSN.  
  
 **chiave esterna**  
 Una o più colonne di una tabella che corrispondono alla chiave primaria in un'altra tabella.  
  
 **cursore di sola trasmissione**  
 Cursore che può essere spostato in avanti solo attraverso il set di risultati e in genere recupera solo una riga alla volta. La maggior parte dei database relazionali supporta solo i cursori di sola trasmissione.  
  
## <a name="h"></a>H  
 **gestire**  
 Valore che identifica in modo univoco un elemento, ad esempio un file o una struttura di dati. Gli handle sono significativi solo per il software che li crea e li utilizza, ma vengono passati da un altro software per identificare gli elementi. ODBC definisce gli handle per gli ambienti, le connessioni, le istruzioni e i descrittori.  
  
## <a name="i"></a>I  
 **descrittore parametri di implementazione (dpi)**  
 Descrittore che descrive i parametri dinamici utilizzati in un'istruzione SQL dopo qualsiasi conversione specificata dall'applicazione.  
  
 **descrittore della riga di implementazione (IRD)**  
 Descrittore che descrive una riga di dati prima di qualsiasi conversione specificata dall'applicazione.  
  
 **DLL del programma di installazione**  
 DLL che consente di installare i componenti ODBC e di configurare le origini dati.  
  
 **Funzionalità di miglioramento dell'integrità**  
 Subset di SQL progettato per mantenere l'integrità di un database.  
  
 **livello di conformità dell'interfaccia**  
 Livello dell'interfaccia ODBC 3,7 supportata da un driver; può essere core, Level 1 o Level 2.  
  
 **interoperabilità**  
 Capacità di un'applicazione di utilizzare lo stesso codice quando si accede ai dati in DBMS diversi.  
  
 **IPD**  
 *Vedere* Descrittore del parametro di implementazione (dpi).  
  
 **IRD**  
 *Vedere* Descrittore della riga di implementazione (IRD).  
  
 **ISO/IEC**  
 International Standards Organization/International Electrotechnical Commission. L'API ODBC è basata sull'interfaccia a livello di chiamata ISO/IEC.  
  
## <a name="j"></a>J  
 **Join**  
 Operazione in un database relazionale che collega le righe in due o più tabelle in base ai valori corrispondenti nelle colonne specificate.  
  
## <a name="k"></a>K  
 **key**  
 Colonna o colonne i cui valori identificano una riga. *Vedere anche* chiave esterna *e* chiave primaria.  
  
 **keyset**  
 Set di chiavi utilizzate da un cursore misto o gestito da keyset per recuperare le righe.  
  
 **cursore gestito da keyset**  
 Cursore scorrevole che rileva le righe aggiornate ed eliminate tramite un keyset.  
  
## <a name="l"></a>L  
 **valore letterale**  
 Rappresentazione in forma di caratteri di un valore di dati effettivo in un'istruzione SQL.  
  
 **blocco**  
 Processo mediante il quale un sistema DBMS limita l'accesso a una riga in un ambiente multiutente. In genere, il sistema DBMS imposta un bit in una riga o nella pagina fisica contenente una riga che indica che la riga o la pagina è bloccata.  
  
 **dati lunghi**  
 Dati binari o di tipo carattere su una determinata lunghezza, ad esempio 255 byte o caratteri. In genere, molto più a lungo. Tali dati vengono in genere inviati e recuperati dall'origine dati in parti. Noto anche come *BLOB*s o *CLOB*.  
  
## <a name="m"></a>M  
 **origine dati computer**  
 Origine dati per la quale vengono archiviate le informazioni di connessione nel sistema, ad esempio il registro di sistema.  
  
 **modalità di commit manuale**  
 Modalità di commit delle transazioni in cui è necessario eseguire il commit esplicito delle transazioni chiamando **SQLTransact**.  
  
 **metadati**  
 Dati che descrivono un parametro in un'istruzione SQL o in una colonna di un set di risultati. Ad esempio, il tipo di dati, la lunghezza in byte e la precisione di un parametro.  
  
 **driver a più livelli**  
 *Vedere* Driver basato su DBMS.  
  
## <a name="n"></a>N  
 **Valore NULL**  
 Nessun valore assegnato in modo esplicito. In particolare, un valore NULL è diverso da zero o da uno spazio vuoto.  
  
## <a name="o"></a>O  
 **ottetto**  
 Otto bit o un byte. *Vedere anche* byte.  
  
 **lunghezza ottetto**  
 Lunghezza in ottetti di un buffer o dei dati in esso contenuti.  
  
 **ODBC**  
 Open Database Connectivity. Specifica per un'API che definisce un set standard di routine a cui un'applicazione può accedere ai dati in un'origine dati.  
  
 **Amministratore ODBC**  
 Programma eseguibile che chiama la DLL del programma di installazione per configurare le origini dati.  
  
 Apri gruppo  
 Società che pubblica gli standard. In particolare, pubblica gli standard del gruppo di accesso SQL (SAG).  
  
 **concorrenza ottimistica**  
 Strategia per aumentare la concorrenza in cui le righe non sono bloccate. Al contrario, prima che vengano aggiornati o eliminati, un cursore verifica se sono stati modificati dall'ultima lettura. In tal caso, l'aggiornamento o l'eliminazione non riesce. *Vedere anche* la concorrenza pessimistica.  
  
 **join esterno**  
 Join in cui vengono restituite sia le righe corrispondenti che quelle non corrispondenti. I valori di tutte le colonne della tabella senza corrispondenza in righe non corrispondenti vengono impostati su NULL.  
  
 **proprietario**  
 Proprietario di una tabella.  
  
## <a name="p"></a>P  
 **parametro**  
 Variabile in un'istruzione SQL, contrassegnata con un marcatore di parametro o un punto interrogativo (?). I parametri sono associati alle variabili dell'applicazione e ai relativi valori recuperati quando viene eseguita l'istruzione.  
  
 **descrittore di parametro**  
 Descrittore che descrive i parametri della fase di esecuzione utilizzati in un'istruzione SQL, prima di qualsiasi conversione specificata dall'applicazione (un descrittore di parametri dell'applicazione o APD) o dopo una conversione specificata dall'applicazione (un descrittore di parametri di implementazione o un dpi).  
  
 **Array operazione parametro**  
 Matrice contenente i valori che un'applicazione può impostare per indicare che il parametro corrispondente deve essere ignorato in un'operazione **SQLExecDirect** o **SQLExecute** .  
  
 **matrice di stato del parametro**  
 Matrice contenente lo stato di un parametro dopo una chiamata a **SQLExecDirect** o **SQLExecute**.  
  
 **concorrenza pessimistica**  
 Strategia per l'implementazione della serializzabilità, in cui le righe sono bloccate in modo che non possano essere modificate da altre transazioni. *Vedere anche* concorrenza ottimistica *e* serializzabilità.  
  
 **operazione posizionata**  
 Qualsiasi operazione che agisce sulla riga corrente. Ad esempio, le istruzioni Update e Delete posizionate, **SQLGetData**e **SQLSetPos**.  
  
 **istruzione UPDATE posizionata**  
 Istruzione SQL utilizzata per aggiornare i valori nella riga corrente.  
  
 **istruzione DELETE posizionata**  
 Istruzione SQL utilizzata per eliminare la riga corrente.  
  
 **preparare**  
 Per compilare un'istruzione SQL. Un piano di accesso viene creato preparando un'istruzione SQL.  
  
 **chiave primaria**  
 Colonna o colonne che identifica in modo univoco una riga in una tabella.  
  
 **procedura**  
 Gruppo di una o più istruzioni SQL precompilate archiviate come oggetto denominato in un database.  
  
 **colonna procedure**  
 Un argomento in una chiamata di routine, il valore restituito da una routine o una colonna in un set di risultati creato da una procedura.  
  
## <a name="q"></a>Q  
 **qualificatore**  
 Un database che contiene una o più tabelle.  
  
 **query**  
 Istruzione SQL. Viene talvolta usato per indicare un'istruzione **Select** .  
  
 **quoted identifier**  
 Identificatore racchiuso tra virgolette per gli identificatori, in modo che possa contenere caratteri speciali o parole chiave corrispondenti (noto anche come identificatore delimitato di SQL-92).  
  
## <a name="r"></a>R  
 **radice**  
 Base di un sistema di numeri. In genere 2 o 10.  
  
 **record**  
 *Vedere* la riga.  
  
 **set di risultati**  
 Set di righe creato mediante l'esecuzione di un'istruzione **Select** .  
  
 **codice restituito**  
 Valore restituito da una funzione ODBC.  
  
 **rollback**  
 Per restituire i valori modificati da una transazione allo stato originale.  
  
 **riga**  
 Set di colonne correlate che descrivono un'entità specifica. Noto anche come *record*.  
  
 **descrittore di riga**  
 Descrittore che descrive le colonne di un set di risultati, prima di qualsiasi conversione specificata dall'applicazione (un descrittore della riga di implementazione o IRD) o dopo qualsiasi conversione specificata dall'applicazione (un descrittore di riga dell'applicazione o ARD).  
  
 **Array operazione riga**  
 Matrice contenente i valori che un'applicazione può impostare per indicare che la riga corrispondente deve essere ignorata in un'operazione **SQLSetPos** .  
  
 **matrice stato riga**  
 Matrice contenente lo stato di una riga dopo una chiamata a **SQLFetch**, **SQLFetchScroll**o **SQLSetPos**.  
  
 **righe**  
 Set di righe restituite in una singola operazione di recupero mediante un cursore a blocchi.  
  
 **buffer dei set di righe**  
 Buffer associati alle colonne di un set di risultati e in cui vengono restituiti i dati per un intero set di righe.  
  
## <a name="s"></a>S  
 **SAG**  
 *Vedere* Gruppo di accesso SQL (SAG).  
  
 **funzione scalare**  
 Funzione che genera un singolo valore da un singolo valore. Ad esempio, una funzione che modifica la combinazione di maiuscole e minuscole dei dati di tipo carattere.  
  
 **Schema**  
 *Vedere* Catalog.  
  
 **cursore scorrevole**  
 Cursore che può spostarsi avanti o indietro nel set di risultati.  
  
 **serializzabilità**  
 Se due transazioni eseguite simultaneamente producono un risultato uguale all'esecuzione seriale (o sequenziale) di tali transazioni. Le transazioni serializzabili sono necessarie per mantenere l'integrità del database.  
  
 **database del server**  
 DBMS progettato per essere eseguito in un ambiente client/server. Questi DBMS forniscono un motore di database autonomo che offre supporto avanzato per SQL e transazioni. È possibile accedervi tramite driver basati su DBMS. Ad esempio, Oracle, Informix, DB/2 o Microsoft® SQL Server.  
  
 **funzione set**  
 *Vedere* funzione di aggregazione.  
  
 **DLL di installazione**  
 *Vedere* la dll di installazione del driver e la dll *di installazione di* Translator.  
  
 **driver a livello singolo**  
 *Vedere* driver basato su file.  
  
 **SQL**  
 Structured Query Language. Linguaggio utilizzato dai database relazionali per eseguire query, aggiornare e gestire i dati.  
  
 **Gruppo di accesso SQL (SAG)**  
 Un consorzio di settore di aziende che interessano i sistemi DBMS SQL. L'interfaccia a livello di chiamata del gruppo aperto è basata sul lavoro eseguito originariamente dal gruppo di accesso SQL.  
  
 **Livello di conformità SQL**  
 Livello della grammatica SQL-92 supportato da un driver; può essere entry, FIPS transitive, Intermediate o full.  
  
 **Tipo di dati SQL**  
 Tipo di dati di una colonna o di un parametro archiviato nell'origine dati.  
  
 **SQLSTATE**  
 Valore di cinque caratteri che indica un errore specifico.  
  
 **Istruzione SQL**  
 Frase completa in SQL che inizia con una parola chiave e descrive completamente un'azione da intraprendere. Ad esempio, selezionare * da Orders. Le istruzioni SQL non devono essere confuse con le istruzioni.  
  
 **state**  
 Condizione ben definita di un elemento. Ad esempio, una connessione ha sette Stati, inclusi i dati non allocati, allocati, connessi e necessari. Alcune operazioni possono essere eseguite solo quando un elemento si trova in un determinato stato. Ad esempio, una connessione può essere liberata solo quando si trova in uno stato allocato e non, ad esempio, quando è in uno stato connesso.  
  
 **transizione di stato**  
 Spostamento di un elemento da uno stato a un altro. ODBC definisce le transizioni di stato rigorose per ambienti, connessioni e istruzioni.  
  
 **istruzione**  
 Contenitore per tutte le informazioni correlate a un'istruzione SQL. Le istruzioni non devono essere confuse con le istruzioni SQL.  
  
 **handle di istruzione**  
 Handle per una struttura di dati che contiene informazioni su un'istruzione.  
  
 **cursore statico**  
 Cursore scorrevole che non è in grado di rilevare aggiornamenti, eliminazioni o inserimenti nel set di risultati. Viene in genere implementato eseguendo una copia del set di risultati.  
  
 **SQL statico**  
 Tipo di SQL incorporato in cui le istruzioni SQL sono hardcoded e compilate quando viene compilato il resto del programma. *Vedere anche* SQL dinamico.  
  
 **stored procedure**  
 *Vedere* la procedura.  
  
## <a name="t"></a>T  
 **tabella**  
 Raccolta di righe.  
  
 **thunking**  
 La conversione di indirizzi a 16 bit in indirizzi a 32 bit o viceversa, quando le applicazioni a 16 bit vengono utilizzate con driver ODBC a 32 bit.  
  
 **transazione**  
 Unità di lavoro atomica. Il lavoro in una transazione deve essere completato nel suo complesso. Se qualsiasi parte della transazione non riesce, l'intera transazione avrà esito negativo.  
  
 **isolamento delle transazioni**  
 Operazione di isolamento di una transazione dagli effetti di tutte le altre transazioni.  
  
 **livello di isolamento delle transazioni**  
 Misura della modalità di isolamento di una transazione. Sono disponibili cinque livelli di isolamento delle transazioni: Read uncommitted, Read Committed, Repeatable Read, Serializable e Versioning.  
  
 **DLL di traduzione**  
 DLL utilizzata per convertire i dati da un set di caratteri a un altro.  
  
 **DLL di installazione di Translator**  
 Una DLL che contiene funzioni di installazione e configurazione specifiche del traduttore.  
  
 **commit in due fasi**  
 Processo di commit di una transazione distribuita in due fasi. Nella prima fase, il processore di transazioni controlla che sia possibile eseguire il commit di tutte le parti della transazione. Nella seconda fase viene eseguito il commit di tutte le parti della transazione. Se una parte della transazione indica nella prima fase che non è possibile eseguire il commit, la seconda fase non si verifica. ODBC non supporta i commit a due fasi.  
  
 **indicatore di tipo**  
 Valore integer passato o restituito da una funzione ODBC per indicare il tipo di dati di una variabile di applicazione, un parametro o una colonna. ODBC definisce gli indicatori di tipo per i tipi di dati C e SQL.  
  
## <a name="v"></a>V  
 **visualizzare**  
 Modo alternativo per esaminare i dati in una o più tabelle. Una vista viene in genere creata come subset delle colonne di una o più tabelle. In ODBC le visualizzazioni sono generalmente equivalenti alle tabelle.
