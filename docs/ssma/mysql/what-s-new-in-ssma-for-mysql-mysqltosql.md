---
title: Novità in SSMA per MySQL (MySQLToSql) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 03/06/2019
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 1451a0b0-6713-4d0c-954f-ea3d8fce1d31
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 0b87a9604af788158f774ca31a1ed6f4283e4c91
ms.sourcegitcommit: d7ed341b2c635dcdd6b0f5f4751bb919a75a6dfe
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/06/2019
ms.locfileid: "57527034"
---
# <a name="whats-new-in-ssma-for-mysql-mysqltosql"></a>Novità di SSMA per MySQL (MySQLToSql)
Questo articolo elenca SQL Server Migration Assistant (SSMA) per le modifiche di MySQL in ogni versione.

## <a name="ssma-v81"></a>SSMA v8.1
La versione v8.1 di SSMA per MySQL è stata migliorata con correzioni mirate che sono progettate per migliorare le metriche di qualità e la conversione.

> [!NOTE]
> Un problema noto con l'aggiornamento automatico potrebbe essere il guasto di un aggiornamento dalla versione 8.0 SSMA per v8.1. Se si verifica questo errore,. scaricare la nuova versione e installarlo manualmente.

> [!IMPORTANT]
> Con v7.4 SSMA e versioni successive, .net 4.5.2 è un prerequisito di installazione.

## <a name="ssma-v80"></a>SSMA v8.0
La versione 8.0 di SSMA per MySQL è stata migliorata con correzioni mirate progettate per migliorare la qualità e la conversione delle metriche. Questa versione offre anche le nuove funzionalità seguenti:

* Supporto per **istanza gestita di Azure SQL Database** come destinazione. È ora possibile creare nuovi progetti destinati a istanza gestita di Azure SQL Database:

    ![Progetto di database SQL istanza Gestita](../media/ssma-newproject-sqldbmi.png)

*   Post-conversione **correzione advisor**. Come descritto in dettaglio [qui](https://blogs.msdn.microsoft.com/datamigration/2019/02/17/%20accelerate-your-oracle-migrations-with-new-machine-learning-capabilities-in-ssma/).

*   Selezione database preliminare o nello schema.

    Quando ci si connette all'origine, l'utente può a questo punto selezionare i database/schemi di interesse. Selezionando solo gli schemi che si intende eseguire la migrazione verrà risparmiare tempo durante la connessione iniziale e migliorare le prestazioni complessive SSMA.

    ![Oggetti filtro SSMA](../media/ssma-filter-objects.png)

## <a name="ssma-v710"></a>SSMA v7.10
La versione v7.10 di SSMA per MySQL contiene le seguenti modifiche:
- Correzioni mirate progettate per offrire maggiore sicurezza e protezione della privacy per soddisfare le modifiche nei requisiti globali.
- Una correzione per la conversione degli spazi tra elenco nome e gli argomenti della funzione.

## <a name="ssma-v79"></a>SSMA v7.9
La versione v7.9 di SSMA per MySQL contiene le seguenti modifiche:
- Correzioni mirate che consentono di migliorare le metriche di qualità e la conversione.
- Supporto parziale per la migrazione dei tipi di dati spaziali da MySQL a Database SQL di Azure.
- Supporto nella riga di comando SSMA per modificare il mapping dei tipi di dati e le preferenze del progetto.
- Supporto per la migrazione dei dati usando SQL Server Integration Services (SSIS). Dopo la conversione dello schema, è possibile creare un pacchetto SSIS usando un'opzione di menu di scelta rapida.
- Finestra di dialogo di connessione Database SQL di Azure in SSMA è stato modificato anche per specificare il nome completo del server. Nelle versioni precedenti di SSMA, il prefisso di Database SQL di Azure doveva essere indicato in modo esplicito all'interno delle impostazioni di progetti.

## <a name="ssma-v78"></a>SSMA v7.8
La versione di v 7.8 di SSMA per MySQL contiene le seguenti modifiche:
- Modificare il mapping dei tipi evidenziate nelle impostazioni del progetto.
- La possibilità per gli utenti disabilitare la telemetria.

## <a name="ssma-v77"></a>SSMA v7.7
La versione v7.7 di SSMA per MySQL contiene le seguenti modifiche:
- SSMA per MySQL è stata migliorata con correzioni mirate che consentono di migliorare le metriche di qualità e la conversione.
- Basato su richiesta comune, la versione a 32 bit di SSMA per MySQL è nuovamente. Rispetto all'implementazione precedente (prima v7.4), sono disponibili due pacchetti di installazione, ma non possono essere installati side-by-side. Di conseguenza, è necessario scegliere la versione più appropriata in base ai componenti di connettività che si dispone. È sempre preferibile usare la versione a 64 bit, se possibile.
- SSMA per MySQL dispone ora di modalità di connessione per la stringa di connessione ODBC, che consente di usare tutti i driver ODBC di terze parti compatibili con MySQL.

## <a name="ssma-v76"></a>SSMA v7.6
La versione v7.6 di SSMA per MySQL è stata migliorata con correzioni mirate che consentono di migliorare le metriche di qualità e la conversione e con il supporto per SQL Server 2017 (anteprima pubblica). Supporto per SQL Server 2017 in Windows e Linux è disponibile in anteprima pubblica e non deve essere usato per le migrazioni di produzione.

## <a name="ssma-v75"></a>SSMA v7.5
La versione v7.5 di SSMA per MySQL è stata migliorata con numerosi miglioramenti per assicurare maggiore accessibilità per persone affette da disabilità.

## <a name="ssma-v74"></a>SSMA v7.4
La versione v7.4 di SSMA per MySQL contiene le seguenti modifiche:
- Il **timeout Query** opzione ora è disponibile durante l'individuazione di oggetti dello schema all'origine e destinazione.

    ![query timeout-opzione](../media/query-timeout_red.png)
- La metrica della qualità e la conversione è stata migliorata con correzioni mirate, ai suggerimenti dei clienti.

> [!IMPORTANT]
> .NET 4.5.2 è un prerequisito per l'installazione di SSMA v7.4. Inoltre, a partire da v7.4, la versione a 32 bit di SSMA verrà terminato a breve.

## <a name="ssma-v73"></a>SSMA v7.3
La versione v7.3 di SSMA per MySQL contiene le seguenti modifiche:
- Metrica qualità e conversione migliorata con correzioni mirate ai suggerimenti dei clienti.
- Framework di estendibilità SSMA esposta tramite gli elementi seguenti:
  - La funzionalità di esportazione in un progetto di SQL Server Data Tools (SSDT).
    -   È ora possibile esportare gli script dello schema da SSMA per un progetto di SSDT. È possibile utilizzare gli script dello schema per apportare ulteriori modifiche dello schema e distribuire il database.

        ![Salva come comando di progetto SSDT](../media/export-schema-scripts_red.png)
  - Librerie che possono essere usate da SSMA per l'esecuzione di conversioni personalizzate.
    - È ora possibile creare codice in grado di gestire le conversioni di sintassi personalizzata e che non sono stati precedentemente gestiti da SSMA.
      - Le istruzioni su come costruire un convertitore personalizzato sono disponibili in questo post di blog [funzionalità di conversione di estensione di SQL Server Migration Assistant](https://blogs.msdn.microsoft.com/datamigration/2017/02/21/2185/).
      - Scaricare un progetto di esempio per la conversione da questo [post di blog](https://blogs.msdn.microsoft.com/datamigration/ssmafororacleconversionsample/).

## <a name="ssma-v72"></a>SSMA v7.2
La versione di versione 7.2 di SSMA per MySQL contiene le seguenti modifiche:
- Metrica qualità e conversione migliorata con correzioni mirate ai suggerimenti dei clienti.
- Miglioramenti della telemetria per fornire una migliore punti dati per risolvere i problemi dei clienti e migliorare il tasso di conversione di SSMA.

## <a name="ssma-v71"></a>SSMA v7.1
La versione 7.1 di SSMA per MySQL contiene le seguenti modifiche:
- A questo punto, SQL Server 2017 in Windows e Linux CTP1 è una piattaforma di destinazione supportate per la migrazione. Questa funzionalità è della versione technical preview e consente lo spostamento dei dati e lo schema per i server SQL di destinazione.
- SSMA supporta ora gli aggiornamenti automatici per scaricare la versione più recente di SSMA, non appena è disponibile.
- I file binari installabili SSMA vengono ora forniti tramite file del pacchetto Windows installer (MSI).

**Risorse**

[Estensione delle funzionalità di SQL Server Migration Assistant conversione](https://blogs.msdn.microsoft.com/datamigration/2017/02/21/2185/)

[Valutare e migrare i dati da piattaforme di dati non Microsoft per SQL Server *(con esempio di Oracle)*](https://blogs.msdn.microsoft.com/datamigration/2016/11/16/sql-server-migration-assistant-how-to-assess-and-migrate-databases-from-non-microsoft-data-platforms-to-sql-server/) 

## <a name="may-2016"></a>Maggio 2016  
La versione di maggio 2016 di SSMA per MySQL contiene le seguenti modifiche:

-  Aggiunta del supporto per SQL Server 2016.
-  Parser migliorata e sistema di risoluzione.
-  Rimosso controllo programma di installazione per .net 2.0.
-  Pacchetto di estensioni delle dipendenze aggiornato da .net 3.5 a .net 4.0.
-  Mapping dei tipi BigInt fisso predefinito per MySql.
-  Risolto "Salva progetto" e "open project" comandi per la Console SSMA.
-  Comando fissa "securepassword" per la Console SSMA.
-  Risolto il conteggio degli oggetti per il caricamento iniziale.
-  Il caricamento di oggetti MsSql fissi.
-  Correzione del bug nelle impostazioni globali.
 
## <a name="march-2016"></a>Marzo 2016  
La versione di anteprima di marzo 2016 di SSMA per MySQL aggiunge il supporto per la migrazione a SQL Server 2016. 
  
## <a name="january-2016"></a>Gennaio 2016  
La versione di gennaio 2016 la manutenzione di SSMA per MySQL contiene le seguenti modifiche:  

-  Voce di Menu Visualizza aggiunta Log per SSMA (RFC 5706203).  
-  Aggiunti i dati di telemetria.  
  
## <a name="july-2014"></a>Luglio 2014  
La versione di luglio 2014 di SSMA per MySQL contiene le seguenti modifiche:  
  
-  Conversione del codice di Azure SQL DB migliorata. 
-  Estensione pack funzionalità spostata allo schema per supportare database SQL di Azure.  
-  Miglioramenti delle prestazioni testate per i database con oltre 10k oggetti.  
-  Miglioramenti dell'interfaccia utente per la gestione con un numero elevato di oggetti.  
-  L'evidenziazione degli schemi LOB "noti" (in modo che possono essere ignorati nella conversione).  
-  Miglioramenti di velocità di conversione.  
-  Visualizzare conteggi oggetti nell'interfaccia utente.  
-  Riduzione delle dimensioni dei report da più di 25%.  
-  Messaggi di errore migliorati per i costrutti non analizzati.  
  
## <a name="april-2014"></a>Aprile 2014  
La versione di luglio 2011 di SSMA per MySQL contiene le seguenti modifiche:  
  
-  Aggiunta del supporto di Microsoft SQL Server 2014.  
-  Bug risolti riguardanti la conversione in Azure  
-  Bug risolti relative alle pagine del report invisibile in Internet Explorer 10.  
  
## <a name="july-2011"></a>Mese di luglio 2011  
La versione di luglio 2011 di SSMA per MySQL contiene le seguenti modifiche:  
  
-   Supporto per la conversione del limite a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] OFFSET "Denali".  
-   Migliore segnalazione errori durante la migrazione dei dati.  
  
## <a name="april-2011"></a>Ad aprile 2011  
La versione di aprile 2011 di SSMA per MySQL contiene le seguenti modifiche:  
  
-   Singolo installabile "SSMA per MySQL", che supporta [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] "Denali" e SQL di Azure.  
-   La possibilità di connettersi [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] "Denali".  
-   Modulo di migrazione avanzata dei dati lato client, supporto per la migrazione parallela dei dati.  
-   Alle prestazioni della migrazione dei dati migliorate con semplici e operazioni Bulk registrate di modelli di recupero.  
-   SSMA per la versione della MySQL Console supporta la compatibilità con le versioni precedenti. È possibile aprire i progetti creati nelle versioni precedenti a v5.0 SSMA.  
-   SSMA per MySQL v5.0 prodotto può essere installata affiancata (SxS) con le versioni precedenti del prodotto SSMA.  
  
## <a name="july-2010"></a>Luglio 2010  
La versione di luglio 2010 di SSMA per MySQL contiene le funzionalità seguenti:  
  
1.  **Miglioramenti all'interfaccia utente:**  
  
    -   Scheda 'Modalità SQL' per gli oggetti di MySQL Database  
    -   Scheda 'Impostazioni' per gli oggetti di MySQL Database  
    -   Scheda 'Data' per le tabelle di MySQL  
    -   Impostazioni di progetto aggiornato nelle pagine di migrazione e conversione  
    -   'Impostazioni di migrazione dati' a livello di tabella  
  
2.  **Miglioramenti per la connessione a MySQL e SQL Server:**  
  
    -   Connettività SSL in MySQL  
    -   Connettività crittografata in SQL Server  
  
3.  **Miglioramenti alla Metabase MySQL Explorer:**  
  
    -   Il caricamento di tutti gli oggetti di Database MySQL e le rispettive schede.  
  
4.  **Miglioramenti per la conversione dell'oggetto:**  
  
    -   Conversione di oggetti della MySQL Metabase - procedure, funzioni, viste, trigger e le istruzioni.  
    -   Supporto limitato per i tipi di dati spaziali in tabelle.  
    -   Opzione per convertire le funzioni di MySQL in Stored procedure di SQL Server  
    -   Opzione per applicare il mapping di modalità SQL e set di caratteri durante la conversione degli oggetti  
  
5.  **Miglioramenti alla migrazione dei dati:**  
  
    -   Supporto per la migrazione dei dati tramite motori di migrazione dei dati lato Client e lato Server  
    -   Supporto per la migrazione di dati spaziali  
    -   SQL personalizzato per la migrazione dei dati per le tabelle  
  
6.  **SSMA per la Console MySQL:**  
  
    -   Supporto di funzionalità della Console di SSMA per MySQL  
    -   Supporto per l'interfaccia di livello dello Script  
  
## <a name="january-2010"></a>Gennaio 2010  
La versione di gennaio 2010 di SSMA per MySQL è la versione iniziale. Contiene le funzionalità seguenti: 
  
-   Aggiunta del supporto per la migrazione sia on-premises SQL Server e SQL di Azure.  
  
-   **Funzionalità Snapshot:** Migrazione dello schema e dati di tabelle/indici o vincoli di MySQL.
