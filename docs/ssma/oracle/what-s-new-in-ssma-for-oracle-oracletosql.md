---
title: Novità di SSMA per Oracle (OracleToSQL) Documenti Microsoft
authors: HJToland3;nahk-ivanov
ms.prod: sql
ms.custom: ''
ms.date: 4/2/2020
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: f305ebb6-7393-4a43-abb3-6332b739d690
ms.author: jtoland;alexiva
ms.openlocfilehash: 88b87aad931f28637accc95aa4d993037fcf0b0a
ms.sourcegitcommit: d818a307725983c921987749915fe1a381233d98
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/03/2020
ms.locfileid: "80625605"
---
# <a name="whats-new-in-ssma-for-oracle-oracletosql"></a>Novità di SSMA per Oracle (OracleToSQL)

In questo articolo vengono elencate le modifiche di SQL Server Sql Server Migration Assistant (SSMA) per Oracle in ogni versione.

## <a name="ssma-v88"></a>SSMA v8.8

La versione v8.8 di SSMA per Oracle include:

* Miglioramenti alla stabilità della sincronizzazione degli oggetti di SQL ServerSQL Server objects synchronization stability improvements
* Miglioramenti delle prestazioni dell'interfaccia grafica durante la valutazione e la conversione
* Migliore conversione `OVER PARTITION` delle clausole analitiche
* Nuova conversione per `LEAD` la funzione analitica
* Nuova conversione per le clausole di factoring di sottoquery
* Nuova `REPLICATE` opzione di distribuzione per Azure SQL Data Warehouse
* Nuovo parser di sintassi Oracle per migliorare ulteriormente le prestazioni di conversione

## <a name="ssma-v87"></a>SSMA v8.7

La versione v8.7 di SSMA per Oracle ha correzioni minori e miglioramenti delle prestazioni nell'interfaccia utente grafica.

Inoltre, SSMA per Oracle consente ora di filtrare gli oggetti in base allo stato di validità nella finestra di dialogo 'Selezione avanzata oggetti'.

> [!IMPORTANT]
> Con SSMA v8.5 e versioni successive, .NET 4.7.2 è un prerequisito per l'installazione. Se è necessario installare questa versione, è possibile scaricare il file di runtime da [qui](https://dotnet.microsoft.com/download/dotnet-framework/net472).

## <a name="ssma-v86"></a>SSMA v8.6

Oltre a un set mirato di correzioni progettate per migliorare l'usabilità e le prestazioni, la versione v8.6 di SSMA per Oracle è stata migliorata aggiungendo un'impostazione che consente agli utenti di omettere le proprietà estese SSMA nel codice convertito.

Per utilizzare questa impostazione, in SSMA per Oracle passare a **Strumenti** > **Impostazioni** > di progetto**Conversione****generale** > , quindi in **Varie**aggiornare il valore dell'impostazione **Omettere proprietà estese** su **Sì**.

![Omettere l'impostazione delle proprietà estese](../oracle/media/ssma-omit-extended-properties.png)

Inoltre, SSMA per Oracle ora fornisce una `XMLTABLE` migliore analisi della clausola.

> [!IMPORTANT]
> Con SSMA v8.5 e versioni successive, .NET 4.7.2 è un prerequisito per l'installazione. Se è necessario installare questa versione, è possibile scaricare il file di runtime da [qui](https://dotnet.microsoft.com/download/dotnet-framework/net472).

## <a name="ssma-v85"></a>SSMA v8.5

La versione v8.5 di SSMA per Oracle è stata migliorata con il supporto per l'autenticazione di Azure Active Directory e il supporto di base per le funzionalità JSON nel server SQL, insieme a un set mirato di correzioni progettate per migliorare l'usabilità e le prestazioni.

Inoltre, SSMA per Oracle è stato migliorato con il supporto per:In addition, SSMA for Oracle has been enhanced with support for:

* Limitare il numero di oggetti selezionati per l'individuazione a 990 (il limite della clausola di `WHERE .. IN (..)` Oracle è 1000 elementi).
* Migrazione dei `RAW` `UNIQUEIDENTIFIER`dati da a .
* Analisi della `PARALLEL_ENABLE` clausola.

Infine, la versione v8.5 di SSMA per Oracle ora fornisce:

* Miglioramento delle prestazioni delle costanti in pacchetto convertite.
* Un aggiornamento per il provider di dati Oracle per .NET alla versione 19.5.0.An update for Oracle Data Provider for .NET to version 19.5.0.

> [!IMPORTANT]
> Con SSMA v8.5, .NET 4.7.2 è un prerequisito per l'installazione. Se è necessario installare questa versione, è possibile scaricare il file di runtime da [qui](https://dotnet.microsoft.com/download/dotnet-framework/net472).

## <a name="ssma-v84"></a>SSMA v8.4

La versione v8.4 di SSMA per Oracle è stata migliorata con correzioni mirate progettate per risolvere i problemi di accessibilità e correggere un bug relativo alle colonne di indice max (per consentire 32 anziché 16) per SQL Server 2016 e versioni successive.

Inoltre, questa versione di SSMA per `SYS_REFCURSOR` Oracle `OUT` aggiunge la conversione per come parametri di stored procedure.

> [!IMPORTANT]
> Con le versioni SSMA da 7.4 a 8.4, .NET 4.5.2 è un prerequisito per l'installazione.

## <a name="ssma-v83"></a>SSMA v8.3

La versione v8.3 di SSMA per Oracle è stata migliorata con correzioni mirate progettate per migliorare la qualità e le metriche di conversione. Inoltre, questa versione di SSMA per Oracle fornisce correzioni che:In addition, this release of SSMA for Oracle provides fixes that:

* Risolvere i problemi di accessibilità.
* Aggiungere il `hierarchyid` supporto di base per il tipo in SQL Server.Add basic support for type in SQL Server.
* Risolvere un problema con un tipo restituito sconosciuto per una funzione chiamata tramite sinonimo.
* Aggiornare ODP.NET alla versione 19.3.

## <a name="ssma-v82"></a>SSMA v8.2

La versione v8.2 di SSMA per Oracle è stata migliorata per:

* Aggiungere il `DBMS_OUTPUT.ENABLE` / `DISABLE`supporto per .
* Rimuovere `CAST AS FLOAT` `BINARY_FLOAT` per `BINARY_DOUBLE` e colonne nella query di migrazione dei dati predefinita.
* Correggere l'aggiornamento delle sequenze se il valore corrente è stato modificato.
* Correggere il bug relativo all'errata`ROWNUM`interpretazione delle pseudo-colonne ( , e così via) se esiste una colonna con lo stesso nome.
* Correggere un arresto anomalo `FOR` che si verifica la conversione di cicli con identificatore ambiguo non risolto.

Inoltre, questa versione include un set mirato di correzioni progettate per migliorare la qualità e le metriche di conversione, nonché correzioni per:

* Problema con gli indici non cluster disabilitati dopo la migrazione dei dati.
* Rilevamento di .NET Framework durante l'installazione invisibile all'utente.
* Arresto anomalo intermittente che si verifica quando viene scaricata una nuova versione.

> [!NOTE]
> Un problema noto con l'aggiornamento automatico può causare l'errore di un aggiornamento da SSMA v8.1 a v8.2. Se si verifica questo errore, scaricare la nuova versione e installarla manualmente.

## <a name="ssma-v81"></a>SSMA v8.1

La versione v8.1 di SSMA per Oracle è stata migliorata con correzioni mirate progettate per migliorare la qualità e le metriche di conversione.

> [!NOTE]
> Un problema noto con l'aggiornamento automatico può causare l'errore di un aggiornamento da SSMA v8.0 a v8.1. Se si verifica questo errore, scaricare la nuova versione e installarla manualmente.

## <a name="ssma-v80"></a>SSMA v8.0

La versione v8.0 di SSMA per Oracle è stata migliorata con correzioni mirate progettate per migliorare la qualità e le metriche di conversione. Questa versione offre anche le seguenti nuove funzionalità:

* Supporto per **l'istanza gestita del database SQL** di Azure come destinazione. È ora possibile creare nuovi progetti destinati all'istanza gestita del database SQL di Azure:You can now create new projects targeting Azure SQL Database Managed Instance:

  ![Progetto SQL DB MI](../media/ssma-newproject-sqldbmi.png)

  > [!NOTE]
  > È stato aggiornato anche SSMA per Oracle Extension Pack per consentire le installazioni remote nell'istanza gestita del database SQL di Azure:The SSMA for Oracle Extension Pack was also updated to allow remote installations on Azure SQL Database Managed Instance:
  >
  > ![SSMA per Oracle Extension Pack](../media/ssma-oracle-ext-pack.png)

  Alcune funzionalità, tra cui Tester e la migrazione dei dati sul lato server, non sono supportate quando si ha come destinazione l'istanza gestita del database SQL di Azure.Some features, including Tester and Server-side data migration, are not supported when targeting Azure SQL Database Managed Instance. Per altre informazioni, leggere [qui](https://blogs.msdn.microsoft.com/datamigration/2019/02/17/migrate-your-oracle-database-to-azure-sql-database-managed-instance-using-ssma-8-0/).

* Avviso **fix**post-conversione . Scopri di più [qui](https://blogs.msdn.microsoft.com/datamigration/2019/02/17/%20accelerate-your-oracle-migrations-with-new-machine-learning-capabilities-in-ssma/).

* Selezione preliminare di database/schema.

  Quando ci si connette all'origine, l'utente può ora selezionare database/schemi di interesse. Selezionando solo gli schemi che si prevede di eseguire la migrazione si risparmia tempo durante la connessione iniziale e migliorare le prestazioni complessive SSMA.

  ![Oggetti filtro SSMASSMA filter objects](../media/ssma-filter-objects.png)

* La possibilità di utilizzare il driver .NET ufficiale e gestito per connettersi a Oracle. Il driver OCI non è più un prerequisito per l'utilizzo di Assistente migrazione SQL Server per Oracle.

* La possibilità `ROWID` di `UROWID` `VARCHAR` mappare e per impostazione predefinita. Modificato `uniqueidentifier` da per consentire `ROWID` la migrazione dei dati per le colonne esplicite.

## <a name="ssma-v710"></a>SSMA v7.10

La versione v7.10 di SSMA per Oracle contiene le seguenti modifiche:

* Correzioni mirate progettate per fornire ulteriori protezioni di sicurezza e privacy per soddisfare i cambiamenti nei requisiti globali.
* Miglioramento della conversione relativo a query gerarchiche.

## <a name="ssma-v79"></a>SSMA v7.9

La versione v7.9 di SSMA per Oracle contiene le seguenti modifiche:

* Correzioni mirate che migliorano la qualità e le metriche di conversione.
* Supporto per la migrazione di istruzioni "Continue" da Oracle a SQL Server.Support for migrating "Continue" statements from Oracle to SQL Server.
* Supporto nella riga di comando SSMA per modificare il mapping dei tipi di dati e le preferenze di progetto.
* Supporto per la migrazione dei dati tramite SQL Server Integration Services (SSIS). Dopo aver convertito lo schema, è possibile creare un pacchetto SSIS utilizzando un'opzione del menu di scelta rapida.
* Anche la finestra di dialogo di connessione al database SQL di Azure in SSMA è stata modificata per specificare il nome completo del server. Nelle versioni precedenti di SSMA, il prefisso del database SQL di Azure doveva essere menzionato in modo esplicito all'interno delle impostazioni dei progetti.

## <a name="ssma-v78"></a>SSMA v7.8

La versione v7.8 di SSMA per Oracle contiene le seguenti modifiche:

* Supporto per:
  * Espressione di `IN` riga per la clausola.
  * Cast di tipo implicito.
  * `UID`conversione per il database SQL di Azure.Conversion for Azure SQL Database.
* Modifica del mapping dei tipi evidenziato in **Impostazioni progetto**.
* Possibilità per gli utenti di disabilitare i dati di telemetria.

## <a name="ssma-v77"></a>SSMA v7.7

La versione v7.7 di SSMA per Oracle contiene le seguenti modifiche:

* SSMA per Oracle è stato migliorato con correzioni mirate che migliorano la qualità e le metriche di conversione.
* In base alla richiesta popolare, la versione a 32 bit di SSMA per Oracle è tornato. Rispetto all'implementazione precedente (prima della v7.4), esistono due pacchetti di installazione, ma non possono essere installati affiancati. Di conseguenza, è necessario scegliere la versione più appropriata in base ai componenti di connettività disponibili. È sempre preferibile utilizzare la versione a 64 bit, se possibile.
* Il supporto di SQL Server 2017 è ora ufficiale con l'Oracle Extension Pack supportato anche su Linux (nuova opzione di installazione remota). Si noti che la funzionalità di Extension Pack è limitata se installata su Linux, poiché le funzionalità di migrazione dei dati lato server e tester non sono supportate.
* SSMA per Oracle consente di eseguire la migrazione delle viste materializzate come tabelle normali (configurabili tramite le impostazioni in **Impostazioni progetto** -> **Sincronizzazione** -> **Individuazione delle tabelle di backup per le viste materializzate**).

## <a name="ssma-v76"></a>SSMA v7.6

La versione v7.6 di SSMA per Oracle è stata migliorata con correzioni mirate che migliorano la qualità e le metriche di conversione e con il supporto per SQL Server 2017 (anteprima pubblica). Il supporto per SQL Server 2017 in Windows e Linux è in anteprima pubblica e non deve essere usato per le migrazioni di produzione.

## <a name="ssma-v75"></a>SSMA v7.5

La versione v7.5 di SSMA per Oracle contiene le seguenti modifiche:

* Migliorato con diversi miglioramenti per garantire una maggiore accessibilità per le persone con disabilità.
* Aggiornato per migliorare la metrica di qualità e conversione con correzioni mirate, ad esempio una migliore gestione dei tipi di dati di data e float durante la migrazione dei dati, in base al feedback dei clienti.

## <a name="ssma-v74"></a>SSMA v7.4

La versione v7.4 di SSMA per Oracle contiene le seguenti modifiche:

* SSMA per Oracle ora supporta Azure SQL Data Warehouse come piattaforma di destinazione per la migrazione.

  ![Finestra Nuovo progetto](../media/new-project.png)
  * Supporta le opzioni di archiviazione del data warehouse, come illustrato nell'immagine seguente:Supports the Data Warehouse storage options as shown in the following image:

  ![opzioni di archiviazione per il data warehouse](../media/storage-options_red.png)
  * Supporta le opzioni di distribuzione dei dati come illustrato nell'immagine seguente:Supports the data distribution options as shown in the following image:

  ![distribuzione dei dati per il data warehouse](../media/data-distribution_red.png)

* L'opzione **Timeout query** è ora disponibile durante l'individuazione degli oggetti dello schema nell'origine e nella destinazione.

  ![opzione di timeout della query](../media/query-timeout_red.png)

* La metrica di qualità e conversione è stata migliorata con correzioni mirate, in base al feedback dei clienti.

> [!IMPORTANT]
> .NET 4.5.2 è un prerequisito per l'installazione di SSMA v7.4. Inoltre, a partire dalla v7.4, la versione a 32 bit di SSMA viene interrotta.

## <a name="ssma-v73"></a>SSMA v7.3

La versione v7.3 di SSMA per Oracle contiene le seguenti modifiche:

* Metriche di qualità e conversione migliorate con correzioni mirate in base al feedback dei clienti.
* Framework di estendibilità SSMA esposto tramite gli elementi seguenti:SSMA extensibility framework exposed via the following items:
  * Funzionalità di esportazione in un progetto SQL Server Data Tools (SSDT).
    * È ora possibile esportare gli script dello schema da SSMA a un progetto SSDT. È possibile utilizzare gli script dello schema per apportare ulteriori modifiche allo schema e distribuire il database.

      ![Comando salva come progetto SSDT](../media/export-schema-scripts_red.png)
  * Librerie che possono essere utilizzate da SSMA per l'esecuzione di conversioni personalizzate.
    * È ora possibile costruire codice in grado di gestire le conversioni di sintassi personalizzate e le conversioni che non sono state gestite in precedenza da SSMA.
      * Le istruzioni su come costruire un convertitore personalizzato sono disponibili in questo post di blog, Estensione delle funzionalità di [conversione di Assistente migrazione SQL Server.](https://blogs.msdn.microsoft.com/datamigration/2017/02/21/2185/)
      * Scarica un progetto di esempio per la conversione da questo post di [blog](https://blogs.msdn.microsoft.com/datamigration/ssmafororacleconversionsample/).

## <a name="ssma-v72"></a>SSMA v7.2

La versione v7.2 di SSMA per Oracle contiene le seguenti modifiche:

* Metriche di qualità e conversione migliorate con correzioni mirate in base al feedback dei clienti.
* Miglioramenti della telemetria per fornire punti dati migliori per risolvere i problemi dei clienti e migliorare i tassi di conversione di SSMA.

## <a name="ssma-v71"></a>SSMA v7.1

La versione v7.1 di SSMA per Oracle contiene le seguenti modifiche:

* SQL Server 2017 SQL su CTP1 di Windows e Linux è ora una piattaforma di destinazione supportata per la migrazione. Questa funzionalità è in anteprima tecnica e consente lo spostamento di schema e dati ai server SQL di destinazione.
* SSMA ora supporta gli aggiornamenti automatici per scaricare la versione più recente di SSMA non appena è disponibile.
* I file binari installabili SSMA vengono ora recapitati tramite i file del pacchetto di Windows Installer (MSI).

## <a name="may-2016"></a>Maggio 2016

La versione di maggio 2016 di SSMA per Oracle contiene le seguenti modifiche:

* Aggiunto il supporto per SQL Server 2016.Added support for SQL Server 2016.
* Aggiunta la conversione delle tabelle di archivio flashback Oracle in tabelle temporali di SQL Server.Added conversion of Oracle flashback archive tables to SQL Server temporal tables.

  > [!NOTE]
  > SSMA non copia i dati della cronologia dalle tabelle di Oracle Flashback Data Archive. Di conseguenza, i dati della cronologia devono essere copiati manualmente durante il processo di migrazione. In addition, while SSMA doesn't display the history table in the SQL Server metadata explorer because it's treated as a system table, you can view the history table in SQL Server Management Studio.
  >
  > SQL Server 2016 non supporta diverse funzionalità di Oracle Flashback, tra cui:
  >
  >   * Query sulle transazioni Flashback Oracle
  >   * `DBMS_FLASHBACK` Pacchetto
  >   * Transazione Flashback
  >   * Archivio dati Flashback
  >   * Tabella Flashback
  >   * Caduta Flashback
  >   * Flashback Database

* Aggiunta la conversione dei criteri Oracle VPD agli oggetti Criteri di SQL Server (protezione a livello di riga per Oracle).
* Riduzione del tempo di caricamento iniziale per Oracle.
* Parser e resolver migliorati.
* È stato rimosso il controllo del programma di installazione per .NET 2.0.Removed installer check for .NET 2.0.
* Dipendenza di Extension Pack aggiornata da .NET 3.5 a .NET 4.0.Updated Extension Pack dependency from .NET 3.5 to .NET 4.0.
* Risolto `save-project` `open-project` e comandi per la console SSMA.
* Comando `securepassword` fisso per la console SSMA.
* Corretto il conteggio degli oggetti per il caricamento iniziale.
* Correzione della conversione dei tipi di dati carattere per Oracle.Fixed converting of character data types for Oracle.
* Corretto bug in Impostazioni globali.

## <a name="march-2016"></a>marzo 2016

La versione di anteprima di marzo 2016 di SSMA per Oracle aggiunto il supporto per:

* Migrazione a SQL Server 2016.Migration to SQL Server 2016.
* Migrazione di Oracle Row Level Security (con alcune limitazioni).
* Migrazione di Oracle nelle tabelle di memoria all'archivio colonne di SQL Server.Migrating Oracle in memory tables to SQL Server Column Store.

## <a name="january-2016"></a>Gennaio 2016

La versione di manutenzione di gennaio 2014 di SSMA per Oracle contiene le seguenti modifiche:

* Aggiunto il supporto per gli indici cluster.
* Correzione delle query dello schema Oracle lente (RFC 5076207).
* Risolto il problema della connessione ad Azure dalla console.
* Aggiunta voce di menu Visualizza registro a SSMA (RFC 5706203).
* Aggiunto Telemetria.

## <a name="july-2014"></a>Luglio 2014

La versione di luglio 2014 di SSMA per Oracle contiene le seguenti modifiche:

* Aggiunto il supporto per il database SQL di Azure.Added support for Azure SQL DB.
* Funzionalità del pacchetto di estensione spostata nello schema per supportare il database SQL di Azure.Extension pack functionality moved to schema to support Azure SQL DB.
* Aggiunto il supporto per le viste Materializzate Oracle.Added support for Oracle Materialized views.
* Aggiunto il supporto per le tabelle con ottimizzazione per la memoria di SQL Server 2014.Added support for SQL Server 2014 Memory optimized tables.
* Miglioramenti delle prestazioni inclusi testati per i database con oltre 10k oggetti.
* Aggiunti miglioramenti dell'interfaccia utente per la gestione di un numero elevato di oggetti.
* Aggiunta l'evidenziazione degli schemi LOB noti.
* Inclusi i miglioramenti della velocità di conversione.
* Aggiunto il supporto per la visualizzazione dei conteggi degli oggetti nell'interfaccia utente.
* Dimensioni del report ridotte di oltre il 25%.
* Messaggi di errore migliorati per i costrutti non analizzati.

## <a name="april-2014"></a>Aprile 2014

La versione di aprile 2014 di SSMA per Oracle contiene le seguenti modifiche:

* Aggiunto il supporto di MS SQL Server 2014.
* Aggiunto il supporto di Oracle 12 e l'ottimizzazione delle query.
* Corretti i bug relativi alla conversione in Azure.Fixed bugs regarding conversion to Azure.
* Corretti i bug relativi alle pagine di report invisibili in IE 10.

## <a name="january-2012"></a>gennaio 2012

La versione di gennaio 2012 di SSMA per Oracle aggiunge il supporto per `RowType` e `RecordType` parametri di input per impostazione predefinita . `NULL`

## <a name="july-2011"></a>luglio 2011

La versione di luglio 2011 di SSMA per Oracle contiene le seguenti modifiche:

* Aggiunto il supporto per [!INCLUDE [ssSQL11](../../includes/sssql11-md.md)] la conversione della sequenza Oracle al generatore di sequenze.
* Segnalazione degli errori migliorata durante la migrazione dei dati.
* Migliorata la conversione dell'istruzione utilizzando parole riservate.
* È stata migliorata la conversione implicita del valore di data in una funzione.

## <a name="april-2011"></a>Aprile 2011

La versione di aprile 2011 di SSMA per Oracle contiene le seguenti modifiche:

* Prodotto consolidato "SSMA per Oracle", [!INCLUDE [ssSQL10](../../includes/sssql10-md.md)] [!INCLUDE [ssSQL11](../../includes/sssql11-md.md)]che supporta [!INCLUDE [ssVersion2005](../../includes/ssversion2005-md.md)], e .
* Aggiunto il supporto per [!INCLUDE [ssSQL11](../../includes/sssql11-md.md)]la connessione e la migrazione a .
* Motore di migrazione dei dati lato client migliorato, che supporta la migrazione parallela dei dati.
* Miglioramento delle prestazioni `Simple` `Bulk` di migrazione dei dati e dei modelli di recupero registrati.
* Aggiunto il supporto per la compatibilità con le versioni precedenti dei progetti creati da versioni precedenti di SSMA (v4.0 e v4.2).
* Aggiunta la possibilità di installare SSMA per Oracle v5.0 prodotto side-by-side (SxS) con versioni precedenti di SSMA (v4.0 e v4.2).
* Aggiunto il supporto per la segnalazione `VARRAY`dei `NESTED TABLE`tipi definiti dall'utente (include sottotipi, , , tabella oggetti e vista oggetto) e il relativo utilizzo nei blocchi PL/SQL con messaggi di errore speciali.

## <a name="july-2010"></a>Luglio 2010

La versione di luglio 2010 di SSMA per Oracle ha aggiunto:

* Supporto per la migrazione a SQL Server 2008 R2.
* Una nuova applicazione Console SSMA per l'esecuzione della riga di comando.
* Supporto per la migrazione dei dati tramite motori di migrazione dei dati lato server e lato client.
* Supporto per l'istruzione "Custom SELECT" nella migrazione dei dati.
* Supporto per la migrazione da Oracle 11g R2.

## <a name="june-2008"></a>Giugno 2008

La versione di giugno 2008 di SSMA per Oracle contiene le seguenti modifiche:

* Aggiunti miglioramenti al report di valutazione, incluse informazioni aggiuntive per i sinonimi, l'origine non elaborata per gli oggetti analizzabili, i pannelli e la rimozione del logo di SQL Server e la persistenza del layout.
* Aggiunti miglioramenti nella conversione degli oggetti:
  * Pacchetti `DBMS_LOB` `DBMS_SQL` , conversione aggiunta.
  * Unisce la conversione rivista.
  * Modifica delle raccolte e della conversione dei record, ora conversione dei record in casi semplici rilasciati tramite variabili separate per ogni campo.
  * Miglioramento dell'implementazione di record e raccolte.
  * Funzioni di aggregazione di windowing aggiunte.
  * `ROLLUP`/`CUBE`clausola aggiunta.
  * Miglioramento `NEXTVAL` / `CURVAL`per .
  * Sono state `SET` aggiunte colonne che raggruppano nella clausola, set di raggruppamento e ID di raggruppamento.
  * `MERGE`istruzione aggiunta.
  * Supporto di nuovi tipi datetime e conversione di record e raccolte con l'aggiunta di tipi di dati CLR.
* Aggiunte nuove funzionalità di Tester. Le tabelle possono ora essere testate come oggetti utilizzando Tester, è possibile modificare l'ordine di chiamata di diversi oggetti testabili nel test case, testare le procedure e le funzioni con record e raccolte come parametri e valori restituiti ed è stato aggiunto un analizzatore delle dipendenze per controllare solo le tabelle utilizzate.
  
## <a name="august-2007"></a>Agosto 2007

La versione di agosto 2007 di SSMA per Oracle ha aggiunto:

* Un nuovo componente Tester consente di creare, gestire ed eseguire test case per verificare il codice SQL convertito.
* Il supporto per la conversione di sottotipi, raccolte e moduli locali Oracle è stato aggiunto al convertitore SQL.
* Una nuova funzionalità di sincronizzazione consente di sincronizzare oggetti specifici con il database di SQL Server.
* Nuove opzioni di conversione.
  
## <a name="april-2007"></a>Aprile 2007

La versione di aprile 2007 di SSMA per Oracle è stata la versione iniziale.
