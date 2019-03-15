---
title: Valutare un'azienda e di consolidare i report di valutazione (SQL Server) | Microsoft Docs
description: Informazioni su come utilizzare DMA per valutare un'azienda e consolidare i report di valutazione prima di aggiornare SQL Server o la migrazione al Database SQL di Azure.
ms.custom: ''
ms.date: 03/12/2019
ms.prod: sql
ms.prod_service: dma
ms.reviewer: ''
ms.technology: dma
ms.topic: conceptual
keywords: ''
helpviewer_keywords:
- Data Migration Assistant, Assess
ms.assetid: ''
author: HJToland3
ms.author: rajpo
manager: craigg
ms.openlocfilehash: b2723d437a8171570436fb42f7cd9e305e3a8fea
ms.sourcegitcommit: e9fcd10c7eb87a4f09ac2d8f7647018e83a5f5c5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/14/2019
ms.locfileid: "57974290"
---
# <a name="assess-an-enterprise-and-consolidate-assessment-reports-with-dma"></a>Valutare un'azienda e di consolidare i report di valutazione con DMA

Le istruzioni dettagliate riportate aiutarti a usare Data Migration Assistant per eseguire una valutazione di scalabilità ha esito positivo per l'aggiornamento di SQL Server in locale o in esecuzione SQL Server in macchine virtuali di Azure o per eseguire la migrazione al Database SQL di Azure.

## <a name="prerequisites"></a>Prerequisiti

- Designare un computer di strumenti della rete da cui verrà avviato DMA. Assicurarsi che il computer disponga della connettività per le destinazioni di SQL Server.
- Scaricare e installare:
    - [Data Migration Assistant](https://www.microsoft.com/download/details.aspx?id=53595) v3.6 o versione successiva.
    - [PowerShell](https://aka.ms/wmf5download) versione 5.0 o versione successiva.
    - [.NET framework](https://www.microsoft.com/download/details.aspx?id=30653) v4.5 o successiva.
    - [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) 17.0 o versione successiva.
    - [Power BI desktop](https://docs.microsoft.com/power-bi/desktop-get-the-desktop).
    - [Moduli di Azure PowerShell](https://docs.microsoft.com/powershell/azure/install-az-ps?view=azps-1.0.0)
- Scaricare ed estrarre:
    - Il [modello di Power BI i report di DMA](https://msdnshared.blob.core.windows.net/media/2019/02/PowerBI-Reports.zip).
    - Il [LoadWarehouse script](https://msdnshared.blob.core.windows.net/media/2019/02/LoadWarehouse1.zip).

## <a name="loading-the-powershell-modules"></a>Il caricamento di moduli di PowerShell
Salvare i moduli di PowerShell nella directory dei moduli di PowerShell consente di chiamare i moduli senza la necessità di caricare in modo esplicito prima dell'uso.

Per caricare i moduli, procedere come segue:
1. Passare a c:\Programmi\Microsoft files\windowspowershell\modules. e quindi creare una cartella denominata **DataMigrationAssistant**.
2. Aprire il [moduli di PowerShell](https://msdnshared.blob.core.windows.net/media/2019/02/PowerShell-Modules2.zip)e quindi salvarle nella cartella creata.

      ![Moduli di PowerShell](../dma/media//dma-consolidatereports/dma-powershell-modules.png)

    Ogni cartella contiene il file psm1 associati, come illustrato nella figura seguente:

   ![File psm1 i moduli di PowerShell](../dma/media//dma-consolidatereports/dma-powershell-modules-psm1-files.png)

   > [!NOTE]
   > La cartella e file psm1 che contiene deve avere lo stesso nome.

   > [!IMPORTANT]
   > Potrebbe essere necessario sbloccare i file di PowerShell dopo averle salvate nella directory di WindowsPowerShell per garantire che i moduli da caricare in modo corretto. Per sbloccare un file di PowerShell, fare doppio clic sul file, seleziona **delle proprietà**, selezionare la **Unblock** casella di testo e quindi selezionare **Ok**.

   ![proprietà file psm1](../dma/media//dma-consolidatereports/dma-psm1-file-properties.png)

    PowerShell è ora necessario caricare questi moduli automaticamente quando si avvia una nuova sessione di PowerShell.

## <a name="create-inventory"></a> Creare un inventario delle istanze di SQL Server
Prima di eseguire lo script di PowerShell per valutare i computer SQL Server, è necessario creare un inventario dei server SQL che si desidera valutare.

L'inventario può trovarsi in uno dei due formati:
- File CSV di Excel
- Tabella di SQL Server

### <a name="if-using-a-csv-file"></a>Se si usa un file CSV
> [!IMPORTANT]
> Verificare che il file di inventario viene salvato come file delimitato da virgole (CSV).

Quando si usa un file csv per importare i dati, assicurarsi che esistono solo due colonne di dati - **nome istanza** e **Nome Database**, e che le colonne non includono le righe di intestazione.
 
 ![contenuto del file CSV](../dma/media//dma-consolidatereports/dma-csv-file-contents.png)

### <a name="if-using-sql-server-table"></a>Se si usa una tabella di SQL Server
Creare un database denominato **EstateInventory** e una tabella denominata **DatabaseInventory**. La tabella che contiene questi dati di inventario può avere qualsiasi numero di colonne, fino a quando esistono quattro colonne seguenti:
- ServerName
- InstanceName
- DatabaseName
- AssessmentFlag

![Contenuto della tabella SQL Server](../dma/media//dma-consolidatereports/dma-sql-server-table-contents.png)

Se questo database non è nel computer gli strumenti, verificare che il computer di strumenti disponga della connettività di rete a questa istanza di SQL Server.

Il vantaggio dell'uso di una tabella di SQL Server tramite un file CSV è che è possibile usare la colonna del contrassegno della valutazione per controllare l'istanza o database che ottiene prelevato per la valutazione, che rende più semplice separare le valutazioni in blocchi più piccoli.  Si possono quindi estendersi su più valutazioni (vedere la sezione sull'esecuzione di una valutazione più avanti in questo articolo), che è più semplice che gestire più file CSV.

Tenere presente che in base al numero di oggetti e della loro complessità, una valutazione può richiedere un estremamente lungo tempo (ore +), pertanto è consigliabile separare la valutazione in blocchi gestibili.

## <a name="running-a-scaled-assessment"></a>Esegue una valutazione della scalabilità
Dopo il caricamento di moduli di PowerShell nella directory dei moduli e creazione di un inventario, è necessario eseguire una valutazione con scalabilità, aprire PowerShell e che esegue la funzione dmaDataCollector.
 
  ![elenchi di dmaDataCollector (funzione)](../dma/media//dma-consolidatereports/dma-dmaDataCollector-function-listing.png)

I parametri associati alla funzione dmaDataCollector sono descritti nella tabella seguente.

|Parametro  |Descrizione |
|---------|---------|
|**getServerListFrom** | L'inventario. I valori possibili sono **SqlServer** e **CSV**.<br/>Per altre informazioni, vedi [creare un inventario dei server SQL](#create-inventory). |
|**csvPath** | Il percorso del file di inventario CSV.  Utilizzati solo quando si **getServerListFrom** è impostata su **CSV**. |
|**serverName** | Il nome dell'istanza SQL Server dell'inventario quando si usa **SqlServer** nel **getServerListFrom** parametro. |
|**databaseName** | Il database che ospita la tabella di inventario. |
|**AssessmentName** | Il nome della valutazione DMA. |
|**TargetPlatform** | Il tipo di destinazione della valutazione che si desidera eseguire.  I valori possibili sono **AzureSQLDatabase**, **SQLServer2012**, **SQLServer2014**, **SQLServer2016**,  **SQLServerLinux2017**, **SQLServerWindows2017**, e **ManagedSqlServer**. |
|**AuthenticationMethod** | Il metodo di autenticazione per la connessione alle destinazioni di SQL Server a cui si desidera valutare. I valori possibili sono **SQLAuth** e **WindowsAuth**. |
|**OutputLocation** | La directory in cui si desidera archiviare il codice JSON file di output della valutazione. A seconda del numero di database viene valutata e il numero di oggetti all'interno dei database, le valutazioni possono richiedere tempi estremamente lunghi. Il file verrà scritto dopo aver completato tutte le valutazioni. |

Se si verifica un errore imprevisto, quindi la finestra di comando che ottiene avviata da questo processo verrà terminata.  Esaminare il log degli errori per determinare il motivo dell'errore.
 
  ![Percorso log degli errori](../dma/media//dma-consolidatereports/dma-error-log-file-location.png)

## <a name="consuming-the-assessment-json-file"></a>Utilizzo del file JSON di valutazione

Al termine della valutazione, ora possibile importare i dati in SQL Server per l'analisi. Per utilizzare il file JSON di valutazione, aprire PowerShell ed eseguire la funzione dmaProcessor.
 
  ![elenco di dmaProcessor (funzione)](../dma/media//dma-consolidatereports/dma-dmaProcessor-function-listing.png)

I parametri associati alla funzione dmaProcessor sono descritti nella tabella seguente.

|Parametro  |Descrizione |
|---------|---------|
|**processTo** | Il percorso in cui verrà elaborato il file JSON. I valori possibili sono **SQLServer** e **AzureSQLDatabase**. |
|**serverName** | Istanza di SQL Server in cui verranno elaborati i dati.  Se si specifica **AzureSQLDatabase** per il **processTo** parametro, quindi includere solo il nome di SQL Server (non includono. database.windows.net). Verrà richiesto per due account di accesso quando la destinazione di Database SQL di Azure. il primo è le credenziali del tenant di Azure, mentre il secondo è l'account di accesso di amministratore per il Server SQL di Azure. |
|**CreateDMAReporting** | Il database di gestione temporanea per creare per l'elaborazione del file JSON.  Se il database che si specifica già esiste e questo parametro è impostato su uno, quindi gli oggetti non ottenere creati.  Questo parametro è utile per la ricreazione di un singolo oggetto che è stato eliminato. |
|**CreateDataWarehouse** | Crea il data warehouse che verrà usato nel report di Power BI. |
|**databaseName** | Il nome del database DMAReporting. |
|**warehouseName** | Nome del database del data warehouse. |
|**jsonDirectory** | Directory contenente il file JSON di valutazione.  Se sono presenti più file JSON nella directory, il che sta elaborati uno alla volta. |

La funzione dmaProcessor dovrebbe richiedere solo alcuni secondi per elaborare un singolo file.

## <a name="loading-the-data-warehouse"></a>Il caricamento del data warehouse
Dopo il dmaProcessor ha completato l'elaborazione dei file di valutazione, i dati verranno caricati nel database DMAReporting nella tabella dati rapporto. A questo punto, è necessario caricare il data warehouse.

1. Usare lo script LoadWarehouse per popolare i valori mancanti nelle dimensioni.

    Lo script accettano i dati dalla tabella di dati rapporto nel database DMAReporting e caricarlo nel warehouse.  Se si verificano errori durante questo processo di caricamento, si tratta probabilmente di un risultato di voci mancanti nelle tabelle delle dimensioni.

2. Caricare il data warehouse.
 
      ![LoadWarehouse contenuto caricato](../dma/media//dma-consolidatereports/dma-LoadWarehouse-loaded.png)

## <a name="set-your-database-owners"></a>Impostare i proprietari del database
Sebbene non sia obbligatorio, per ottenere il massimo valore dai report, è consigliabile impostare i proprietari di database **dimDBOwner** dimensione e quindi aggiornare **DBOwnerKey** nel  **FactAssessment** tabella.  Seguendo questa procedura consentirà di sezionamento e filtro del report di Power BI in base ai proprietari di database specifici.

È anche possibile usare lo script LoadWarehouse per fornire le istruzioni TSQL di base per impostare i proprietari di database.

  ![Proprietari di impostazione LoadWarehouse](../dma/media//dma-consolidatereports/dma-LoadWarehouse-set-owners.png)

## <a name="dma-reports"></a>Report DMA

1. Aprire il modello DMA i report Power BI in Power BI Desktop.
2. Immettere i dettagli del server che puntano alle **DMAWarehouse** del database e quindi selezionare **carico**.
   
      ![Caricare il modello DMA i report Power BI](../dma/media//dma-consolidatereports/dma-reports-powerbi-template-loaded.png)

   Dopo che il report ha aggiornato i dati di **DMAWarehouse** database, viene visualizzato un report simile al seguente.

   ![Visualizzazione di report DMAWarehouse](../dma/media//dma-consolidatereports/dma-DMAWarehouse-report1.png)

   > [!TIP]
   > Se non è possibile visualizzare i dati che previsti, provare a modificare il segnalibro attivo.  Per altre informazioni, vedere i dettagli nella sezione seguente.

## <a name="working-with-dma-reports"></a>Utilizzo dei report DMA
Per usare i report DMA, usare i segnalibri e filtri dei dati per filtrare in base:
- Tipi di valutazione (database SQL di Azure, istanza Gestita SQL di Azure, SQL in locale) 
- Nome istanza
- Nome database
- Nome del team

Per accedere al pannello di segnalibri e filtri, selezionare il segnalibro filtri nella pagina del report principale:

![I filtri e i segnalibri report DMA](../dma/media//dma-consolidatereports/dma-report-bookmarks-filters.png)

In questo modo il pannello seguente:

![Pannello di visualizzazioni dei rapporti DMA](../dma/media//dma-consolidatereports/dma-report-views-blade.png)

È possibile usare i segnalibri per cambiare il contesto di creazione di report tra:
- Valutazioni cloud di Azure SQL DB
- Valutazioni di cloud di istanza Gestita di SQL Azure
- Valutazioni in locale

![Segnalibri di visualizzazioni dei rapporti DMA](../dma/media//dma-consolidatereports/dma-report-bookmarks1.png)

Per nascondere il pannello di filtri, CTRL + clic sul pulsante indietro:

![Visualizzazioni dei rapporti DMA pulsante Indietro](../dma/media//dma-consolidatereports/dma-report-bookmarks-back.png)

C'è un prompt dei comandi nella parte inferiore della pagina del report per mostrare se attualmente si applica un filtro in uno qualsiasi degli elementi seguenti:
* FactAssessment-InstanceName
* FactAssessment-DatabaseName
* dimDBOwner - DBOwner

![Prompt dei comandi filtro applicato](../dma/media//dma-consolidatereports/dma-filter-applied-prompt.png)

> [!NOTE]
> Se si esegue solo una valutazione di Database SQL di Azure, vengono popolati solo i report di Cloud. Viceversa, se si esegue solo una valutazione in locale, vengono popolati solo i report in locale. Tuttavia, se si esegue un'istanza di Azure sia una valutazione di On-Premise e quindi caricano entrambi valutazioni nel warehouse, è possibile passare tra i report di Cloud e locale facendo clic CTRL l'icona associata.

## <a name="reports-visuals"></a>Oggetti visivi di report
I dettagli visualizzati nei report di Power BI viene visualizzato nelle sezioni seguenti.

### <a name="readiness-"></a>% Conformità

  ![Percentuale conformità DMA](../dma/media//dma-consolidatereports/dma-readiness-percentage.png)

Questo oggetto visivo viene aggiornato in base al contesto di selezione (tutti gli elementi, dell'istanza, database [multipli di]).

### <a name="readiness-count"></a>Conteggio di conformità

  ![Conteggio di conformità DMA](../dma/media//dma-consolidatereports/dma-readiness-count.png)

Questo oggetto visivo Mostra il numero di database che sono pronti per eseguire la migrazione il numero di database che non sono ancora pronti per eseguire la migrazione.

### <a name="readiness-bucket"></a>Bucket di conformità

  ![Bucket Readiness DMA](../dma/media//dma-consolidatereports/dma-readiness-bucket.png)

Questo oggetto visivo Mostra una suddivisione dei database da parte dei bucket di idoneità seguenti:
- PRONTO PER 100%
- PRONTI A 99 75%
- 50-75% PRONTO
- NON È PRONTO

### <a name="issues-word-cloud"></a>Problemi Word Cloud
 
  ![Problemi DMA WordCloud](../dma/media//dma-consolidatereports/dma-issues-word-cloud.png)

Questo oggetto visivo Mostra i problemi che attualmente si verificano all'interno nel contesto di selezione (tutti gli elementi, dell'istanza, database [multipli di]). Maggiore di word viene visualizzato sullo schermo, maggiore il numero di problemi in tale categoria. Si posiziona il puntatore del mouse su una parola Mostra il numero di problemi che si verificano in tale categoria.

### <a name="database-readiness"></a>Preparazione del database

  ![Report di conformità Database DMA](../dma/media//dma-consolidatereports/dma-database-readiness-report.png)

In questa sezione è la parte principale del report, che mostra l'idoneità di un database di istanza. Questo report include una gerarchia di drill-down di:
- InstanceDatabase
- ChangeCategory
- Titolo
- ObjectType
- ImpactedObjectName

 ![Drill-down report di conformità Database DMA](../dma/media//dma-consolidatereports/dma-database-readiness-report-drilldown.png)

Questo report viene usato anche come punto di filtro per la creazione di Report piano di correzione.

Per analizzare il Report piano di correzione, fare clic su un punto dati nel grafico a barre, scegliere **drill-through**, quindi selezionare **piani di correzione**.

Questa attività consente di filtrare il report piano di correzione per il livello della gerarchia corrente in base al punto in cui si selezionano il drill-through opzione.

  ![DMA Database Readiness drill-down report filtrato](../dma/media//dma-consolidatereports/dma-database-readiness-report-drilldown-filtered.png)

  ![Report piano di correzione DMA](../dma/media//dma-consolidatereports/dma-remediation-plan-report.png)

È possibile usare anche il report piano di correzione sul proprio per compilare una risoluzione personalizzata piano usando i filtri nel **filtri di visualizzazioni** pannello.
 
  ![Opzioni di filtro report piano di correzione DMA](../dma/media//dma-consolidatereports/dma-remediation-plan-report-filter-options.png)

### <a name="script-disclaimer"></a>Dichiarazione di non responsabilità script
*Gli script di esempio forniti in questo articolo non sono supportati in alcun programma di supporto tecnico standard di Microsoft o un servizio. Tutti gli script vengono forniti così come sono senza garanzie di alcun tipo. Microsoft ha declina tutte le garanzie implicite tra cui, in via esemplificativa, qualsiasi garanzia di commerciabilità o di adeguatezza per uno scopo specifico. Il rischio derivante dall'utilizzo o gli script di esempio e documentazione deell'utente. In nessun caso Microsoft, i relativi autori o chiunque altro coinvolti nella creazione, produzione o recapito degli script sarà responsabile per danni (incluso, in via esemplificativa, danni per perdita o mancato guadagno, interruzione dell'attività, perdita di le informazioni aziendali, o altre perdite economiche) derivanti dall'utilizzo di o all'impossibilità di usare gli script di esempio o documentazione, anche se Microsoft sia stata informata della possibilità del verificarsi di tali danni.  Autorizzazione prima di questi script di report in altri siti/repository/blog di ricerca.*
