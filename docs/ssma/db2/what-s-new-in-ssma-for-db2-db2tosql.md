---
title: Quali sono le novità di SSMA per DB2 (DB2ToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 02/27/2019
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 1cc38f85-3caa-42d0-8c76-a380c1d15c67
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 0254f57e5c653c68762159c7e51e71e70fa5fcd2
ms.sourcegitcommit: 2ab79765e51913f1df6410f0cd56bf2a13221f37
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/27/2019
ms.locfileid: "56955892"
---
# <a name="whats-new-in-ssma-for-db2-db2tosql"></a>Quali sono le novità di SSMA per DB2 (DB2ToSQL)
Questo articolo elenca SQL Server Migration Assistant (SSMA) per le modifiche di DB2 in ogni versione.

## <a name="ssma-v80"></a>SSMA v8.0
La versione 8.0 di SSMA per DB2 è stata migliorata per fornire correzioni mirate progettate per migliorare la qualità e la conversione delle metriche. Questa versione offre anche le nuove funzionalità seguenti:

* Supporto per **istanza gestita di Azure SQL Database** come destinazione. È ora possibile creare nuovi progetti destinati a istanza gestita di Azure SQL Database:

    ![Progetto di database SQL istanza Gestita](../media/ssma-newproject-sqldbmi.png)

*   Post-conversione **correzione advisor**. Come descritto in dettaglio [qui](https://blogs.msdn.microsoft.com/datamigration/2019/02/17/%20accelerate-your-oracle-migrations-with-new-machine-learning-capabilities-in-ssma/).

*   Selezione database preliminare o nello schema.

    Quando ci si connette all'origine, l'utente può a questo punto selezionare i database/schemi di interesse. Selezionando solo gli schemi che si intende eseguire la migrazione verrà risparmiare tempo durante la connessione iniziale e migliorare le prestazioni complessive SSMA.

    ![Oggetti filtro SSMA](../media/ssma-filter-objects.png)

> [!IMPORTANT]
> Con v7.4 SSMA e versioni successive, .net 4.5.2 è un prerequisito di installazione.

## <a name="ssma-v710"></a>SSMA v7.10
La versione v7.10 di SSMA per DB2 contiene le seguenti modifiche:
- Correzioni mirate progettate per offrire maggiore sicurezza e protezione della privacy per soddisfare le modifiche nei requisiti globali.
- Una correzione per la conversione dei blocchi BEGIN-END.

> [!IMPORTANT]
> Con v7.4 SSMA e versioni successive, .net 4.5.2 è un prerequisito di installazione.

## <a name="ssma-v79"></a>SSMA v7.9
La versione v7.9 di SSMA per DB2 contiene le seguenti modifiche:
- Correzioni mirate che consentono di migliorare le metriche di qualità e la conversione.
- Supporto nella riga di comando SSMA per modificare il mapping dei tipi di dati e le preferenze del progetto.
- Supporto per la migrazione dei dati usando SQL Server Integration Services (SSIS). Dopo la conversione dello schema, è possibile creare un pacchetto SSIS usando un'opzione di menu di scelta rapida.
- Finestra di dialogo di connessione Database SQL di Azure in SSMA è stato modificato anche per specificare il nome completo del server. Nelle versioni precedenti di SSMA, il prefisso di Database SQL di Azure doveva essere indicato in modo esplicito all'interno delle impostazioni di progetti.

> [!IMPORTANT]
> Con v7.4 SSMA e versioni successive, .net 4.5.2 è un prerequisito di installazione.

## <a name="ssma-v78"></a>SSMA v7.8
La versione di v 7.8 di SSMA per DB2 contiene le seguenti modifiche:
- Mapping dei tipi di modifica evidenziata nelle impostazioni del progetto.
- È stato possibile agli utenti di disabilitare la telemetria.

> [!IMPORTANT]
> Con v7.4 SSMA e versioni successive, .net 4.5.2 è un prerequisito di installazione.

## <a name="ssma-v77"></a>SSMA v7.7
La versione v7.7 di SSMA per DB2 contiene le seguenti modifiche:
- SSMA per DB2 è stata migliorata con correzioni mirate che consentono di migliorare le metriche di qualità e la conversione.
- La versione a 32 bit di SSMA per DB2 è basato su richiesta comune, è nuovamente. Rispetto all'implementazione precedente (antecedente a v7.4), sono disponibili due pacchetti di installazione, ma non possono essere installati side-by-side. Di conseguenza, è necessario scegliere la versione più appropriata in base ai componenti di connettività che si dispone. È sempre preferibile usare la versione a 64 bit, se possibile.

> [!IMPORTANT]
> Con v7.4 SSMA e versioni successive, .net 4.5.2 è un prerequisito di installazione.

## <a name="ssma-v76"></a>SSMA v7.6
La versione v7.6 di SSMA per DB2 è stata migliorata con correzioni mirate che consentono di migliorare le metriche di qualità e la conversione e con il supporto per SQL Server 2017 (anteprima pubblica). Supporto per SQL Server 2017 in Windows e Linux è disponibile in anteprima pubblica e non deve essere usato per le migrazioni di produzione.

> [!IMPORTANT]
> Con v7.4 SSMA e versioni successive, .net 4.5.2 è un prerequisito di installazione e la versione a 32 bit dello strumento è stata interrotta.

## <a name="ssma-v75"></a>SSMA v7.5
La versione v7.5 di SSMA per DB2 è stata migliorata con numerosi miglioramenti per assicurare maggiore accessibilità per persone affette da disabilità.

> [!IMPORTANT]
> .NET 4.5.2 è un prerequisito per l'installazione di SSMA v7.5. Inoltre, a partire da v7.4, la versione a 32 bit di SSMA verrà terminato a breve.

## <a name="ssma-v74"></a>SSMA v7.4
La versione v7.4 di SSMA per DB2 contiene le seguenti modifiche:
- Il **timeout Query** opzione ora è disponibile durante l'individuazione di oggetti dello schema all'origine e destinazione.
![query timeout-opzione](../media/query-timeout_red.png)

- La metrica della qualità e la conversione è stata migliorata con correzioni mirate, ai suggerimenti dei clienti.

> [!IMPORTANT]
> .NET 4.5.2 è un prerequisito per l'installazione di SSMA v7.4. Inoltre, a partire da v7.4, la versione a 32 bit di SSMA verrà terminato a breve.

## <a name="ssma-v73"></a>SSMA v7.3
La versione v7.3 di SSMA per DB2 contiene le seguenti modifiche:
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
La versione di versione 7.2 di SSMA per DB2 contiene le seguenti modifiche:
- Metrica qualità e conversione migliorata con correzioni mirate ai suggerimenti dei clienti.
- Miglioramenti della telemetria per fornire una migliore punti dati per risolvere i problemi dei clienti e migliorare il tasso di conversione di SSMA.

## <a name="ssma-v71"></a>SSMA v7.1
La versione 7.1 di SSMA per Access contiene le seguenti modifiche:
- A questo punto, SQL Server 2017 in Windows e Linux CTP1 è una piattaforma di destinazione supportate per la migrazione. Questa funzionalità è della versione technical preview e consente lo spostamento dei dati e lo schema per i server SQL di destinazione.
- SSMA supporta ora gli aggiornamenti automatici per scaricare la versione più recente di SSMA, non appena è disponibile.
- I file binari installabili SSMA vengono ora forniti tramite file del pacchetto Windows installer (MSI).

**Risorse**

[Estensione delle funzionalità di SQL Server Migration Assistant conversione](https://blogs.msdn.microsoft.com/datamigration/2017/02/21/2185/)

[Valutare e migrare i dati da piattaforme di dati non Microsoft per SQL Server *(con esempio di Oracle)*](https://blogs.msdn.microsoft.com/datamigration/2016/11/16/sql-server-migration-assistant-how-to-assess-and-migrate-databases-from-non-microsoft-data-platforms-to-sql-server/) 

## <a name="may-2016"></a>Maggio 2016  
La versione di maggio 2016 di SSMA per DB2 contiene le seguenti modifiche:  

-  Aggiunta del supporto per SQL Server 2016.
-  Aggiunta la conversione delle tabelle in memoria e regolare di DB2 alle funzionalità di SQL Server in-memory e hekaton.
-  Conversione aggiunta di controlli di accesso DB2 agli oggetti Criteri di SQL Server (sicurezza a livello di riga per DB2).
-  Aggiunta la conversione delle tabelle con controllo delle versioni del sistema DB2 le tabelle temporali di SQL Server.
-  Parser di DB2 e resolver migliorati.
-  Rimosso controllo programma di installazione per .net 2.0.
-  Rimosso *. dll non necessari dal programma di installazione di Db2.
-  Risolto "Salva progetto" e "open project" comandi per la Console SSMA.
-  Comando fissa "securepassword" per la Console SSMA.
-  Risolto il conteggio degli oggetti per il caricamento iniziale.
-  Correzione del bug nelle impostazioni globali.
  
## <a name="march-2016"></a>Marzo 2016  
La versione di anteprima di marzo 2016 di SSMA per DB2 contiene le seguenti modifiche:  
  
-  Aggiunta del supporto per la migrazione a SQL Server 2016.  
  
## <a name="january-2016"></a>Gennaio 2016  
La versione di gennaio 2016 la manutenzione di SSMA per DB2 contiene le seguenti modifiche:  
  
-  Aggiunta del supporto per un numero di funzioni standard.  
-  Correzione di errori del Parser di DB2.  
-  ZOS di v9 DB2 fisso supporto (RFC 5690920).  
-  DB2 predefinito non risolti errori di identificatore durante la conversione.  
-  Voce di Menu Visualizza aggiunta Log per SSMA (RFC 5706203).  
-  Aggiunti i dati di telemetria.
  
## <a name="november-2014"></a>Novembre 2014  
La versione di novembre 2014 di SSMA per DB2 è la versione iniziale.
