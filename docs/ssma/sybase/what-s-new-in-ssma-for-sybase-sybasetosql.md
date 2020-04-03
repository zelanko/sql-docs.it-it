---
title: Novità di SSMA per SAP ASE (SybaseToSQL) Documenti Microsoft
authors: HJToland3;nahk-ivanov
ms.prod: sql
ms.custom: ''
ms.date: 4/2/2020
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 2be0cf8d-6dbe-443a-abbd-036249922205
ms.author: jtoland;alexiva
ms.openlocfilehash: 7f23c7e1c676b4ade42b43cf963e0fa6956f93c6
ms.sourcegitcommit: d818a307725983c921987749915fe1a381233d98
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/03/2020
ms.locfileid: "80625591"
---
# <a name="whats-new-in-ssma-for-sap-ase-sybasetosql"></a>Novità di SSMA per SAP ASE (SybaseToSQL)

In questo articolo vengono elencate le modifiche di SQL Server Migration Assistant (SSMA) per SAP ASE (in precedenza SSMA per Sybase) in ogni versione.

## <a name="ssma-v88"></a>SSMA v8.8

La versione v8.8 di SSMA per SAP ASE include:

* Miglioramenti alla stabilità della sincronizzazione degli oggetti di SQL ServerSQL Server objects synchronization stability improvements
* Miglioramenti delle prestazioni dell'interfaccia grafica durante la valutazione e la conversione
* Correzione del problema con i caratteri mancanti nelle definizioni SQL per gli oggettiFix for the issue with missing characters in SQL definitions for objects

## <a name="ssma-v87"></a>SSMA v8.7

La versione v8.7 di SSMA per SAP ASE presenta correzioni minori e miglioramenti delle prestazioni nell'interfaccia utente grafica.

> [!IMPORTANT]
> Con SSMA v8.5 e versioni successive, .NET 4.7.2 è un prerequisito per l'installazione. Se è necessario installare questa versione, è possibile scaricare il file di runtime da [qui](https://dotnet.microsoft.com/download/dotnet-framework/net472).

## <a name="ssma-v86"></a>SSMA v8.6

Oltre a un set mirato di correzioni progettate per migliorare l'usabilità e le prestazioni, la versione v8.6 di SSMA per SAP ASE è stata migliorata aggiungendo un'impostazione che consente agli utenti di omettere le proprietà estese SSMA nel codice convertito.

Per utilizzare questa impostazione, in SSMA per SAP ASE passare a **Strumenti** > **Impostazioni** > generali impostazioni progetto**Conversione****generale** > , quindi in **Varie**aggiornare il valore dell'impostazione **Omettere proprietà estese** su **Sì**.

![Omettere l'impostazione delle proprietà estese](../sybase/media/ssma-omit-extended-properties.png)

> [!IMPORTANT]
> Con SSMA v8.5 e versioni successive, .NET 4.7.2 è un prerequisito per l'installazione. Se è necessario installare questa versione, è possibile scaricare il file di runtime da [qui](https://dotnet.microsoft.com/download/dotnet-framework/net472).

## <a name="ssma-v85"></a>SSMA v8.5

La versione v8.5 di SSMA per SAP ASE è stata migliorata con il supporto per l'autenticazione di Azure Active Directory e il supporto di base per le funzionalità JSON nel server SQL, insieme a un set mirato di correzioni progettate per migliorare l'usabilità e le prestazioni.

Inoltre, SSMA per SAP ASE ora consente di nascondere le tabelle e le visualizzazioni di sistema (escluderle dalla conversione).

> [!IMPORTANT]
> Con SSMA v8.5, .NET 4.7.2 è un prerequisito per l'installazione. Se è necessario installare questa versione, è possibile scaricare il file di runtime da [qui](https://dotnet.microsoft.com/download/dotnet-framework/net472).

## <a name="ssma-v84"></a>SSMA v8.4

La versione v8.4 di SSMA per SAP ASE è stata migliorata con correzioni mirate progettate per risolvere i problemi di accessibilità e correggere un bug relativo alle colonne dell'indice max (per consentire 32 anziché 16) per SQL Server 2016 e versioni successive.

> [!IMPORTANT]
> Con le versioni SSMA da 7.4 a 8.4, .NET 4.5.2 è un prerequisito per l'installazione.

## <a name="ssma-v83"></a>SSMA v8.3

La versione v8.3 di SSMA per SAP ASE è stata migliorata con correzioni mirate progettate per migliorare la qualità e le metriche di conversione. Inoltre, questa versione di SSMA per SAP ASE fornisce correzioni che:

* Risolvere i problemi di accessibilità
* Aggiungere il `hierarchyid` supporto di base per il tipo in SQL ServerAdd basic support for type in SQL Server

## <a name="ssma-v82"></a>SSMA v8.2

La versione v8.2 di SSMA per SAP ASE è stata migliorata con un set mirato di correzioni progettate per migliorare le metriche di qualità e conversione, nonché correzioni per:

* Problema con gli indici non cluster disabilitati dopo la migrazione dei dati.
* Rilevamento di .NET Framework durante l'installazione invisibile all'utente.
* Arresto anomalo intermittente che si verifica quando viene scaricata una nuova versione.

> [!NOTE]
> Un problema noto con l'aggiornamento automatico può causare l'errore di un aggiornamento da SSMA v8.1 a v8.2. Se si verifica questo errore, scaricare la nuova versione e installarla manualmente.

## <a name="ssma-v81"></a>SSMA v8.1

La versione v8.1 di SSMA per SAP ASE è stata migliorata con correzioni mirate progettate per migliorare la qualità e le metriche di conversione.

> [!NOTE]
> Un problema noto con l'aggiornamento automatico può causare l'errore di un aggiornamento da SSMA v8.0 a v8.1. Se si verifica questo errore, scaricare la nuova versione e installarla manualmente.

## <a name="ssma-v80"></a>SSMA v8.0

La versione v8.0 di SSMA per SAP ASE è stata migliorata con correzioni mirate progettate per migliorare la qualità e le metriche di conversione. Inoltre, questa versione offre le seguenti nuove funzionalità:

* Supporto per **l'istanza gestita del database SQL** di Azure come destinazione. È ora possibile creare nuovi progetti destinati all'istanza gestita del database SQL di Azure:You can now create new projects targeting Azure SQL Database Managed Instance:

  ![Progetto SQL DB MI](../media/ssma-newproject-sqldbmi.png)

* Avviso **fix**post-conversione . Scopri di più [qui](https://blogs.msdn.microsoft.com/datamigration/2019/02/17/%20accelerate-your-oracle-migrations-with-new-machine-learning-capabilities-in-ssma/).

* Selezione preliminare di database/schema.

  Quando ci si connette all'origine, l'utente può ora selezionare database/schemi di interesse. Selezionando solo gli schemi che si prevede di eseguire la migrazione si risparmia tempo durante la connessione iniziale e migliorare le prestazioni complessive SSMA.

  ![Oggetti filtro SSMASSMA filter objects](../media/ssma-filter-objects.png)

## <a name="ssma-v710"></a>SSMA v7.10

La versione v7.10 di SSMA per SAP ASE è stata migliorata con correzioni mirate progettate per fornire ulteriori protezioni della sicurezza e della privacy per soddisfare i cambiamenti nei requisiti globali.

## <a name="ssma-v79"></a>SSMA v7.9

La versione v7.9 di SSMA per SAP ASE contiene le seguenti modifiche:

* Correzioni mirate che migliorano la qualità e le metriche di conversione.
* Supporto nella riga di comando SSMA per modificare il mapping dei tipi di dati e le preferenze di progetto.
* Supporto per la migrazione dei dati tramite SQL Server Integration Services (SSIS). Dopo aver convertito lo schema, è possibile creare un pacchetto SSIS utilizzando un'opzione del menu di scelta rapida.
* Anche la finestra di dialogo di connessione al database SQL di Azure in SSMA è stata modificata per specificare il nome completo del server. Nelle versioni precedenti di SSMA, il prefisso del database SQL di Azure doveva essere menzionato in modo esplicito all'interno delle impostazioni dei progetti.

## <a name="ssma-v78"></a>SSMA v7.8

La versione v7.8 di SSMA per SAP ASE contiene le seguenti modifiche:

* Modifica del mapping dei tipi evidenziato in **Impostazioni progetto**.
* Possibilità per gli utenti di disabilitare i dati di telemetria.

## <a name="ssma-v77"></a>SSMA v7.7

La versione v7.7 di SSMA per SAP ASE contiene le seguenti modifiche:

* SSMA per SAP ASE è stato migliorato con correzioni mirate che migliorano la qualità e le metriche di conversione.
* In base alla richiesta popolare, la versione a 32 bit di SSMA per SAP ASE è tornato. Rispetto all'implementazione precedente (prima della v7.4), sono disponibili due pacchetti di installazione, ma non possono essere installati affiancati. Di conseguenza, è necessario scegliere la versione più appropriata in base ai componenti di connettività disponibili. È sempre preferibile utilizzare la versione a 64 bit, se possibile.

## <a name="ssma-v76"></a>SSMA v7.6

La versione v7.6 di SSMA per SAP ASE contiene le seguenti modifiche:

* Correzioni mirate che migliorano la qualità e le metriche di conversione e con il supporto per SQL Server 2017 (anteprima pubblica). Il supporto per SQL Server 2017 in Windows e Linux è in anteprima pubblica e non deve essere usato per le migrazioni di produzione.
* Supporto per la conversione delle funzioni Sybase.

## <a name="ssma-v75"></a>SSMA v7.5

La versione v7.5 di SSMA per SAP ASE (precedentemente SSMA per Sybase) contiene le seguenti modifiche:

* Diversi miglioramenti per garantire una maggiore accessibilità per le persone con disabilità.
* Supporto `CREATE OR REPLACE` per la sintassi.

## <a name="ssma-v74"></a>SSMA v7.4

La versione v7.4 di SSMA per Sybase contiene le seguenti modifiche:

* L'opzione **Timeout query** è ora disponibile durante l'individuazione degli oggetti dello schema nell'origine e nella destinazione.

  ![opzione di timeout della query](../media/query-timeout_red.png)
* La metrica di qualità e conversione è stata migliorata con correzioni mirate, in base al feedback dei clienti.

  > [!IMPORTANT]
  > .NET 4.5.2 è un prerequisito per l'installazione di SSMA v7.4. Inoltre, a partire dalla v7.4, la versione a 32 bit di SSMA viene interrotta.

## <a name="ssma-v73"></a>SSMA v7.3

La versione v7.3 di SSMA per Sybase contiene le seguenti modifiche:

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

La versione v7.2 di SSMA per Sybase contiene le seguenti modifiche:

* Metriche di qualità e conversione migliorate con correzioni mirate in base al feedback dei clienti.
* Miglioramenti della telemetria per fornire punti dati migliori per risolvere i problemi dei clienti e migliorare i tassi di conversione di SSMA.

## <a name="ssma-v71"></a>SSMA v7.1

La versione v7.1 di SSMA per Sybase contiene le seguenti modifiche:

* SQL Server 2017 SQL su CTP1 di Windows e Linux è ora una piattaforma di destinazione supportata per la migrazione. Questa funzionalità è in anteprima tecnica e supporta lo spostamento di schema e dati ai server SQL di destinazione.
* Supporto per gli aggiornamenti automatici per scaricare la versione più recente di SSMA non appena è disponibile.
* I file binari installabili SSMA vengono ora recapitati tramite i file del pacchetto di Windows Installer (MSI).

## <a name="may-2016"></a>Maggio 2016

La versione di maggio 2016 di SSMA per Sybase contiene le seguenti modifiche:

* Aggiunto il supporto per SQL Server 2016.Added support for SQL Server 2016.
* È stato rimosso il controllo del programma di installazione per .NET 2.0.Removed installer check for .NET 2.0.
* Dipendenza di Extension Pack aggiornata da .NET 3.5 a .NET 4.0.Updated Extension Pack dependency from .NET 3.5 to .NET 4.0.
* Risolto `save-project` `open-project` e comandi per la console SSMA.
* Comando `securepassword` fisso per la console SSMA.
* Corretto il conteggio degli oggetti per il caricamento iniziale.
* Corretto bug nelle impostazioni globali.

## <a name="march-2016"></a>marzo 2016

La versione di anteprima di marzo 2016 di SSMA per Sybase aggiunge il supporto per la migrazione a SQL Server 2016.

## <a name="january-2016"></a>Gennaio 2016

La versione di manutenzione di gennaio 2016 di SSMA per Sybase contiene le seguenti modifiche:

* Aggiunta voce di menu Visualizza registro a SSMA (RFC 5706203).
* Aggiunto Telemetria.

## <a name="july-2014"></a>Luglio 2014

La versione di luglio 2014 di SSMA per Sybase contiene le seguenti modifiche:

* Conversione del codice del database SQL di Azure migliorata.
* È stata spostata la funzionalità del pacchetto di estensione allo schema per supportare il database SQL di Azure.Moved extension pack functionality to schema to support Azure SQL DB.
* Aggiunti miglioramenti delle prestazioni testati per i database con oltre 10k oggetti.
* Aggiunti miglioramenti dell'interfaccia utente per la gestione di un numero elevato di oggetti.
* Aggiunta la possibilità di evidenziare schemi LOB noti (in modo che possano essere ignorati nella conversione).
* Aggiunti miglioramenti alla velocità di conversione.
* Aggiunta la possibilità di mostrare i conteggi degli oggetti nell'interfaccia utente.
* Dimensioni del report ridotte di oltre il 25%.
* Messaggi di errore migliorati per i costrutti non analizzati.

## <a name="april-2014"></a>Aprile 2014

La versione di aprile 2014 di SSMA per Sybase contiene le seguenti modifiche:

* Aggiunto il supporto di MS SQL Server 2014.
* Corretti i bug relativi alla conversione in Azure.Fixed bugs regarding conversion to Azure.
* Corretti i bug relativi alle pagine di report invisibili in IE 10.

## <a name="january-2012"></a>gennaio 2012

La versione di gennaio 2012 di SSMA per Sybase contiene le seguenti modifiche:

* Aggiunto il supporto per la conversione del trigger di rollback.
* Fornito fix per `@@ROWCOUNT` `@@ERROR` la conversione e nella stessa `SET` istruzione.

## <a name="july-2011"></a>luglio 2011

La versione di luglio 2011 di SSMA per Sybase fornisce una migliore segnalazione degli errori durante la migrazione dei dati.

## <a name="april-2011"></a>Aprile 2011

La versione di aprile 2011 di SSMA per Sybase contiene le seguenti modifiche:

* Prodotto consolidato "SSMA for Sybase", [!INCLUDE [ssSQL10](../../includes/sssql10-md.md)] [!INCLUDE [ssSQL11](../../includes/ssSQL11-md.md)] che supporta [!INCLUDE [ssVersion2005](../../includes/ssversion2005-md.md)], e SQL di Azure.
* Aggiunto il supporto per [!INCLUDE [ssSQL11](../../includes/sssql11-md.md)]la connessione e la migrazione a .
* Aggiunta una nuova funzionalità per convertire ed eseguire la migrazione dei database Sybase in SQL di Azure.Added a new feature to convert and migrate Sybase databases to Azure SQL.
* Motore di migrazione dei dati lato client migliorato, che supporta la migrazione parallela dei dati.
* Miglioramento delle prestazioni di migrazione dei dati con i modelli di recupero con registrazione semplice e con registrazione bulk.
* Aggiunta la possibilità di convertire e migrare correttamente i database Sybase con distinzione tra maiuscole e minuscole in SQL Server con distinzione tra maiuscole e minuscole.
* È stato esteso il supporto per la conversione delle istruzioni di join non ANSI Sybase ASE in istruzioni join ANSI di SQL ServerSQL Server.
* Sono state fornite opzioni di connettività aggiuntive per la connessione ai server Sybase ASE utilizzando il provider ODBC Sybase ASE e il provider di ADO.NET Sybase ASE.
* È stata rimossa la `SysDB`dipendenza da un database separato denominato , che contiene le funzioni di emulazione Sybase (installate come parte di Extension Pack).
* Aggiunta la possibilità di installare SSMA per [!INCLUDE [ssNoVersion](../../includes/ssnoversion-md.md)] Sybase Extension Pack nei cluster.
* Aggiunta la compatibilità con le versioni precedenti dei progetti creati da versioni precedenti di SSMA (v4.0 e v4.2).
* Aggiunta la possibilità di installare sSMA per Sybase v5.0 prodotto side-by-side (SxS) con versioni precedenti di SSMA (v4.0 e v4.2).

## <a name="july-2010"></a>Luglio 2010

La versione di luglio 2010 di SSMA per Sybase ha aggiunto:

* Supporto per la migrazione a SQL Server 2008 R2.
* Una nuova applicazione Console SSMA per l'esecuzione della riga di comando.
* Supporto per la migrazione dei dati tramite motori di migrazione dei dati lato server e lato client.
* Supporto per l'istruzione "Custom SELECT" nella migrazione dei dati.
* Supporto per la migrazione da Sybase ASE 15.0.3 e 15.5.Support for migrating from Sybase ASE 15.0.3 and 15.5.

## <a name="june-2008"></a>Giugno 2008

La versione di giugno 2008 di SSMA per Sybase contiene le seguenti modifiche:

* Aggiunto Tester SSMA, che verifica automaticamente la conversione degli oggetti di database e la migrazione dei dati effettuata da SSMA. Al termine di tutti i passaggi di migrazione SSMA, usare Tester SSMA per verificare che gli oggetti convertiti funzionino allo stesso modo e che tutti i dati siano stati trasferiti correttamente.
* Aggiunta la conversione pre-SQL. L'utente può ora specificare le dichiarazioni di tabella temporanea (e altri oggetti) per ogni procedura di origine da utilizzare nella conversione.
* Aggiunti miglioramenti nella conversione degli oggetti:
  * Unisce la conversione rivista.
  * Aggregazioni e non aggregazioni senza clausole having/group by.
  * Funzione `IDENTITY` con `SELECT INTO` un'istruzione.
  * Vincoli cluster e indici bloccati solo ai dati.
  * Tabelle temporanee `SELECT INTO`create da .
  * Vincoli / Indici per le tabelle temporanee.
  * Sono [!INCLUDE [ssSQL10](../../includes/sssql10-md.md)] supportati nuovi tipi datetime.
  * La connettività e i tipi di dati di Sybase 15.0 sono supportati.

## <a name="may-2007"></a>Maggio 2007

La versione di maggio 2007 di SSMA per Sybase ha aggiunto:

* Possibilità di caricare più rapidamente il contenuto del database durante il salvataggio di un progetto.
* Supporto per i commenti immessi dall'utente in modalità SQL in formato SQL ServerSQL Server.Support for user-entered comments in the SQL Server formatted SQL mode.
* Miglioramenti nella conversione degli oggetti.

## <a name="november-2006"></a>Novembre 2006

La versione di novembre 2006 di SSMA per Sybase contiene le seguenti modifiche:

* Aggiunte nuove impostazioni globali:
  * È possibile scegliere di visualizzare i numeri di riga nelle finestre dell'editor.
  * È possibile configurare SSMA per richiedere di sostituire gli oggetti duplicati o sempre o mai sostituire gli oggetti duplicati durante la conversione dello schema.
* Aggiunta una nuova opzione di conversione che consente di configurare il modo in cui SSMA gestisce le situazioni seguenti:Added a new conversion option that lets you configure how SSMA handles the following situations:
  * Un'istruzione `CAST` o `CONVERT` che contiene una stringa binaria.
  * Controlla i valori Null nelle espressioni di uguaglianza.
  * Tabelle proxy.
  * Numeri di errore `RAISERROR`dei messaggi utente per .
  * `UPDATE`dichiarazioni che contengono identificatori non risolti.
* Aggiunta una nuova opzione di migrazione che consente di specificare [!INCLUDE [ssNoVersion](../../includes/ssnoversion-md.md)] come SSMA deve gestire le date che non sono all'esterno dell'intervallo di date.
* Aggiunta un'impostazione **SQL formattato** nella scheda **SQL,** che formatta il codice per migliorare la leggibilità.
* Correzioni di bug, tra cui:
  * SSMA ora `LOCK TABLE <table> IN { SHARED | EXCLUSIVE } MODE` converte le `TABLOCK` istruzioni `TABLOCKX` aggiungendo un `SELECT` o hint alla query successiva nella tabella.
  * I cast necessari vengono ora aggiunti quando i tipi binari vengono utilizzati nelle espressioni carattere.
  * Miglioramenti della memoria e delle prestazioni.

## <a name="july-2006"></a>Luglio 2006

La versione di SSMA per Sybase di luglio 2006 costituisce la versione iniziale.

## <a name="see-also"></a>Vedere anche

[Introduzione a SSMA per sybase &#40;SybaseToSQL&#41;](../../ssma/sybase/getting-started-with-ssma-for-sybase-sybasetosql.md)
