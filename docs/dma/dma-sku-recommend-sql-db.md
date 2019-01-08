---
title: Identificare lo SKU del Database SQL di Azure corretto per il database locale (Data Migration Assistant) | Microsoft Docs
description: Informazioni su come usare Data Migration Assistant per identificare destra dello SKU del Database SQL di Azure per il database in locale
ms.custom: ''
ms.date: 10/20/2018
ms.prod: sql
ms.prod_service: dma
ms.reviewer: ''
ms.technology: dma
ms.topic: conceptual
keywords: ''
helpviewer_keywords:
- Data Migration Assistant, Assess
ms.assetid: ''
author: pochiraju
ms.author: rajpo
manager: craigg
ms.openlocfilehash: 6e990d8b3320eafccc3da574476fa66cdf52d8d5
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/28/2018
ms.locfileid: "52544113"
---
# <a name="identify-the-right-azure-sql-database-sku-for-your-on-premises-database"></a>Identificare lo SKU del Database SQL di Azure corretto per il database in locale

L'attività di migrazione dei database nel cloud è un complicato e che richiedono molto tempo, che includono una serie di variabili. Selezione dello SKU e destinazione di database di Azure corretta per il database può risultare complessa. Il nostro obiettivo con il Database Migration Assistant (DMA) consiste nel risolvere questi dubbi e rendere la migrazione dei database esperienza semplice ed efficace.

Questo articolo è incentrato principalmente sulla funzionalità consigli di DMA SKU del Database SQL di Azure, che consente di identificare il valore minimo consigliato di SKU di Database SQL di Azure basati sui contatori delle prestazioni raccolti dai computer che ospita i database. Questa funzionalità offre consigli relativi ai prezzi di livello, a livello di calcolo e le dimensioni massime dei dati, nonché il costo stimato al mese. Offre inoltre la possibilità di eseguire il provisioning in blocco tutti i database in Azure.

> [!NOTE] 
> Questa funzionalità è attualmente disponibile solo tramite l'interfaccia della riga di comando (CLI). Supporto per questa funzionalità tramite l'interfaccia utente DMA verrà aggiunto in una versione futura.

> [!IMPORTANT]
> Le raccomandazioni dello SKU per il Database SQL di Azure sono attualmente disponibili per le migrazioni da SQL Server 2016 o versione successiva.

Le istruzioni seguenti consentono di determinare le raccomandazioni dello SKU del Database SQL di Azure ed effettuare il provisioning dei database associati in Azure usando Data Migration Assistant.

## <a name="prerequisites"></a>Prerequisiti

Scaricare Database Migration Assistant v4.0 o versione successiva e quindi installarlo. Se hai già lo strumento di installazione, chiudere e riaprirlo e verrà richiesto di aggiornare lo strumento.

## <a name="collect-performance-counters"></a>Raccogliere i contatori delle prestazioni

Il primo passaggio del processo è per raccogliere i contatori delle prestazioni per i database. È possibile raccogliere i contatori delle prestazioni eseguendo un comando di PowerShell nel computer che ospita i database. DMA fornisce una copia di questo file di PowerShell, ma è anche possibile usare il proprio metodo per acquisire i contatori delle prestazioni dal computer.

Non devi eseguire questa attività per ogni database singolarmente. I contatori delle prestazioni raccolti da un computer sono utilizzabile per consigliare lo SKU per tutti i database ospitati nel computer.

> [!IMPORTANT]
> Il computer da cui si esegue questo comando richiede le autorizzazioni di amministratore nel computer che ospita i database.

1. Verificare che il file di PowerShell necessario per raccogliere i contatori delle prestazioni sia installato nella cartella DMA.

    ![File di PowerShell riportato nella cartella DMA](../dma/media/dma-sku-recommend-data-collection-file.png)

2. Eseguire lo script di PowerShell con gli argomenti seguenti:
    - **ComputerName**: Il nome del computer che ospita i database.
    - **OutputFilePath**: Il percorso del file di output per salvare i contatori raccolti.
    - **CollectionTimeInSeconds**: La quantità di tempo durante il quale si vuole raccogliere i dati dei contatori delle prestazioni.
      Acquisire i contatori delle prestazioni per almeno 40 minuti ottenere una raccomandazione significativo. Maggiore è la durata dell'acquisizione, più accurato l'indicazione sarà.
    - **DbConnectionString**: La stringa di connessione che punta al database master ospitato nel computer da cui si sta raccogliendo i dati dei contatori delle prestazioni.
     
    Di seguito è una chiamata di esempio:

    ```
    .\SkuRecommendationDataCollectionScript.ps1
     -ComputerName Foobar1
     -OutputFilePath D:\counters2.csv
     -CollectionTimeInSeconds 10
     -DbConnectionString "Server=localhost;Initial Catalog=master;Integrated Security=SSPI;"
    ```
    
    Dopo l'esecuzione del comando, il processo genererà un file con contatori delle prestazioni nel percorso specificato. Questo file può essere usato come input per il comando di raccomandazione di SKU nella sezione successiva.

## <a name="use-the-dma-cli-to-get-sku-recommendations"></a>Usare la CLI di DMA per ottenere le raccomandazioni dello SKU

Utilizzare il file di output dei contatori delle prestazioni nel passaggio precedente come input per questo passaggio. DMA fornirà indicazioni per il Database SQL di Azure piano tariffario, il livello di calcolo e la dimensione massima dei dati per ogni database nel computer. DMA anche fornirà all'utente il costo mensile stimato per ogni database.

Eseguire il dmacmd.exe con gli argomenti seguenti:

- **/ Action = SkuRecommendation**: Specificare questo argomento per eseguire valutazioni dello SKU.
- **/ SkuRecommendationInputDataFilePath**: Il percorso del file dei contatori raccolti nella sezione precedente.
- **/ SkuRecommendationTsvOutputResultsFilePath**: Il percorso in cui scrivere i risultati di output in formato TSV.
- **/ SkuRecommendationJsonOutputResultsFilePath**: Il percorso in cui scrivere i risultati di output in formato JSON.
- **/ SkuRecommendationHtmlResultsFilePath**: Percorso in cui scrivere i risultati di output in formato HTML.

Inoltre, è necessario scegliere uno degli argomenti seguenti:
- Impedire l'aggiornamento di prezzo
    - **/ SkuRecommendationPreventPriceRefresh**: Impedisce l'aggiornamento di prezzo. Utilizzare se è in esecuzione in modalità offline.
- Ottieni i prezzi più recenti 
    - **/ SkuRecommendationCurrencyCode**: La valuta in cui visualizzare i prezzi (ad esempio "USD").
    - **/ SkuRecommendationOfferName**: L'offerta assegnare un nome (ad esempio "MS-AZR - 0003P"). Per altre informazioni, vedere la [dettagli dell'offerta Microsoft Azure](https://azure.microsoft.com/support/legal/offer-details/) pagina.
    - **/ SkuRecommendationRegionName**: L'area assegnare un nome (ad esempio "Stati Uniti occidentali").
    - **/ SkuRecommendationSubscriptionId**: ID della sottoscrizione.
    - **/ AzureAuthenticationTenantId**: Il tenant di autenticazione.
    - **/ AzureAuthenticationClientId**: L'ID client dell'app AAD usato per l'autenticazione.
    - Una delle opzioni di autenticazione seguenti:
        - Interattiva
            - **AzureAuthenticationInteractiveAuthentication**: Impostato su true per una finestra popup dell'autenticazione.
        - Basata su
            - **AzureAuthenticationCertificateStoreLocation**: Impostare il percorso dell'archivio certificati (ad esempio "CurrentUser").
            - **AzureAuthenticationCertificateThumbprint**: Impostare l'identificazione personale del certificato.
        - Basato su token
            - **AzureAuthenticationToken**: Impostare per il token di certificato.

Ecco alcune chiamate di esempio:

```
.\DmaCmd.exe /Action=SkuRecommendation
/SkuRecommendationInputDataFilePath="C:\TestOut\out.csv"
/SkuRecommendationTsvOutputResultsFilePath="C:\TestOut\prices.tsv"
/SkuRecommendationJsonOutputResultsFilePath="C:\TestOut\prices.json"
/SkuRecommendationOutputResultsFilePath="C:\TestOut\prices.html"
/SkuRecommendationCurrencyCode=USD
/SkuRecommendationOfferName=MS-AZR-0044p
/SkuRecommendationRegionName=UKWest
/SkuRecommendationSubscriptionId=<Your Subscription Id>
/AzureAuthenticationInteractiveAuthentication=true
/AzureAuthenticationClientId=<Your AzureAuthenticationClientId>
/AzureAuthenticationTenantId=<Your AzureAuthenticationTenantId>
```

```
.\DmaCmd.exe /Action=SkuRecommendation
/SkuRecommendationInputDataFilePath="C:\TestOut\out.csv"
/SkuRecommendationTsvOutputResultsFilePath="C:\TestOut\prices.tsv"
/SkuRecommendationJsonOutputResultsFilePath="C:\TestOut\prices.json"
/SkuRecommendationOutputResultsFilePath="C:\TestOut\prices.html"
/SkuRecommendationPreventPriceRefresh=true
```

Il file di output TSV conterrà le colonne visualizzate nel grafico seguente:

   ![File di PowerShell riportato nella cartella DMA](../dma/media/dma-tsv-file-column.png)

Segue una descrizione di ogni colonna.

- **DatabaseName** -il nome del database.
- **MetricName** : se è stata eseguita una metrica.
- **MetricType** -livello di Database SQL di Azure consigliata.
- **MetricValue** -consigliato di Database SQL di Azure lo SKU.
- **SQLMiEquivalentCores** -se si sceglie a chi rivolgersi per istanza gestita di Azure SQL Database, è possibile usare questo valore per il numero di core.
- **IsTierRecommended** -rendiamo un minimo consigliato di SKU per ogni livello. È quindi possibile applicare l'euristica per determinare il livello più adatto per il database. 
- **ExclusionReasons** -questo valore è vuoto se un livello è consigliato. Per ogni livello che non è consigliato, offriamo i motivi il motivo per cui non è stato selezionato.
- **AppliedRules** -una notazione breve delle regole che sono state applicate.

Il valore consigliato è lo SKU minimo richiesto per le query da eseguire in Azure con una percentuale di successo simile ai database in locale. Ad esempio, se lo SKU minima consigliato è S4 per il livello standard, quindi scegliere S3 o di sotto verrà impedire il timeout delle query o un errore di esecuzione.

Il file HTML contiene queste informazioni in formato grafico. È possibile utilizzare il file HTML per le informazioni di sottoscrizione di Azure di input, selezionare il piano tariffario, dimensioni massime dei dati e a livello di calcolo per i database e generare uno script per eseguire il provisioning dei database. Questo script può essere eseguito tramite PowerShell.

## <a name="provision-your-databases-to-azure"></a>Effettuare il provisioning dei database in Azure
Con pochi clic, è possibile usare le raccomandazioni nel passaggio precedente per il provisioning dei database di destinazione in Azure a cui è possibile eseguire la migrazione dei database. È anche possibile apportare modifiche ai consigli aggiornando il file HTML, come indicato di seguito.

1. Aprire il file HTML e immettere le informazioni seguenti:
    - **ID sottoscrizione** -l'ID sottoscrizione della sottoscrizione di Azure a cui si desidera eseguire il provisioning dei database.
    - **Area** -l'area in cui eseguire il provisioning di database. Assicurarsi che la propria sottoscrizione supporti il selezionare region.
    - **Gruppo di risorse** -il gruppo di risorse a cui si desidera distribuire i database. Immettere un gruppo di risorse esistente.
    - **Nome del server** -server di Database SQL di Azure a cui si desidera che i database distribuiti. Se si immette un nome di server che non esiste, verrà creato.
    - **Admin Username\Password** -il nome utente amministratore server e la password.

2. Esaminare le raccomandazioni per ogni database e modificare il piano tariffario, livello e le dimensioni di dati max in base alle esigenze di calcolo. Assicurarsi di deselezionare tutti i database desiderati non attualmente effettuare il provisioning.

3. Selezionare **genera Script di Provisioning**, salvare lo script e quindi di eseguirlo in PowerShell.

    Questo processo deve creare tutti i database selezionati nella pagina HTML.

È possibile eseguire tutti i passaggi in questo processo in un singolo computer oppure è possibile eseguirle in più computer per determinare le raccomandazioni dello SKU su larga scala. DMA rende un'esperienza semplice e scalabile grazie al supporto di tutti questi passaggi tramite l'interfaccia della riga di comando. Anche in questo caso, il supporto per questa funzionalità tramite l'interfaccia utente DMA saranno disponibile più avanti quest'anno.

## <a name="next-steps"></a>Passaggi successivi
- Scaricare la versione più recente di [Data Migration Assistant](https://aka.ms/get-dma).
- Vedere l'articolo [eseguito Data Migration Assistant da riga di comando](https://docs.microsoft.com/sql/dma/dma-commandline?view=sql-server-2017) per un elenco completo dei comandi per l'esecuzione DMA dal comando.
