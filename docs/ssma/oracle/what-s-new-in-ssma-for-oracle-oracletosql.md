---
title: Quali sono le novità di SSMA per Oracle (OracleToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 03/06/2019
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: f305ebb6-7393-4a43-abb3-6332b739d690
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 1d28ddc0ca3338c9f3a5f8e9e912efa90f6cbcfa
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63011891"
---
# <a name="whats-new-in-ssma-for-oracle-oracletosql"></a>Quali sono le novità di SSMA per Oracle (OracleToSQL)
Questo articolo elenca SQL Server Migration Assistant (SSMA) per le modifiche di Oracle in ogni versione.

## <a name="ssma-v81"></a>SSMA v8.1
La versione v8.1 di SSMA per Oracle è stata migliorata con correzioni mirate che sono progettate per migliorare le metriche di qualità e la conversione.

> [!NOTE]
> Un problema noto con l'aggiornamento automatico potrebbe essere il guasto di un aggiornamento dalla versione 8.0 SSMA per v8.1. Se si verifica questo errore,. scaricare la nuova versione e installarlo manualmente.

> [!IMPORTANT]
> Con v7.4 SSMA e versioni successive, .net 4.5.2 è un prerequisito di installazione.

## <a name="ssma-v80"></a>SSMA v8.0
La versione 8.0 di SSMA per Oracle è stata migliorata con correzioni mirate progettate per migliorare la qualità e la conversione delle metriche. Questa versione offre anche le nuove funzionalità seguenti:

* Supporto per **istanza gestita di Azure SQL Database** come destinazione. È ora possibile creare nuovi progetti destinati a istanza gestita di Azure SQL Database:

  ![Progetto di database SQL istanza Gestita](../media/ssma-newproject-sqldbmi.png)

    > [!NOTE]
    > SSMA per Oracle Extension Pack è stato inoltre aggiornato per consentire le installazioni remote nell'istanza gestita di Azure SQL Database:
    >
    > ![SSMA per Oracle Extension Pack](../media/ssma-oracle-ext-pack.png)

    Alcune funzionalità, tra cui la migrazione dei dati lato Server e i Tester, non sono supportati quando la destinazione di istanza gestita di Azure SQL Database. Altre informazioni, vedere [qui](https://blogs.msdn.microsoft.com/datamigration/2019/02/17/migrate-your-oracle-database-to-azure-sql-database-managed-instance-using-ssma-8-0/).

*   Post-conversione **correzione advisor**. Come descritto in dettaglio [qui](https://blogs.msdn.microsoft.com/datamigration/2019/02/17/%20accelerate-your-oracle-migrations-with-new-machine-learning-capabilities-in-ssma/).

* Selezione database preliminare o nello schema.

    Quando ci si connette all'origine, l'utente può a questo punto selezionare i database/schemi di interesse. Selezionando solo gli schemi che si intende eseguire la migrazione verrà risparmiare tempo durante la connessione iniziale e migliorare le prestazioni complessive SSMA.

    ![Oggetti filtro SSMA](../media/ssma-filter-objects.png)

* La possibilità di usare il driver NET ufficiale, gestito per connettersi a Oracle. Il driver OCI non è più un prerequisito per l'uso di SQL Server Migration Assistant per Oracle.

* La possibilità di eseguire il mapping ROWID e UROWID in VARCHAR per impostazione predefinita. Modificato da 'uniqueidentifier' per supportare la migrazione dei dati per le colonne ROWID esplicitare.

## <a name="ssma-v710"></a>SSMA v7.10
La versione v7.10 di SSMA per Oracle include le seguenti modifiche:
- Correzioni mirate progettate per offrire maggiore sicurezza e protezione della privacy per soddisfare le modifiche nei requisiti globali.
- Un miglioramento di conversione relative alle query gerarchiche.

## <a name="ssma-v79"></a>SSMA v7.9
La versione v7.9 di SSMA per Oracle include le seguenti modifiche:
- Correzioni mirate che consentono di migliorare le metriche di qualità e la conversione.
- Supporto per le istruzioni "Continua" migrazione da Oracle a SQL Server.
- Supporto nella riga di comando SSMA per modificare il mapping dei tipi di dati e le preferenze del progetto.
- Supporto per la migrazione dei dati usando SQL Server Integration Services (SSIS). Dopo la conversione dello schema, è possibile creare un pacchetto SSIS usando un'opzione di menu di scelta rapida.
- Finestra di dialogo di connessione Database SQL di Azure in SSMA è stato modificato anche per specificare il nome completo del server. Nelle versioni precedenti di SSMA, il prefisso di Database SQL di Azure doveva essere indicato in modo esplicito all'interno delle impostazioni di progetti.

## <a name="ssma-v78"></a>SSMA v7.8
La versione v 7.8 di SSMA per Oracle include le seguenti modifiche:
-   Supporto per:
    - Espressione di riga per la clausola IN.
    - Cast di tipo implicito.
    - Conversione di UID per Database SQL di Azure.
- Modificare il mapping dei tipi evidenziate nelle impostazioni del progetto.
- La possibilità per gli utenti disabilitare la telemetria.

## <a name="ssma-v77"></a>SSMA v7.7
La versione v7.7 di SSMA per Oracle include le seguenti modifiche:
- SSMA per Oracle è stato migliorato con correzioni mirate che consentono di migliorare le metriche di qualità e la conversione.
- Basato su richiesta comune, la versione a 32 bit di SSMA per Oracle è nuovamente. Rispetto all'implementazione precedente (prima v7.4), sono disponibili due pacchetti di installazione, ma non possono essere installati side-by-side. Di conseguenza, è necessario scegliere la versione più appropriata in base ai componenti di connettività che si dispone. È sempre preferibile usare la versione a 64 bit, se possibile.
- SQL Server 2017 è ora il supporto ufficiale con il pacchetto di estensione di Oracle supportata anche in Linux (nuova opzione di installazione remota). Si noti che la funzionalità di pacchetto di estensioni è limitata durante l'installazione in Linux, come i tester e le funzionalità di migrazione dei dati lato server non sono supportate.
- SSMA per Oracle consente di eseguire la migrazione di viste materializzate sotto forma di tabelle regolari (può essere configurata tramite le impostazioni al **impostazioni del progetto** -> **sincronizzazione**  ->  **Individuare le tabelle sottostanti per le viste materializzate**).

## <a name="ssma-v76"></a>SSMA v7.6
La versione v7.6 di SSMA per Oracle è stata migliorata con correzioni mirate che consentono di migliorare le metriche di qualità e la conversione e con il supporto per SQL Server 2017 (anteprima pubblica). Supporto per SQL Server 2017 in Windows e Linux è disponibile in anteprima pubblica e non deve essere usato per le migrazioni di produzione.

## <a name="ssma-v75"></a>SSMA v7.5
La versione v7.5 di SSMA per Oracle include le seguenti modifiche:
- Migliorato con numerosi miglioramenti per assicurare maggiore accessibilità per persone affette da disabilità.
- Aggiornato per migliorare la metrica di qualità e la conversione con correzioni mirate, ad esempio Gestione migliorata di tipi di dati date e float durante la migrazione dei dati, in base ai suggerimenti dei clienti.

## <a name="ssma-v74"></a>SSMA v7.4
La versione v7.4 di SSMA per Oracle include le seguenti modifiche:

- SSMA per Oracle supporta ora Azure SQL Data Warehouse come piattaforma di destinazione per la migrazione.

    ![Finestra Nuovo progetto](../media/new-project.png)
  - Supporta le opzioni di archiviazione di Data Warehouse, come illustrato nell'immagine seguente:

    ![opzioni di archiviazione per data warehouse](../media/storage-options_red.png)
  - Supporta le opzioni di distribuzione dei dati, come illustrato nell'immagine seguente:

    ![distribuzione dei dati per data warehouse](../media/data-distribution_red.png)

- Il **timeout Query** opzione ora è disponibile durante l'individuazione di oggetti dello schema all'origine e destinazione.

    ![query timeout-opzione](../media/query-timeout_red.png)

- La metrica della qualità e la conversione è stata migliorata con correzioni mirate, ai suggerimenti dei clienti.

> [!IMPORTANT]
> .NET 4.5.2 è un prerequisito per l'installazione di SSMA v7.4. Inoltre, a partire da v7.4, la versione a 32 bit di SSMA verrà terminato a breve.

## <a name="ssma-v73"></a>SSMA v7.3
La versione v7.3 di SSMA per Oracle include le seguenti modifiche:
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
Il rilascio della versione 7.2 di SSMA per Oracle contiene le seguenti modifiche:
- Metrica qualità e conversione migliorata con correzioni mirate ai suggerimenti dei clienti.
- Miglioramenti della telemetria per fornire una migliore punti dati per risolvere i problemi dei clienti e migliorare il tasso di conversione di SSMA.

## <a name="ssma-v71"></a>SSMA v7.1
La versione 7.1 di SSMA per Oracle contiene le seguenti modifiche:
- A questo punto, SQL Server 2017 in Windows e Linux CTP1 è una piattaforma di destinazione supportate per la migrazione. Questa funzionalità è della versione technical preview e consente lo spostamento dei dati e lo schema per i server SQL di destinazione.
- SSMA supporta ora gli aggiornamenti automatici per scaricare la versione più recente di SSMA, non appena è disponibile.
- I file binari installabili SSMA vengono ora forniti tramite file del pacchetto Windows installer (MSI).

**Risorse**

[Estensione delle funzionalità di SQL Server Migration Assistant conversione](https://blogs.msdn.microsoft.com/datamigration/2017/02/21/2185/)

[Valutare e migrare i dati da piattaforme di dati non Microsoft per SQL Server *(con esempio di Oracle)*](https://blogs.msdn.microsoft.com/datamigration/2016/11/16/sql-server-migration-assistant-how-to-assess-and-migrate-databases-from-non-microsoft-data-platforms-to-sql-server/) 

## <a name="may-2016"></a>Maggio 2016  
La versione di maggio 2016 di SSMA per Oracle contiene le seguenti modifiche:  

- Aggiunta del supporto per SQL Server 2016.
- Aggiuntiva conversione di tabelle di archiviazione flashback Oracle nelle tabelle temporali di SQL Server.

    **Nota** -SSMA non copia i dati di cronologia dalle tabelle di archiviazione di dati Oracle Flashback. Di conseguenza, i dati di cronologia devono essere copiati manualmente durante il processo di migrazione. Inoltre, mentre SSMA non viene visualizzata la tabella di cronologia in Visualizzatore metadati SQL Server perché viene considerata come una tabella di sistema, è possibile visualizzare la tabella di cronologia in SQL Server Management Studio.
    SQL Server 2016 non supporta diverse funzionalità Flashback Oracle, tra cui:
    - Query di Oracle Flashback delle transazioni
    - Pacchetto DBMS_FLASHBACK
    - Flashback transazione
    - Flashback Data Archive
    - Flashback tabella
    - Flashback Drop
    - Flashback Database
- Aggiunta conversione di Oracle VPD criteri in oggetti Criteri di SQL Server (sicurezza a livello di riga per Oracle).
- Una riduzione tempo di caricamento iniziale per Oracle.
- Parser migliorata e sistema di risoluzione.
- Rimosso controllo programma di installazione per .net 2.0.
- Pacchetto di estensioni delle dipendenze aggiornato da .net 3.5 a .net 4.0.
- Risolto "Salva progetto" e "open project" comandi per la Console SSMA.
- Comando fissa "securepassword" per la Console SSMA.
- Risolto il conteggio degli oggetti per il caricamento iniziale.
- Correzione di conversione dei tipi di dati carattere per Oracle.
- Correzione del bug nelle impostazioni globali.
  
## <a name="march-2016"></a>Marzo 2016  
La versione di anteprima di marzo 2016 di SSMA per Oracle include le modifiche seguenti:  
  
-   Aggiunta del supporto per la migrazione a SQL Server 2016.  
-   Aggiunta del supporto per la migrazione sicurezza a livello di riga Oracle (con alcune limitazioni).  
-   Aggiunta del supporto per la migrazione di tabelle di Oracle in memoria per SQL Server colonna Store.  
  
## <a name="january-2016"></a>Gennaio 2016  
Gennaio 2014 versione di manutenzione di SSMA per Oracle include le seguenti modifiche:  
  
-   Aggiunta del supporto per gli indici cluster.  
-   Correzione di query di schema Oracle lenta (RFC 5076207).  
-   Fisso connettersi ad Azure dalla console.  
-   Voce di Menu Visualizza aggiunta Log per SSMA (RFC 5706203). 
-   Aggiunti i dati di telemetria.  
  
## <a name="july-2014"></a>Luglio 2014  
La versione di luglio 2014 di SSMA per Oracle contiene le seguenti modifiche:  
  
-   Aggiunta del supporto per database SQL di Azure.  
-   Estensione pack funzionalità spostata allo schema per supportare database SQL di Azure.  
-   Aggiunta del supporto per le viste materializzate Oracle.  
-   Le tabelle con ottimizzazione aggiunta del supporto per la memoria di SQL Server 2014.  
-   Miglioramenti delle prestazioni incluso testato per i database con oltre 10k oggetti.  
-   Aggiunti miglioramenti dell'interfaccia utente per la gestione con un numero elevato di oggetti.  
-   Aggiungere l'evidenziazione degli schemi LOB "noti".  
-   Inclusi i miglioramenti di velocità di conversione.  
-   Aggiunta del supporto per la visualizzazione oggetto conta nell'interfaccia utente.  
-   Dimensioni del report ridotta da più di 25%.
-   Messaggi di errore migliorati per i costrutti non analizzati.  
  
## <a name="april-2014"></a>Aprile 2014  
La versione di aprile 2014 di SSMA per Oracle contiene le seguenti modifiche:  
  
-   Aggiunta del supporto di Microsoft SQL Server 2014.  
-   Aggiunta del supporto di ottimizzazione 12 Oracle ed eseguire una query.  
-   Bug risolti riguardanti la conversione in Azure.  
-   Bug risolti relative alle pagine del report invisibile in Internet Explorer 10.  
  
## <a name="january-2012"></a>Gennaio 2012  
Aggiunge il supporto per tipo di riga per la versione di gennaio 2012 di SSMA per Oracle e i parametri di input RecordType automaticamente impostati su NULL.  
  
## <a name="july-2011"></a>Mese di luglio 2011  
La versione di luglio 2011 di SSMA per Oracle contiene le seguenti modifiche:  
  
-   Aggiunta del supporto per la conversione di sequenze di Oracle a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] generatore di sequenza "Denali".  
-   Migliore segnalazione errori durante la migrazione dei dati.  
-   Migliorata la conversione dell'istruzione tramite le parole riservate.  
-   Migliorata la conversione implicita del valore di data in una funzione.  
  
## <a name="april-2011"></a>Ad aprile 2011  
La versione aprile 2011 di SSMA per Oracle contiene le seguenti modifiche:  
  
-   Prodotto "SSMA per Oracle" consolidato, che supporta [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008 e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] "Denali".  
-   Aggiunta del supporto per la connessione e la migrazione a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] "Denali".  
-   Modulo di migrazione avanzata dei dati lato client, supporto per la migrazione parallela dei dati.  
-   Alle prestazioni della migrazione dei dati migliorate con semplici e operazioni Bulk registrate di modelli di recupero.  
-   Aggiunta del supporto per la compatibilità con le versioni precedenti dei progetti creati nelle versioni precedenti di SSMA (v4.0 e v4.2).  
-   Aggiunta la possibilità di installare SSMA per Oracle v5.0 prodotto affiancata (SxS) con le versioni precedenti di SSMA (v4.0 e v4.2).  
-   Aggiunta del supporto per tipi definiti dall'utente (include sottotipo, VARRAY, tabella nidificata, tabella oggetti e visualizzazione di oggetti) e i relativi utilizzi in blocchi PL/SQL con i messaggi di errore speciale di report.  

## <a name="july-2010"></a>Luglio 2010  
La versione di luglio 2010 di SSMA per Oracle contiene le seguenti modifiche:  
  
-   Aggiunta del supporto per la migrazione a SQL Server 2008 R2.  
-   Aggiungere una nuova applicazione Console SSMA per l'esecuzione della riga di comando.  
-   Aggiunta del supporto per la migrazione dei dati tramite motori di migrazione dei dati lato Client e lato Server.  
-   Aggiunta del supporto per l'istruzione "SELECT Custom" nella migrazione dei dati.  
-   Aggiunta del supporto per la migrazione da Oracle 11g R2.  
  
## <a name="june-2008"></a>Giugno 2008  
La versione di giugno 2008 di SSMA per Oracle contiene le seguenti modifiche:  
  
-   Aggiunti miglioramenti per il Report di valutazione, tra cui informazioni aggiuntive per i sinonimi, origine non elaborata di oggetti analizzabili, i pannelli e la rimozione del logo di SQL Server e persistenza del layout.  
-   Aggiunti miglioramenti nella conversione degli oggetti:  
    -   Pacchetti DBMS_LOB, conversione DBMS_SQL aggiunto.  
    -   Crea un join conversione rivista.  
    -   Modifica della conversione di record e le raccolte, a questo punto la conversione di record nei casi più semplici rilasciati tramite variabili separate per ogni campo.  
    -   Miglioramenti dell'implementazione di record e le raccolte.  
    -   Funzioni di aggregazione finestra aggiunte.  
    -   Clausola ROLLUP/CUBE aggiunto.  
    -   Analisi utilizzo software per NEXTVAL/CURVAL.  
    -   Sono state aggiunte colonne nella clausola SET di raggruppamento, Grouping sets e ID di raggruppamento.  
    -   Istruzione aggiunte di MERGE.  
    -   Supporto dei nuovi tipi datetime e conversione dei record e le raccolte come tipi di dati CLR aggiunti.  
-   Vengono aggiunte nuove funzioni di Tester. Le tabelle possono ora essere testate come oggetti usando Tester, un ordine di chiamata di diversi oggetti testabili nel test case può essere modificato, utente possono essere testati procedure e funzioni con i record e le raccolte come parametri e valori restituiti e uno strumento di analisi di dipendenze è stata aggiunta da controllare solo tabelle utilizzate.  
  
## <a name="august-2007"></a>Agosto 2007  
La versione di agosto 2007 di SSMA per Oracle contiene le seguenti modifiche:  
  
-   Aggiungere che un nuovo componente TESTER consente di creare, gestire ed eseguire test case per verificare il codice SQL convertito.  
-   Aggiunta del supporto per la conversione dei sottotipi, raccolte e moduli locali Oracle sono stati aggiunti al convertitore di tipi SQL.  
-   Aggiungere che una nuova funzionalità di sincronizzazione consente di sincronizzare oggetti specifici con database di SQL Server.  
-   Aggiunte nuove opzioni di conversione.  
  
## <a name="april-2007"></a>Aprile 2007  
La versione di aprile 2007 di SSMA per Oracle è la versione iniziale.
