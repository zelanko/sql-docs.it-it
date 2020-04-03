---
title: Novità di SSMA per DB2 (DB2ToSQL) Documenti Microsoft
authors: HJToland3;nahk-ivanov
ms.prod: sql
ms.custom: ''
ms.date: 4/2/2020
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 1cc38f85-3caa-42d0-8c76-a380c1d15c67
ms.author: jtoland;alexiva
ms.openlocfilehash: 53a159627750a5ec66b5aa0b3fd6510c647e26a5
ms.sourcegitcommit: d818a307725983c921987749915fe1a381233d98
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/03/2020
ms.locfileid: "80625517"
---
# <a name="whats-new-in-ssma-for-db2-db2tosql"></a>Novità di SSMA per DB2 (DB2ToSQL)

In questo articolo vengono elencate le modifiche di SQL Server Migration Assistant (SSMA) per DB2 in ogni versione.

## <a name="ssma-v88"></a>SSMA v8.8

La versione v8.8 di SSMA per DB2 include:

* Miglioramenti alla stabilità della sincronizzazione degli oggetti di SQL ServerSQL Server objects synchronization stability improvements
* Miglioramenti delle prestazioni dell'interfaccia grafica durante la valutazione e la conversione
* Mapping aggiornato `ROWID` `varbinary(40)` da a per facilitare la migrazione dei dati
* Conversione `SELECT ... FROM NEW/OLD TABLE` migliorata delle istruzioni
* Nuova conversione di `ALTER` rendiconti per procedure e funzioni
* Nuova conversione delle assegnazioni di destrutturazione

## <a name="ssma-v87"></a>SSMA v8.7

La versione v8.7 di SSMA per DB2 include il nuovo parser di sintassi DB2, nonché correzioni minori e miglioramenti delle prestazioni nell'interfaccia utente grafica.

Inoltre, SSMA per DB2 ora fornisce:In addition, SSMA for DB2 now provides:

* Correzione per l'individuazione delle chiavi esterne durante la migrazione da DB2 in LUW.
* Migliorata `SELECT ... FOR UPDATE` la conversione dell'istruzione.
* È stata `COUNT` migliorata la conversione per la funzione nelle tabelle MQ.
* Conversione `SAVEPOINT` di dichiarazioni.
* Conversione per emulare il `NULL` comportamento `ORDER BY` di DB2 per i valori nella clausola.
* Analisi del supporto per l'istruzione ASSOCIATE RESULT SET.

> [!IMPORTANT]
> Con SSMA v8.5 e versioni successive, .NET 4.7.2 è un prerequisito per l'installazione. Se è necessario installare questa versione, è possibile scaricare il file di runtime da [qui](https://dotnet.microsoft.com/download/dotnet-framework/net472).

## <a name="ssma-v86"></a>SSMA v8.6

Oltre a un set mirato di correzioni progettate per migliorare l'usabilità e le prestazioni, la versione v8.6 di SSMA per DB2 è stata migliorata aggiungendo un'impostazione che consente agli utenti di omettere le proprietà estese SSMA nel codice convertito.

Per utilizzare questa impostazione, in SSMA per DB2 passare a **Strumenti** > **Impostazioni** > di progetto**Conversione****generale** > , quindi in **Varie**aggiornare il valore dell'impostazione **Omettere proprietà estese** su **Sì**.

![Omettere l'impostazione delle proprietà estese](../db2/media/ssma-omit-extended-properties.png)

Inoltre, SSMA per DB2 ora fornisce:In addition, SSMA for DB2 now provides:

* Correzione per la conversione di funzioni che utilizzano valori di argomento predefiniti.
* Analisi migliorata della `PARAMETER` clausola per le funzioni.
* La possibilità di `LEAVE` convertire l'istruzione.

> [!IMPORTANT]
> Con SSMA v8.5 e versioni successive, .NET 4.7.2 è un prerequisito per l'installazione. Se è necessario installare questa versione, è possibile scaricare il file di runtime da [qui](https://dotnet.microsoft.com/download/dotnet-framework/net472).

## <a name="ssma-v85"></a>SSMA v8.5

La versione v8.5 di SSMA per DB2 è stata migliorata con il supporto per l'autenticazione di Azure Active Directory e il supporto di base per le funzionalità JSON nel server SQL, insieme a un set mirato di correzioni progettate per migliorare l'usabilità e le prestazioni.

Inoltre, SSMA per DB2 è stato migliorato con:

* Supporto per l'aggiunta della conversione per `GET DIAGNOSTICS` l'istruzione con `ROW_NUMBER`.
* Correzione per un bug relativo agli spazi all'inizio del nome dell'oggetto non viene rispettato.

> [!IMPORTANT]
> Con SSMA v8.5, .NET 4.7.2 è un prerequisito per l'installazione. Se è necessario installare questa versione, è possibile scaricare il file di runtime da [qui](https://dotnet.microsoft.com/download/dotnet-framework/net472).

## <a name="ssma-v84"></a>SSMA v8.4

La versione v8.4 di SSMA per DB2 è stata migliorata con correzioni mirate progettate per risolvere i problemi di accessibilità e correggere un bug relativo alle colonne di indice max (per consentire 32 anziché 16) per SQL Server 2016 e versioni successive.

> [!IMPORTANT]
> Con SSMA versioni 7.4 anche 8.4, .NET 4.5.2 è un prerequisito per l'installazione.

## <a name="ssma-v83"></a>SSMA v8.3

La versione v8.3 di SSMA per DB2 è stata migliorata con correzioni mirate progettate per migliorare la qualità e le metriche di conversione. Inoltre, questa versione di SSMA per DB2 fornisce correzioni che:In addition, this release of SSMA for DB2 provides fixes that:

* Risolvere i problemi di accessibilità.
* Aggiungere il `hierarchyid` supporto di base per il tipo in SQL Server.Add basic support for type in SQL Server.
* Sostituire l'utilizzo della funzione TRIM `RTRIM` / `LTRIM`nelle query di individuazione z/OS con .
* Consenti all'utente di specificare la raccolta di `NULLID`pacchetti quando ci si connette in 'Modalità Standard' (l'impostazione predefinita è ).
* Aggiungere la `CREATE TABLE AS SELECT`conversione per .
* Migliorare le conversioni per le tabelle temporanee globali.
* Risolvere un problema con l'ordine di controllo dell'univocità degli oggetti per assegnare priorità alle tabelle rispetto ai vincoli, se i nomi collidono.
* Risolvere un problema relativo al `DATE` `TIMESTAMP` caricamento di valori di colonna predefiniti per e per z/OS.
* Supporta il carattere di `NEL`avanzamento riga Unicode (noto anche come ).
* Risolvere un problema con `RETURN TO` la conversione del cursore con clausola mancante.
* Aggiungere il supporto `GOTO`per le etichette e .

## <a name="ssma-v82"></a>SSMA v8.2

La versione v8.2 di SSMA per DB2 è stata migliorata con per risolvere i problemi relativi alle connessioni al database SQL di Azure dallo strumento console SSMA e manca COUNT_BIG colonna nella dichiarazione di viste durante la conversione. Inoltre, questa versione include un set mirato di correzioni progettate per migliorare la qualità e le metriche di conversione, nonché correzioni per:

* Problema con gli indici non cluster disabilitati dopo la migrazione dei dati.
* Rilevamento di .NET Framework durante l'installazione invisibile all'utente.
* Arresto anomalo intermittente che si verifica quando viene scaricata una nuova versione.

> [!NOTE]
> Un problema noto con l'aggiornamento automatico può causare l'errore di un aggiornamento da SSMA v8.1 a v8.2. Se si verifica questo errore, scaricare la nuova versione e installarla manualmente.

## <a name="ssma-v81"></a>SSMA v8.1

La versione v8.1 di SSMA per DB2 è stata migliorata per fornire correzioni mirate progettate per migliorare la qualità e le metriche di conversione.

> [!NOTE]
> Un problema noto con l'aggiornamento automatico può causare l'errore di un aggiornamento da SSMA v8.0 a v8.1. Se si verifica questo errore, scaricare la nuova versione e installarla manualmente.

## <a name="ssma-v80"></a>SSMA v8.0

La versione v8.0 di SSMA per DB2 è stata migliorata per fornire correzioni mirate progettate per migliorare la qualità e le metriche di conversione. Questa versione offre anche le seguenti nuove funzionalità:

* Supporto per **l'istanza gestita del database SQL** di Azure come destinazione. È ora possibile creare nuovi progetti destinati all'istanza gestita del database SQL di Azure:You can now create new projects targeting Azure SQL Database Managed Instance:

  ![Progetto SQL DB MI](../media/ssma-newproject-sqldbmi.png)

* Avviso **fix**post-conversione . Scopri di più [qui](https://blogs.msdn.microsoft.com/datamigration/2019/02/17/%20accelerate-your-oracle-migrations-with-new-machine-learning-capabilities-in-ssma/).

* Selezione preliminare di database/schema.

  Quando ci si connette all'origine, l'utente può ora selezionare database/schemi di interesse. Selezionando solo gli schemi che si prevede di eseguire la migrazione si risparmia tempo durante la connessione iniziale e migliorare le prestazioni complessive SSMA.

  ![Oggetti filtro SSMASSMA filter objects](../media/ssma-filter-objects.png)

## <a name="ssma-v710"></a>SSMA v7.10

La versione v7.10 di SSMA per DB2 contiene le seguenti modifiche:

* Correzioni mirate progettate per fornire ulteriori protezioni di sicurezza e privacy per soddisfare i cambiamenti nei requisiti globali.
* Una correzione per `BEGIN-END` la conversione dei blocchi.

## <a name="ssma-v79"></a>SSMA v7.9

La versione v7.9 di SSMA per DB2 contiene le seguenti modifiche:

* Correzioni mirate che migliorano la qualità e le metriche di conversione.
* Supporto nella riga di comando SSMA per modificare il mapping dei tipi di dati e le preferenze di progetto.
* Supporto per la migrazione dei dati tramite SQL Server Integration Services (SSIS). Dopo aver convertito lo schema, è possibile creare un pacchetto SSIS utilizzando un'opzione del menu di scelta rapida.
* Anche la finestra di dialogo di connessione al database SQL di Azure in SSMA è stata modificata per specificare il nome completo del server. Nelle versioni precedenti di SSMA, il prefisso del database SQL di Azure doveva essere menzionato in modo esplicito all'interno delle impostazioni dei progetti.

## <a name="ssma-v78"></a>SSMA v7.8

La versione v7.8 di SSMA per DB2 contiene le seguenti modifiche:

* Modifica del mapping dei tipi evidenziato in *Impostazioni progetto*.
* Possibilità per gli utenti di disabilitare i dati di telemetria.

## <a name="ssma-v77"></a>SSMA v7.7

La versione v7.7 di SSMA per DB2 contiene le seguenti modifiche:

* Correzioni mirate che migliorano la qualità e le metriche di conversione.
* In base alla richiesta popolare, la versione a 32 bit di SSMA per DB2 è tornato. Rispetto all'implementazione precedente (prima della v7.4), sono disponibili due pacchetti di installazione, ma non possono essere installati affiancati. Di conseguenza, è necessario scegliere la versione più appropriata in base ai componenti di connettività disponibili. È sempre preferibile utilizzare la versione a 64 bit, se possibile.

## <a name="ssma-v76"></a>SSMA v7.6

La versione v7.6 di SSMA per DB2 è stata migliorata con correzioni mirate che migliorano la qualità e le metriche di conversione e con il supporto per SQL Server 2017 (anteprima pubblica). Il supporto per SQL Server 2017 in Windows e Linux è in anteprima pubblica e non deve essere usato per le migrazioni di produzione.

## <a name="ssma-v75"></a>SSMA v7.5

La versione v7.5 di SSMA per DB2 è stata migliorata con diversi miglioramenti per garantire una maggiore accessibilità per le persone con disabilità.

## <a name="ssma-v74"></a>SSMA v7.4

La versione v7.4 di SSMA per DB2 contiene le seguenti modifiche:

* L'opzione **Timeout query** è ora disponibile durante l'individuazione degli oggetti dello schema nell'origine e nella destinazione.

  ![opzione di timeout della query](../media/query-timeout_red.png)

* La metrica di qualità e conversione è stata migliorata con correzioni mirate, in base al feedback dei clienti.

  > [!IMPORTANT]
  > .NET 4.5.2 è un prerequisito per l'installazione di SSMA v7.4. Inoltre, a partire dalla v7.4, la versione a 32 bit di SSMA è stata interrotta.

## <a name="ssma-v73"></a>SSMA v7.3

La versione v7.3 di SSMA per DB2 contiene le seguenti modifiche:

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

La versione v7.2 di SSMA per DB2 contiene le seguenti modifiche:

* Metriche di qualità e conversione migliorate con correzioni mirate in base al feedback dei clienti.
* Miglioramenti della telemetria per fornire punti dati migliori per risolvere i problemi dei clienti e migliorare i tassi di conversione di SSMA.

## <a name="ssma-v71"></a>SSMA v7.1

La versione v7.1 di SSMA per DB2 contiene le seguenti modifiche:

* SQL Server 2017 SQL su CTP1 di Windows e Linux è ora una piattaforma di destinazione supportata per la migrazione. Questa funzionalità è in anteprima tecnica e consente lo spostamento di schema e dati ai server SQL di destinazione.
* Supporto per gli aggiornamenti automatici per scaricare la versione più recente di SSMA non appena è disponibile.
* I file binari installabili SSMA vengono ora recapitati tramite i file del pacchetto di Windows Installer (MSI).

## <a name="may-2016"></a>Maggio 2016

La versione di maggio 2016 di SSMA per DB2 contiene le seguenti modifiche:

* Aggiunto il supporto per SQL Server 2016.Added support for SQL Server 2016.
* Aggiunta la conversione di tabelle regolari e DB2 in funzionalità in memoria e hekaton di SQL Server.Added conversion of DB2 in-memory and regular tables to SQL Server in-memory and hekaton features.
* Aggiunta la conversione dei controlli di accesso DB2 agli oggetti Criteri di SQL Server (protezione a livello di riga per DB2).
* Aggiunta la conversione delle tabelle con controllo delle versioni di sistema DB2 in tabelle temporali di SQL ServerSQL Server .
* Parser e resolver DB2 migliorati.
* È stato rimosso il controllo del programma di installazione per .NET 2.0.Removed installer check for .NET 2.0.
* È \*stata rimossa la DLL non necessaria dal programma di installazione db2.
* Risolto `save-project` `open-project` e comandi per la console SSMA.
* Comando `securepassword` fisso per la console SSMA.
* Corretto il conteggio degli oggetti per il caricamento iniziale.
* Corretto bug nelle impostazioni globali.
  
## <a name="march-2016"></a>marzo 2016

La versione di anteprima di marzo 2016 di SSMA per DB2 aggiunge il supporto per la migrazione a SQL Server 2016.The March 2016 preview release of SSMA for DB2 adds support for migration to SQL Server 2016.

## <a name="january-2016"></a>Gennaio 2016

La versione di manutenzione di gennaio 2016 di SSMA per DB2 contiene le seguenti modifiche:
  
* Aggiunto il supporto per una serie di funzioni standard.
* Correzione degli errori del parser DB2.
* Fisso DB2 v9 zOS Support (RFC 5690920).
* Correzione degli errori di identificatore non risolti DB2 durante la conversione.
* Aggiunta voce di menu Visualizza registro a SSMA (RFC 5706203).
* Aggiunto Telemetria.
  
## <a name="november-2014"></a>Novembre 2014

La versione di novembre 2014 di SSMA per DB2 è stata la versione iniziale.
