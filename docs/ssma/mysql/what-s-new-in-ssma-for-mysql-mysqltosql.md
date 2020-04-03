---
title: Novità di SSMA per MySQL (MySQLToSql) Documenti Microsoft
authors: HJToland3;nahk-ivanov
ms.prod: sql
ms.custom: ''
ms.date: 4/2/2020
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 1451a0b0-6713-4d0c-954f-ea3d8fce1d31
ms.author: jtoland;alexiva
ms.openlocfilehash: 9d5c33bbb9e09a5a833c928547a5ec659fe43c96
ms.sourcegitcommit: d818a307725983c921987749915fe1a381233d98
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/03/2020
ms.locfileid: "80625555"
---
# <a name="whats-new-in-ssma-for-mysql-mysqltosql"></a>Novità di SSMA per MySQL (MySQLToSql)

In questo articolo vengono elencate le modifiche di SQL Server Sql Server Migration Assistant (SSMA) per MySQL in ogni versione.

## <a name="ssma-v88"></a>SSMA v8.8

La versione v8.8 di SSMA per MySQL include:

* Miglioramenti alla stabilità della sincronizzazione degli oggetti di SQL ServerSQL Server objects synchronization stability improvements
* Miglioramenti delle prestazioni dell'interfaccia grafica durante la valutazione e la conversione

## <a name="ssma-v87"></a>SSMA v8.7

La versione v8.7 di SSMA per MySQL ha correzioni minori e miglioramenti delle prestazioni nell'interfaccia utente grafica.

Inoltre, SSMA per MySQL ora `LIMIT` fornisce la conversione per la clausola quando è destinata a SQL di Azure.In addition, SSMA for MySQL now provides conversion for clause when targeting Azure SQL.

> [!IMPORTANT]
> Con SSMA v8.5 e versioni successive, .NET 4.7.2 è un prerequisito per l'installazione. Se è necessario installare questa versione, è possibile scaricare il file di runtime da [qui](https://dotnet.microsoft.com/download/dotnet-framework/net472).

## <a name="ssma-v86"></a>SSMA v8.6

Oltre a un set mirato di correzioni progettate per migliorare l'usabilità e le prestazioni, la versione v8.6 di SSMA per MySQL è stata migliorata aggiungendo un'impostazione che consente agli utenti di omettere le proprietà estese SSMA nel codice convertito.

Per utilizzare questa impostazione, in SSMA per MySQL passare a **Strumenti** > **Impostazioni** > di progetto**Conversione****generale** > , quindi in **Varie**aggiornare il valore dell'impostazione **Omettere proprietà estese** su **Sì**.

![Omettere l'impostazione delle proprietà estese](../mysql/media/ssma-omit-extended-properties.png)

> [!IMPORTANT]
> Con SSMA v8.5 e versioni successive, .NET 4.7.2 è un prerequisito per l'installazione. Se è necessario installare questa versione, è possibile scaricare il file di runtime da [qui](https://dotnet.microsoft.com/download/dotnet-framework/net472).

## <a name="ssma-v85"></a>SSMA v8.5

La versione v8.5 di SSMA per MySQL è stata migliorata con il supporto per l'autenticazione di Azure Active Directory e il supporto di base per le funzionalità JSON nel server SQL, insieme a un set mirato di correzioni progettate per migliorare l'usabilità e le prestazioni.

> [!IMPORTANT]
> Con SSMA v8.5, .NET 4.7.2 è un prerequisito per l'installazione. Se è necessario installare questa versione, è possibile scaricare il file di runtime da [qui](https://dotnet.microsoft.com/download/dotnet-framework/net472).

## <a name="ssma-v84"></a>SSMA v8.4

La versione v8.4 di SSMA per MySQL è stata migliorata con correzioni mirate progettate per risolvere i problemi di accessibilità e correggere un bug relativo alle colonne di indice max (per consentire 32 anziché 16) per SQL Server 2016 e versioni successive.

> [!IMPORTANT]
> Con SSMA versioni 7.4 anche 8.4, .NET 4.5.2 è un prerequisito per l'installazione.

## <a name="ssma-v83"></a>SSMA v8.3

La versione v8.3 di SSMA per MySQL è stata migliorata con correzioni mirate progettate per migliorare la qualità e le metriche di conversione. Inoltre, questa versione di SSMA per MySQL fornisce correzioni che:In addition, this release of SSMA for MySQL provides fixes that:

* Risolvere i problemi di accessibilità.
* Aggiungere il `hierarchyid` supporto di base per il tipo in SQL Server.Add basic support for type in SQL Server.

## <a name="ssma-v82"></a>SSMA v8.2

La versione v8.2 di SSMA per MySQL è stata migliorata con un set mirato di correzioni progettate per migliorare la qualità e le metriche di conversione, nonché correzioni per:

* Problema con gli indici non cluster disabilitati dopo la migrazione dei dati.
* Rilevamento di .NET Framework durante l'installazione invisibile all'utente.
* Arresto anomalo intermittente che si verifica quando viene scaricata una nuova versione.

> [!NOTE]
> Un problema noto con l'aggiornamento automatico può causare l'errore di un aggiornamento da SSMA v8.1 a v8.2. Se si verifica questo errore, scaricare la nuova versione e installarla manualmente.

## <a name="ssma-v81"></a>SSMA v8.1

La versione v8.1 di SSMA per MySQL è stata migliorata con correzioni mirate progettate per migliorare la qualità e le metriche di conversione.

> [!NOTE]
> Un problema noto con l'aggiornamento automatico può causare l'errore di un aggiornamento da SSMA v8.0 a v8.1. Se si verifica questo errore, scaricare la nuova versione e installarla manualmente.

## <a name="ssma-v80"></a>SSMA v8.0

La versione v8.0 di SSMA per MySQL è stata migliorata con correzioni mirate progettate per migliorare la qualità e le metriche di conversione. Questa versione offre anche le seguenti nuove funzionalità:

* Supporto per **l'istanza gestita del database SQL** di Azure come destinazione. È ora possibile creare nuovi progetti destinati all'istanza gestita del database SQL di Azure:You can now create new projects targeting Azure SQL Database Managed Instance:

  ![Progetto SQL DB MI](../media/ssma-newproject-sqldbmi.png)

* Avviso **fix**post-conversione . Scopri di più [qui](https://blogs.msdn.microsoft.com/datamigration/2019/02/17/%20accelerate-your-oracle-migrations-with-new-machine-learning-capabilities-in-ssma/).

* Selezione preliminare di database/schema.

  Quando ci si connette all'origine, l'utente può ora selezionare database/schemi di interesse. Selezionando solo gli schemi che si prevede di eseguire la migrazione si risparmia tempo durante la connessione iniziale e migliorare le prestazioni complessive SSMA.

  ![Oggetti filtro SSMASSMA filter objects](../media/ssma-filter-objects.png)

## <a name="ssma-v710"></a>SSMA v7.10

La versione v7.10 di SSMA per MySQL contiene le seguenti modifiche:

* Correzioni mirate progettate per fornire ulteriori protezioni di sicurezza e privacy per soddisfare i cambiamenti nei requisiti globali.
* Correzione per la conversione di spazi tra il nome della funzione e l'elenco di argomenti.

## <a name="ssma-v79"></a>SSMA v7.9

La versione v7.9 di SSMA per MySQL contiene le seguenti modifiche:

* Correzioni mirate che migliorano la qualità e le metriche di conversione.
* Supporto parziale per la migrazione di tipi di dati spaziali da MySQL al database SQL di Azure.Partial support for migrating spatial data types from MySQL to Azure SQL Database.
* Supporto nella riga di comando SSMA per modificare il mapping dei tipi di dati e le preferenze di progetto.
* Supporto per la migrazione dei dati tramite SQL Server Integration Services (SSIS). Dopo aver convertito lo schema, è possibile creare un pacchetto SSIS utilizzando un'opzione del menu di scelta rapida.
* Anche la finestra di dialogo di connessione al database SQL di Azure in SSMA è stata modificata per specificare il nome completo del server. Nelle versioni precedenti di SSMA, il prefisso del database SQL di Azure doveva essere menzionato in modo esplicito all'interno delle impostazioni dei progetti.

## <a name="ssma-v78"></a>SSMA v7.8

La versione v7.8 di SSMA per MySQL contiene le seguenti modifiche:

* Modificare il mapping dei tipi evidenziato in Impostazioni progetto.
* Possibilità per gli utenti di disabilitare i dati di telemetria.

## <a name="ssma-v77"></a>SSMA v7.7

La versione v7.7 di SSMA per MySQL contiene le seguenti modifiche:

* SSMA per MySQL è stato migliorato con correzioni mirate che migliorano la qualità e le metriche di conversione.
* In base alla richiesta popolare, la versione a 32 bit di SSMA per MySQL è tornato. Rispetto all'implementazione precedente (prima della v7.4), esistono due pacchetti di installazione, ma non possono essere installati affiancati. Di conseguenza, è necessario scegliere la versione più appropriata in base ai componenti di connettività disponibili. È sempre preferibile utilizzare la versione a 64 bit, se possibile.
* SSMA per MySQL dispone ora della modalità di connessione della stringa di connessione ODBC, che consente di utilizzare qualsiasi driver ODBC di terze parti compatibile con MySQL.

## <a name="ssma-v76"></a>SSMA v7.6

La versione v7.6 di SSMA per MySQL è stata migliorata con correzioni mirate che migliorano la qualità e le metriche di conversione e con il supporto per SQL Server 2017 (anteprima pubblica). Il supporto per SQL Server 2017 in Windows e Linux è in anteprima pubblica e non deve essere usato per le migrazioni di produzione.

## <a name="ssma-v75"></a>SSMA v7.5

La versione v7.5 di SSMA per MySQL è stata migliorata con diversi miglioramenti per garantire una maggiore accessibilità per le persone con disabilità.

## <a name="ssma-v74"></a>SSMA v7.4

La versione v7.4 di SSMA per MySQL contiene le seguenti modifiche:

* L'opzione **Timeout query** è ora disponibile durante l'individuazione degli oggetti dello schema nell'origine e nella destinazione.

    ![opzione di timeout della query](../media/query-timeout_red.png)
* La metrica di qualità e conversione è stata migliorata con correzioni mirate, in base al feedback dei clienti.

> [!IMPORTANT]
> .NET 4.5.2 è un prerequisito per l'installazione di SSMA v7.4. Inoltre, a partire dalla v7.4, la versione a 32 bit di SSMA viene interrotta.

## <a name="ssma-v73"></a>SSMA v7.3

La versione v7.3 di SSMA per MySQL contiene le seguenti modifiche:

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

La versione v7.2 di SSMA per MySQL contiene le seguenti modifiche:

* Metriche di qualità e conversione migliorate con correzioni mirate in base al feedback dei clienti.
* Miglioramenti della telemetria per fornire punti dati migliori per risolvere i problemi dei clienti e migliorare i tassi di conversione di SSMA.

## <a name="ssma-v71"></a>SSMA v7.1

La versione v7.1 di SSMA per MySQL contiene le seguenti modifiche:

* SQL Server 2017 SQL su CTP1 di Windows e Linux è ora una piattaforma di destinazione supportata per la migrazione. Questa funzionalità è in anteprima tecnica e consente lo spostamento di schema e dati ai server SQL di destinazione.
* SSMA ora supporta gli aggiornamenti automatici per scaricare la versione più recente di SSMA non appena è disponibile.
* I file binari installabili SSMA vengono ora recapitati tramite i file del pacchetto di Windows Installer (MSI).

## <a name="may-2016"></a>Maggio 2016

La versione di maggio 2016 di SSMA per MySQL contiene le seguenti modifiche:

* Aggiunto il supporto per SQL Server 2016.Added support for SQL Server 2016.
* Parser e resolver migliorati.
* È stato rimosso il controllo del programma di installazione per .NET 2.0.Removed installer check for .NET 2.0.
* Dipendenza di Extension Pack aggiornata da .NET 3.5 a .NET 4.0.Updated Extension Pack dependency from .NET 3.5 to .NET 4.0.
* Corretto il mapping di tipo BigInt predefinito per MySql.Fixed default BigInt type mapping for MySql.
* Risolto `save-project` `open-project` e comandi per la console SSMA.
* Comando `securepassword` fisso per la console SSMA.
* Corretto il conteggio degli oggetti per il caricamento iniziale.
* Correzione del caricamento degli oggetti MsSql.
* Corretto bug nelle impostazioni globali.

## <a name="march-2016"></a>marzo 2016

La versione di anteprima di marzo 2016 di SSMA per MySQL aggiunge il supporto per la migrazione a SQL Server 2016.The March 2016 preview release of SSMA for MySQL adds support for migration to SQL Server 2016.
  
## <a name="january-2016"></a>Gennaio 2016

La versione di manutenzione di gennaio 2016 di SSMA per MySQL contiene le seguenti modifiche:

* Aggiunta voce di menu Visualizza registro a SSMA (RFC 5706203).
* Aggiunto Telemetria.
  
## <a name="july-2014"></a>Luglio 2014

La versione di luglio 2014 di SSMA per MySQL contiene le seguenti modifiche:
  
* Conversione del codice del database SQL di Azure migliorata.
* Funzionalità del pacchetto di estensione spostata nello schema per supportare il database SQL di Azure.Extension pack functionality moved to schema to support Azure SQL DB.
* Miglioramenti delle prestazioni testati per i database con oltre 10k oggetti.
* Miglioramenti dell'interfaccia utente per la gestione di un numero elevato di oggetti.
* Evidenziazione di schemi LOB noti (in modo che possano essere ignorati nella conversione).
* Miglioramenti della velocità di conversione.
* Mostra i conteggi degli oggetti nell'interfaccia utente.
* Riduzione delle dimensioni del rapporto di oltre il 25%.
* Messaggi di errore migliorati per i costrutti non analizzati.
  
## <a name="april-2014"></a>Aprile 2014

La versione di aprile 2014 di SSMA per MySQL contiene le seguenti modifiche:
  
* Aggiunto il supporto per SQL Server 2014.
* Corretti i bug relativi alla conversione in Azure.Fixed bugs regarding conversion to Azure.
* Corretti i bug relativi alle pagine di report invisibili in IE 10.
  
## <a name="july-2011"></a>luglio 2011

La versione di luglio 2011 di SSMA per MySQL contiene le seguenti modifiche:
  
* Supporto per `LIMIT` la [!INCLUDE [ssSQL11](../../includes/sssql11-md.md)] `OFFSET`conversione di .
* Segnalazione degli errori migliorata durante la migrazione dei dati.
  
## <a name="april-2011"></a>Aprile 2011

La versione di aprile 2011 di SSMA per MySQL contiene le seguenti modifiche:
  
* Singolo installabile di "SSMA for MySQL", che supporta [!INCLUDE [ssVersion2005](../../includes/ssversion2005-md.md)], [!INCLUDE [ssSQL10](../../includes/sssql10-md.md)]e [!INCLUDE [ssSQL11](../../includes/sssql11-md.md)] SQL di Azure.
* La possibilità [!INCLUDE [ssSQL11](../../includes/sssql11-md.md)]di connettersi .
* Motore di migrazione dei dati lato client migliorato, che supporta la migrazione parallela dei dati.
* Miglioramento delle prestazioni di migrazione dei dati con i modelli di recupero con registrazione semplice e con registrazione bulk.
* SSMA per la versione di MySQL Console supporta la compatibilità con le versioni precedenti. È possibile aprire i progetti creati da versioni precedenti a SSMA v5.0.You can open the projects created by versions earlier to SSMA v5.0.
* SSMA per il prodotto MySQL v5.0 può essere installato side-by-side (SxS) con le versioni precedenti del prodotto SSMA.
  
## <a name="july-2010"></a>Luglio 2010

La versione di luglio 2010 di SSMA per MySQL contiene le seguenti funzionalità:
  
**1. Miglioramenti all'interfaccia utente:**

* Scheda 'Modalità SQL' per gli oggetti di database MySQL
* Scheda 'Impostazioni' per gli oggetti MySQL Database
* Scheda 'Dati' per le tabelle MySQL
* Impostazioni di progetto aggiornate nelle pagine di conversione e migrazione
* 'Impostazioni di migrazione dei dati' a livello di tabella
  
**2. Miglioramenti alla connessione a MySQL e SQL Server:**
  
* Connettività SSL in MySQL
* Connettività crittografata in SQL ServerEncrypted Connectivity in SQL Server
  
**3. Miglioramenti a MySQL Metabase Explorer:**
  
* Caricamento di tutti gli oggetti di database MySQL e le rispettive schede.
  
**4. Miglioramenti alla conversione degli oggetti:**
  
* Conversione di oggetti della metabase MySQL: procedure, funzioni, viste, trigger e istruzioni.
* Supporto limitato per i tipi di dati spaziali nelle tabelle.
* Opzione per convertire le funzioni MySQL in stored procedure di SQL ServerOption to convert MySQL functions to SQL Server Stored Procedures
* Opzione per applicare le modalità SQL e il mapping del set di caratteri durante la conversione degli oggettiOption to apply SQL Modes and Charset mapping during Object Conversion
  
**5. Miglioramenti alla migrazione dei dati:**  
  
* Supporto per la migrazione dei dati tramite motori di migrazione dei dati lato server e lato clientSupport for Data Migration Engine both Server-Side Data Migration Engines
* Supporto per la migrazione dei dati spazialiSupport for Spatial Data Migration
* SQL personalizzato per la migrazione dei dati per le tabelleCustom SQL for Data Migration for Tables
  
**6. SSMA per MySQL Console:**  
  
* Funzionalità della console di supporto per SSMA per MySQLSupport Console Feature for SSMA for MySQL  
* Supporto per l'interfacing a livello di scriptSupport for Script-Level Interfacing  
  
## <a name="january-2010"></a>Gennaio 2010

La versione di gennaio 2010 di SSMA per MySQL è stata la versione iniziale. Conteneva le seguenti caratteristiche:
  
* Aggiunto il supporto per la migrazione a SQL Server locale e SQL di Azure.Added support for migration to both on-premises SQL Server and Azure SQL.  
  
* **Istantanea della funzione:** Migrazione di schemi e dati di tabelle/indici/vincoli MySQL.Schema and Data migration of MySQL Tables/Indexes/Constraints.
