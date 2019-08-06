---
title: Novità di SSMA per MySQL (MySQLToSql) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 07/31/2019
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 1451a0b0-6713-4d0c-954f-ea3d8fce1d31
author: HJToland3
ms.author: Shamikg
ms.openlocfilehash: d02b002dd5f974fa7fd989026172b70a049d0e5f
ms.sourcegitcommit: 495913aff230b504acd7477a1a07488338e779c6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/06/2019
ms.locfileid: "68811488"
---
# <a name="whats-new-in-ssma-for-mysql-mysqltosql"></a>Novità di SSMA per MySQL (MySQLToSql)

Questo articolo elenca SQL Server Migration Assistant (SSMA) per le modifiche di MySQL in ogni versione.

## <a name="ssma-v83"></a>SSMA v 8.3

La versione 8.3 di SSMA per MySQL è stata migliorata con correzioni mirate progettate per migliorare le metriche di qualità e conversione. Inoltre, questa versione di SSMA per MySQL fornisce le correzioni seguenti:

* Risolvere i problemi di accessibilità
* Aggiungere il supporto di base per il tipo ' hierarchyid ' in SQL Server

> [!IMPORTANT]
> Con SSMA v 7.4 e versioni successive, .NET 4.5.2 è un prerequisito di installazione.

## <a name="ssma-v82"></a>SSMA v8.2

La versione v 8.2 di SSMA per MySQL è stata migliorata con un set di correzioni mirato progettato per migliorare le metriche di qualità e conversione, nonché le correzioni per:

* Un problema con gli indici non cluster disabilitati dopo la migrazione dei dati.
* Rilevamento dei .NET Framework durante l'installazione invisibile all'utente.
* Arresti anomali intermittenti che si verifica quando viene scaricata una nuova versione.

> [!NOTE]
> Un problema noto relativo all'aggiornamento automatico può provocare l'errore di un aggiornamento da SSMA v 8.1 a v 8.2. Se si verifica questo errore, scaricare la nuova versione e installarla manualmente.

> [!IMPORTANT]
> Con SSMA v 7.4 e versioni successive, .NET 4.5.2 è un prerequisito di installazione.

## <a name="ssma-v81"></a>SSMA v8.1

La versione v 8.1 di SSMA per MySQL è stata migliorata con correzioni mirate progettate per migliorare la qualità e le metriche di conversione.

> [!NOTE]
> Un problema noto relativo all'aggiornamento automatico può provocare l'errore di un aggiornamento da SSMA v 8.0 a v 8.1. Se si verifica questo errore, scaricare la nuova versione e installarla manualmente.

## <a name="ssma-v80"></a>SSMA v8.0

La versione v 8.0 di SSMA per MySQL è stata migliorata con correzioni mirate progettate per migliorare la qualità e le metriche di conversione. Questa versione offre anche le seguenti nuove funzionalità:

* Supporto per **istanza gestita di database SQL di Azure** come destinazione. È ora possibile creare nuovi progetti destinati a Istanza gestita di database SQL di Azure:

  ![Progetto di database SQL MI](../media/ssma-newproject-sqldbmi.png)

* **Avviso di correzione**post-conversione. Altre informazioni sono disponibili [qui](https://blogs.msdn.microsoft.com/datamigration/2019/02/17/%20accelerate-your-oracle-migrations-with-new-machine-learning-capabilities-in-ssma/).

* Selezione dello schema o del database preliminare.

  Quando ci si connette all'origine, l'utente può ora selezionare database/schemi di interesse. Se si selezionano solo gli schemi di cui si intende eseguire la migrazione, si risparmia tempo durante la connessione iniziale e si migliorano le prestazioni complessive del SSMA.

  ![Oggetti filtro SSMA](../media/ssma-filter-objects.png)

## <a name="ssma-v710"></a>SSMA v7.10

La versione v 7.10 di SSMA per MySQL contiene le modifiche seguenti:

* Correzioni mirate progettate per fornire protezione aggiuntiva per la sicurezza e la privacy per soddisfare le modifiche nei requisiti globali.
* Correzione per la conversione di spazi tra il nome della funzione e l'elenco di argomenti.

## <a name="ssma-v79"></a>SSMA v7.9

La versione v 7.9 di SSMA per MySQL contiene le modifiche seguenti:

* Correzioni mirate che migliorano le metriche di qualità e conversione.
* Supporto parziale per la migrazione di tipi di dati spaziali da MySQL al database SQL di Azure.
* Supporto nella riga di comando di SSMA per modificare il mapping dei tipi di dati e le preferenze di progetto.
* Supporto per la migrazione dei dati tramite SQL Server Integration Services (SSIS). Dopo la conversione dello schema, è possibile creare un pacchetto SSIS utilizzando l'opzione del menu di scelta rapida.
* La finestra di dialogo di connessione del database SQL di Azure in SSMA è stata anche modificata per specificare il nome completo del server. Nelle versioni precedenti di SSMA, il prefisso del database SQL di Azure doveva essere indicato in modo esplicito all'interno delle impostazioni dei progetti.

## <a name="ssma-v78"></a>SSMA v7.8

La versione v 7.8 di SSMA per MySQL contiene le modifiche seguenti:

* Modificare il mapping dei tipi evidenziato nelle impostazioni del progetto.
* Possibilità per gli utenti di disabilitare la telemetria.

## <a name="ssma-v77"></a>SSMA v7.7

La versione v 7.7 di SSMA per MySQL contiene le modifiche seguenti:

* SSMA per MySQL è stato migliorato con correzioni mirate che migliorano la qualità e la metrica di conversione.
* In base alla richiesta più diffusa, la versione a 32 bit di SSMA per MySQL è di nuovo. Rispetto all'implementazione precedente (prima della versione 7.4), sono disponibili due pacchetti di installazione, ma non possono essere installati side-by-side. Di conseguenza, è necessario scegliere la versione più appropriata in base ai componenti di connettività disponibili. È sempre preferibile usare la versione a 64 bit, se possibile.
* SSMA per MySQL dispone ora della modalità di connessione della stringa di connessione ODBC, che consente di usare qualsiasi driver ODBC di terze parti compatibile con MySQL.

## <a name="ssma-v76"></a>SSMA v7.6

La versione 7.6 di SSMA per MySQL è stata migliorata con correzioni mirate che migliorano le metriche di qualità e conversione e con il supporto per SQL Server 2017 (anteprima pubblica). Il supporto per SQL Server 2017 in Windows e Linux è in versione di anteprima pubblica e non deve essere usato per le migrazioni di produzione.

## <a name="ssma-v75"></a>SSMA v7.5

La versione v 7.5 di SSMA per MySQL è stata migliorata con diversi miglioramenti per garantire una maggiore accessibilità per gli utenti con particolari esigenze.

## <a name="ssma-v74"></a>SSMA v7.4

La versione v 7.4 di SSMA per MySQL contiene le modifiche seguenti:

* L'opzione **query timeout** è ora disponibile durante l'individuazione di oggetti dello schema all'origine e alla destinazione.

    ![query timeout-opzione](../media/query-timeout_red.png)
* La metrica relativa alla qualità e alla conversione è stata migliorata con correzioni mirate, basate sui suggerimenti dei clienti.

> [!IMPORTANT]
> .NET 4.5.2 è un prerequisito per l'installazione di SSMA v 7.4. Inoltre, a partire da v 7.4, la versione a 32 bit di SSMA viene sospesa.

## <a name="ssma-v73"></a>SSMA v7.3

La versione v 7.3 di SSMA per MySQL contiene le modifiche seguenti:

* Miglioramento della qualità e della metrica di conversione con correzioni mirate basate sui suggerimenti dei clienti.
* SSMA Extensibility Framework esposto tramite gli elementi seguenti:
  * Esporta la funzionalità in un progetto di SQL Server Data Tools (SSDT).
    * È ora possibile esportare gli script dello schema da SSMA a un progetto SSDT. È possibile utilizzare gli script dello schema per apportare ulteriori modifiche allo schema e distribuire il database.

      ![Comando Salva come progetto SSDT](../media/export-schema-scripts_red.png)
  * Librerie che possono essere utilizzate da SSMA per l'esecuzione di conversioni personalizzate.
    * È ora possibile costruire codice in grado di gestire le conversioni e le conversioni di sintassi personalizzate che non sono state precedentemente gestite da SSMA.
      * In questo post di Blog sono disponibili istruzioni per la creazione di un convertitore personalizzato, che [estende le funzionalità di conversione di SQL Server Migration Assistant](https://blogs.msdn.microsoft.com/datamigration/2017/02/21/2185/).
      * Scaricare un progetto di esempio per la conversione da questo [post di Blog](https://blogs.msdn.microsoft.com/datamigration/ssmafororacleconversionsample/).

## <a name="ssma-v72"></a>SSMA v7.2

La versione 7.2 di SSMA per MySQL contiene le modifiche seguenti:

* Miglioramento della qualità e della metrica di conversione con correzioni mirate basate sui suggerimenti dei clienti.
* Miglioramenti della telemetria per fornire punti dati migliori per la risoluzione dei problemi dei clienti e per migliorare i tassi di conversione di SSMA.

## <a name="ssma-v71"></a>SSMA v7.1

La versione v 7.1 di SSMA per MySQL contiene le modifiche seguenti:

* SQL Server 2017 in Windows e Linux CTP1 è ora una piattaforma di destinazione supportata per la migrazione. Questa funzionalità è in anteprima tecnica e consente lo spostamento dello schema e dei dati per i server SQL di destinazione.
* SSMA supporta ora gli aggiornamenti automatici per scaricare la versione più recente di SSMA non appena disponibile.
* I file binari installabili di SSMA vengono ora recapitati tramite i file del pacchetto di Windows Installer (MSI).

## <a name="may-2016"></a>Maggio 2016  
La versione 2016 di SSMA per MySQL contiene le modifiche seguenti:

* Aggiunta del supporto per SQL Server 2016.
* Migliorato parser e resolver.
* Controllo del programma di installazione rimosso per .NET 2,0.
* La dipendenza del pacchetto di estensione è stata aggiornata da .NET 3,5 a .NET 4,0.
* Correzione del mapping dei tipi BigInt predefiniti per MySql.
* Corretti i comandi "Salva progetto" e "Apri progetto" per la console SSMA.
* Correzione del comando "SecurePassword" per la console di SSMA.
* Correzione del conteggio degli oggetti per il caricamento iniziale.
* Caricamento degli oggetti MsSql corretti.
* Correzione del bug nelle impostazioni globali.

## <a name="march-2016"></a>marzo 2016

La versione di anteprima di marzo 2016 di SSMA per MySQL aggiunge il supporto per la migrazione a SQL Server 2016. 
  
## <a name="january-2016"></a>2016 gennaio

La versione di manutenzione di SSMA per MySQL di gennaio 2016 contiene le modifiche seguenti:  

* Aggiunta voce di menu Visualizza log a SSMA (RFC 5706203).  
* Aggiunta di dati di telemetria.  
  
## <a name="july-2014"></a>2014 luglio

La versione luglio 2014 di SSMA per MySQL contiene le modifiche seguenti:  
  
* Conversione del codice del database SQL di Azure migliorata. 
* Funzionalità del pacchetto di estensione spostata nello schema per supportare il database SQL di Azure.  
* Miglioramenti delle prestazioni testati per i database con oltre 10.000 oggetti.  
* Miglioramenti dell'interfaccia utente per la gestione di un numero elevato di oggetti.  
* Evidenziazione degli schemi LOB "noti" (in modo che possano essere ignorati nella conversione).  
* Miglioramenti della velocità di conversione.  
* Mostra i conteggi degli oggetti nell'interfaccia utente.  
* Riduzione delle dimensioni del report superiore al 25%.  
* Messaggi di errore migliorati per costrutti non analizzati.  
  
## <a name="april-2014"></a>Aprile 2014

La versione April 2014 di SSMA per MySQL contiene le modifiche seguenti:  
  
* Aggiunta del supporto per MS SQL Server 2014.  
* Correzione dei bug relativi alla conversione in Azure  
* Correzione dei bug relativi alle pagine del report invisibile in IE 10.  
  
## <a name="july-2011"></a>2011 luglio

La versione luglio 2011 di SSMA per MySQL contiene le modifiche seguenti:  
  
* Supporto per la conversione del limite [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nell'offset di "Denali".  
* Segnalazione errori migliorata durante la migrazione dei dati.  
  
## <a name="april-2011"></a>Aprile 2011

La versione April 2011 di SSMA per MySQL contiene le modifiche seguenti:  
  
* Singolo installabile di "SSMA per MySQL", che supporta [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] "Denali" e Azure SQL.  
* La possibilità di connettere [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] "Denali".  
* Motore di migrazione dei dati avanzato sul lato client, che supporta la migrazione parallela dei dati.  
* Miglioramento delle prestazioni di migrazione dei dati con modelli di recupero con registrazione minima  
* SSMA per la versione della console MySQL supporta la compatibilità con le versioni precedenti. È possibile aprire i progetti creati dalle versioni precedenti a SSMA v 5.0.  
* Il prodotto SSMA per MySQL v 5.0 può essere installato side-by-Side (SxS) con le versioni precedenti del prodotto SSMA.  
  
## <a name="july-2010"></a>2010 luglio

La versione July 2010 di SSMA per MySQL contiene le funzionalità seguenti:  
  
1. **Miglioramenti dell'interfaccia utente:**  
  
    * Scheda ' modalità SQL ' per oggetti di database MySQL  
    * Scheda ' impostazioni ' per oggetti di database MySQL  
    * Scheda ' dati ' per le tabelle MySQL  
    * Impostazioni di progetto aggiornate nelle pagine di conversione e migrazione  
    * ' Impostazioni migrazione dati ' a livello di tabella  
  
2. **Miglioramenti per la connessione a MySQL e SQL Server:**  
  
    * Connettività SSL in MySQL  
    * Connettività crittografata in SQL Server  
  
3. **Miglioramenti a MySQL Metabase Explorer:**  
  
    * Caricamento di tutti gli oggetti di database MySQL e delle rispettive schede.  
  
4. **Miglioramenti alla conversione degli oggetti:**
  
    * Conversione di oggetti della metabase di MySQL: procedure, funzioni, viste, trigger e istruzioni.  
    * Supporto limitato per i tipi di dati spaziali nelle tabelle.
    * Opzione per la conversione di funzioni MySQL in SQL Server stored procedure  
    * Opzione per applicare le modalità SQL e il mapping del set di caratteri durante la conversione dell'oggetto  
  
5. **Miglioramenti alla migrazione dei dati:**  
  
    * Supporto per la migrazione dei dati tramite motori di migrazione dei dati lato server e lato client  
    * Supporto per la migrazione dei dati spaziali  
    * SQL personalizzato per la migrazione dei dati per le tabelle  
  
6. **SSMA per la console MySQL:**  
  
    * Funzionalità della console di supporto per SSMA per MySQL  
    * Supporto per l'interazione a livello di script  
  
## <a name="january-2010"></a>2010 gennaio

La versione di SSMA per MySQL di gennaio 2010 è stata la versione iniziale. Contiene le funzionalità seguenti: 
  
* È stato aggiunto il supporto per la migrazione sia alla SQL Server locale che a SQL di Azure.  
  
* **Snapshot funzionalità:** Migrazione dello schema e dei dati di tabelle/indici/vincoli MySQL.
