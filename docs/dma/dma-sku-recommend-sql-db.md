---
title: Identificare lo SKU del Database SQL di Azure corretto per il database locale (Data Migration Assistant) | Microsoft Docs
description: Informazioni su come usare Data Migration Assistant per identificare destra dello SKU del Database SQL di Azure per il database in locale
ms.custom: ''
ms.date: 05/06/2019
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
ms.author: jtoland
manager: jroth
ms.openlocfilehash: 5effd31d37af5fbe119f1ad23781b994fa89c240
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66794318"
---
# <a name="identify-the-right-azure-sql-databasemanaged-instance-sku-for-your-on-premises-database"></a>Identificare il diritto SKU istanza gestita/Database SQL di Azure per il database in locale

Migrazione di database nel cloud può essere complessa, soprattutto quando si tenta di selezionare gli SKU e destinazione di database di Azure ottimo per il database. Il nostro obiettivo con il Database Migration Assistant (DMA) è per risolvere questi dubbi e semplificare la migrazione dei database di esperienza, fornendo anche raccomandazioni questi SKU in un output a semplici da usare.

Questo articolo è incentrato sulla funzionalità di raccomandazioni di DMA SKU del Database SQL di Azure. Database SQL di Azure offre diverse opzioni di distribuzione, tra cui:

- Database singolo
- Pool elastici
- istanza gestita

La funzionalità consente di identificare entrambe minime consigliate database singolo Database SQL di Azure consigli di SKU o istanza gestita SKU basato sui contatori delle prestazioni raccolti dai computer che ospita i database. La funzionalità offre consigli relativi ai prezzi di livello, a livello di calcolo e le dimensioni massime dei dati, nonché il costo stimato al mese. Offre anche la possibilità di blocco provision singoli database e istanze gestite di Azure per tutti i database consigliati.

> [!NOTE]
> Questa funzionalità è attualmente disponibile solo tramite l'interfaccia della riga di comando (CLI).

Di seguito sono istruzioni che consentono di determinare le raccomandazioni dello SKU del Database SQL di Azure ed effettuare il provisioning di database singoli corrispondenti o le istanze gestite di Azure con DMA.

## <a name="prerequisites"></a>Prerequisiti

- Scaricare e installare la versione più recente di [DMA](https://aka.ms/get-dma). Se si dispone già di una versione precedente dello strumento, aprirlo e verrà richiesto per eseguire l'aggiornamento DMA.
- Assicurarsi che il computer abbia [PowerShell versione 5.1](https://www.microsoft.com/download/details.aspx?id=54616) o versioni successive, che è necessario per eseguire tutti gli script. Per informazioni su findoug out quale versione di PowerShell è installata nel computer in uso, vedere l'articolo [scaricare e installare Windows PowerShell 5.1](https://docs.microsoft.com/skypeforbusiness/set-up-your-computer-for-windows-powershell/download-and-install-windows-powershell-5-1).
- Assicurarsi che il computer abbia installato il modulo Powershell di Azure. Per altre informazioni, vedere l'articolo [installare il modulo Azure PowerShell](https://docs.microsoft.com/powershell/azure/install-az-ps?view=azps-1.8.0).
- Verificare che il file di PowerShell **SkuRecommendationDataCollectionScript.ps1**, che è necessario per raccogliere i contatori delle prestazioni, viene installato nella cartella DMA.
- Assicurarsi che il computer in cui si eseguirà questo processo abbia le autorizzazioni di amministratore nel computer che ospita i database.

## <a name="collect-performance-counters"></a>Raccogliere i contatori delle prestazioni

Il primo passaggio del processo è per raccogliere i contatori delle prestazioni per i database. È possibile raccogliere i contatori delle prestazioni eseguendo un comando di PowerShell nel computer che ospita i database. DMA fornisce una copia di questo file di PowerShell, ma è anche possibile usare il proprio metodo per acquisire i contatori delle prestazioni dal computer.

Non devi eseguire questa attività per ogni database singolarmente. I contatori delle prestazioni raccolti da un computer sono utilizzabile per consigliare lo SKU per tutti i database ospitati nel computer.

1. Nella cartella DMA, individuare il file PowerShell SkuRecommendationDataCollectionScript.ps1. Questo file è necessario raccogliere i contatori delle prestazioni.

    ![File di PowerShell riportato nella cartella DMA](../dma/media/dma-sku-recommend-data-collection-file.png)

2. Eseguire lo script di PowerShell con gli argomenti seguenti:
    - **ComputerName**: Il nome del computer che ospita i database.
    - **OutputFilePath**: Il percorso del file di output per salvare i contatori raccolti.
    - **CollectionTimeInSeconds**: La quantità di tempo durante il quale si vuole raccogliere i dati dei contatori delle prestazioni. Acquisire i contatori delle prestazioni per almeno 40 minuti ottenere una raccomandazione significativo. Maggiore è la durata dell'acquisizione, più accurato l'indicazione sarà. Verificare anche i carichi di lavoro sono in esecuzione per i database desiderati abilitare le raccomandazioni più accurate.
    - **DbConnectionString**: La stringa di connessione che punta al database master ospitato nel computer da cui si sta raccogliendo i dati dei contatori delle prestazioni.

    Di seguito è una chiamata di esempio:

    ```
    .\SkuRecommendationDataCollectionScript.ps1
     -ComputerName Foobar1
     -OutputFilePath D:\counters2.csv
     -CollectionTimeInSeconds 2400
     -DbConnectionString "Server=localhost;Initial Catalog=master;Integrated Security=SSPI;"
    ```

    Dopo l'esecuzione del comando, il processo genererà un file, compresi i contatori delle prestazioni per il percorso specificato. È possibile usare questo file come input per la parte successiva del processo, in modo da fornire raccomandazioni dello SKU per il database singolo e le opzioni di istanze gestite.

## <a name="use-the-dma-cli-to-get-sku-recommendations"></a>Usare la CLI di DMA per ottenere le raccomandazioni dello SKU

Utilizzare il file di output di contatori delle prestazioni è stato creato come input per questo processo.

Per l'opzione di database singolo, DMA fornirà indicazioni per il database di Database SQL di Azure singolo piano tariffario, il livello di calcolo e la dimensione massima dei dati per ogni database nel computer. Se si dispone di più database nel computer in uso, è anche possibile specificare i database per cui si vuole ottenere i consigli. DMA anche fornirà all'utente il costo mensile stimato per ogni database.

Per l'istanza gestita, le raccomandazioni supportano uno scenario lift-and-shift. Di conseguenza, DMA fornirà indicazioni per l'istanza gestita di Database SQL di Azure piano tariffario, il livello di calcolo e la dimensione massima dei dati per il set di database nel computer. Anche in questo caso, se si dispone di più database nel computer in uso, è possibile specificare anche i database per cui si vuole ottenere i consigli. DMA anche fornirà all'utente il costo mensile stimato per l'istanza gestita.

Per usare la CLI di DMA per ottenere le raccomandazioni dello SKU, al prompt dei comandi, eseguire dmacmd.exe con gli argomenti seguenti:

- **/Action=SkuRecommendation**: Specificare questo argomento per eseguire valutazioni dello SKU.
- **/SkuRecommendationInputDataFilePath**: Il percorso del file dei contatori raccolti nella sezione precedente.
- **/SkuRecommendationTsvOutputResultsFilePath**: Il percorso in cui scrivere i risultati di output in formato TSV.
- **/SkuRecommendationJsonOutputResultsFilePath**: Il percorso in cui scrivere i risultati di output in formato JSON.
- **/SkuRecommendationHtmlResultsFilePath**: Percorso in cui scrivere i risultati di output in formato HTML.

Inoltre, selezionare uno degli argomenti seguenti:

- Impedire l'aggiornamento di prezzo
  - **/SkuRecommendationPreventPriceRefresh**: Se impostato su True, impedisce l'aggiornamento di prezzo e presuppone che i prezzi predefiniti. Utilizzare se è in esecuzione in modalità offline. Se non si utilizza questo parametro, è necessario specificare i parametri seguenti per ottenere i prezzi più recenti basati su un'area specificata.
- Ottieni i prezzi più recenti
  - **/SkuRecommendationCurrencyCode**: La valuta in cui visualizzare i prezzi (ad esempio "USD").
  - **/SkuRecommendationOfferName**: L'offerta assegnare un nome (ad esempio "MS-AZR-0003P"). Per altre informazioni, vedere la [dettagli dell'offerta Microsoft Azure](https://azure.microsoft.com/support/legal/offer-details/) pagina.
    - **/SkuRecommendationRegionName**: Il nome dell'area (ad esempio "Stati Uniti occidentali").
    - **/SkuRecommendationSubscriptionId**: ID della sottoscrizione.
    - **/AzureAuthenticationTenantId**: Il tenant di autenticazione.
    - **/AzureAuthenticationClientId**: L'ID client dell'app AAD usato per l'autenticazione.
    - Una delle opzioni di autenticazione seguenti:
      - Interattiva
        - **AzureAuthenticationInteractiveAuthentication**: Impostato su true per una finestra popup dell'autenticazione.
      - Basata su
        - **AzureAuthenticationCertificateStoreLocation**: Impostare il percorso dell'archivio certificati (ad esempio, "CurrentUser").
        - **AzureAuthenticationCertificateThumbprint**: Impostare l'identificazione personale del certificato.
      - Basato su token
        - **AzureAuthenticationToken**: Impostare per il token di certificato.

> [!NOTE]
> Per ottenere l'ID client e ID tenant per l'autenticazione interattiva, è necessario configurare una nuova applicazione di AAD. Per altre informazioni sull'autenticazione e il recupero di queste credenziali, nell'articolo [Microsoft Azure Billing esempi di codice API: API RateCard](https://azure.microsoft.com/resources/samples/billing-python-ratecard-api/), seguire le istruzioni riportate sotto **passaggio 1: Configurare un'applicazione Client nativa nel tenant di AAD**.

Infine, è disponibile un argomento facoltativo, che è possibile usare per specificare i database per cui si desidera raccomandazioni: 

- **/SkuRecommendationDatabasesToRecommend**: Un elenco di database per cui si desidera generare indicazioni. Trovare il database nomi sono tra maiuscole e minuscole ed è necessario (1) in di input con estensione csv, (2) ogni essere racchiuso tra virgolette doppie e (3) essere separati da uno spazio singolo tra i nomi (ad esempio /SkuRecommendationDatabasesToRecommend "Database1" = "Database2" "Database3") . Se si omette questo parametro assicurarsi che vengono forniti consigli per tutti i database utente identificati nel file di input con estensione csv.  

Di seguito sono alcune chiamate di esempio:

**Esempio 1: Acquisizione di consigli con prezzi predefiniti. Usare durante l'esecuzione in modalità offline o quando non si dispongono di credenziali di autenticazione.**

```
.\DmaCmd.exe /Action=SkuRecommendation
/SkuRecommendationInputDataFilePath="C:\TestOut\out.csv"
/SkuRecommendationTsvOutputResultsFilePath="C:\TestOut\prices.tsv"
/SkuRecommendationJsonOutputResultsFilePath="C:\TestOut\prices.json"
/SkuRecommendationOutputResultsFilePath="C:\TestOut\prices.html"
/SkuRecommendationPreventPriceRefresh=true
```

**Esempio 2: Acquisizione di consigli con prezzi più recenti per l'area specificata (ad esempio, "UKWest").**

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

**Esempio 3: Recupero di raccomandazioni per database specifici (ad esempio “TPCDS1G,EDW_3G,TPCDS10G”).**

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
/SkuRecommendationDatabasesToRecommend=“TPCDS1G” “EDW_3G” “TPCDS10G” 
/AzureAuthenticationInteractiveAuthentication=true 
/AzureAuthenticationClientId=<Your AzureAuthenticationClientId> 
/AzureAuthenticationTenantId=<Your AzureAuthenticationTenantId>
```

Per altri suggerimenti di database singolo, il file di output TSV apparirà come indicato di seguito:

![File singolo-db PowerShell illustrato nella cartella DMA](../dma/media/dma-sku-recommend-single-db-recommendations.png)

Per altri suggerimenti di istanza gestita, il file di output TSV apparirà come segue:

![File di istanza gestita di PowerShell illustrato nella cartella DMA](../dma/media/dma-sku-recommend-mi-recommendations.png)

Segue una descrizione di ogni colonna nel file di output.

- **DatabaseName** -il nome del database.
- **MetricType** -Database SQL di Azure consiglia di singola/gestita di database dell'istanza livello.
- **MetricValue** -Database SQL di Azure consiglia di singola/gestita di database dell'istanza SKU.
- **PricePerMonth** : il prezzo stimato al mese per lo SKU corrispondente.
- **RegionName** : il nome dell'area dello SKU corrispondente. 
- **IsTierRecommended** -rendiamo un minimo consigliato di SKU per ogni livello. È quindi possibile applicare l'euristica per determinare il livello più adatto per il database. Indica quale livello è consigliato per il database. 
- **ExclusionReasons** -questo valore è vuoto se un livello è consigliato. Per ogni livello che non è consigliato, offriamo i motivi il motivo per cui non è stato selezionato.
- **AppliedRules** -una notazione breve delle regole che sono state applicate.

Il livello consigliato finale (ad esempio, **MetricType**) e il valore (ad esempio, **MetricValue**)-trovato in cui il **IsTierRecommended** colonna è impostata su TRUE - riflette lo SKU minimo obbligatorio per le query da eseguire in Azure con una percentuale di successo simile ai database in locale. Per l'istanza gestita, DMA attualmente supporta le raccomandazioni per il più diffuso 8vcore ai 40vcore SKU. Ad esempio, se lo SKU minima consigliato è S4 per il livello standard, quindi scegliere S3 o di sotto verrà impedire il timeout delle query o un errore di esecuzione.

Il file HTML contiene queste informazioni in formato grafico. Un modo semplice per visualizzare l'indicazione finale e la parte successiva del processo di provisioning. Altre informazioni sull'output HTML sono nella sezione seguente.

## <a name="provision-recommended-skus-to-azure"></a>Effettuare il provisioning consigliati gli SKU in Azure

Con pochi clic, è possibile usare le raccomandazioni identificate alla destinazione di effettuare il provisioning SKU a in Azure a cui è possibile eseguire la migrazione dei database. È possibile utilizzare il file HTML per input di sottoscrizione di Azure; Selezionare il piano tariffario, calcolo livello e dimensioni massime dei dati per i database; e generare uno script per eseguire il provisioning dei database. È possibile eseguire questo script usando PowerShell.

È possibile eseguire questo processo in un singolo computer oppure è possibile eseguirla su più computer per determinare le raccomandazioni dello SKU su larga scala. DMA attualmente rende un'esperienza semplice e scalabile per supportare l'intero processo tramite l'interfaccia della riga di comando.

Per informazioni sul provisioning di input e apportare modifiche ai consigli, aggiornare il file HTML come indicato di seguito.

**Per consigli sul database singolo**

![Schermata di SKU consigli sul database di SQL Azure](../dma/media/dma-sku-recommend-single-db-recommendations1.png)

1. Aprire il file HTML e immettere le informazioni seguenti:
    - **ID sottoscrizione** -l'ID sottoscrizione della sottoscrizione di Azure a cui si desidera eseguire il provisioning dei database.
    - **Gruppo di risorse** -il gruppo di risorse a cui si desidera distribuire i database. Immettere un gruppo di risorse esistente.
    - **Area** -l'area in cui eseguire il provisioning di database. Assicurarsi che la propria sottoscrizione supporti il selezionare region.
    - **Nome del server** -server di Database SQL di Azure a cui si desidera che i database distribuiti. Se si immette un nome di server che non esiste, verrà creato.
    - **Admin Username** -nome utente amministratore del server.
    - **Password amministratore** -la password amministratore server. La password deve essere composta da almeno otto caratteri e non più di 128 caratteri. La password deve contenere caratteri di tre delle categorie seguenti: inglese lettere maiuscole, lettere minuscole, numeri (0-9) e caratteri non alfanumerici (!, $, #, %, e così via.). La password non può contenere tutto o parte (3 + consecutive lettere) dal nome utente.

2. Esaminare le raccomandazioni per ogni database e modificare il piano tariffario, livello e le dimensioni di dati max in base alle esigenze di calcolo. Assicurarsi di deselezionare tutti i database desiderati non attualmente effettuare il provisioning.

3. Selezionare **genera Script di Provisioning**, salvare lo script e quindi di eseguirlo in PowerShell.

    Questo processo deve creare tutti i database selezionati nella pagina HTML.

**Per le indicazioni di istanza gestita**

![Schermata di raccomandazioni SKU istanza Gestita di SQL Azure](../dma/media/dma-sku-recommend-mi-recommendations1.png)

1. Aprire il file HTML e immettere le informazioni seguenti:
    - **ID sottoscrizione** -l'ID sottoscrizione della sottoscrizione di Azure a cui si desidera eseguire il provisioning dei database.
    - **Gruppo di risorse** -il gruppo di risorse a cui si desidera distribuire i database. Immettere un gruppo di risorse esistente.
    - **Area** -l'area in cui eseguire il provisioning di database. Assicurarsi che la propria sottoscrizione supporti il selezionare region.
    - **Nome dell'istanza** – l'istanza di istanza gestita SQL di Azure a cui si desidera eseguire la migrazione dei database. Il nome dell'istanza può contenere solo lettere minuscole lettere, numeri e '-', ma non può iniziare o terminare con '-' o contenere più di 63 caratteri.
    - **Istanza Admin Username** : il nome utente amministratore di istanza. Assicurarsi che il nome di accesso soddisfi i requisiti seguenti: si tratta di un identificatore SQL e non un nome di sistema tipico (ad esempio admin, administrator, sa, root, dbmanager, loginmanager e così via), o un database incorporato utente o ruolo (ad esempio dbo, guest, public e così via). Assicurarsi che il nome non contiene spazi, caratteri Unicode o caratteri non alfabetici e che non inizia con numeri o simboli. 
    - **Password dell'amministratore dell'istanza** -la password di amministratore di istanza. La password deve contenere almeno 16 caratteri e non più di 128 caratteri. La password deve contenere caratteri di tre delle categorie seguenti: inglese lettere maiuscole, lettere minuscole, numeri (0-9) e caratteri non alfanumerici (!, $, #, %, e così via.). La password non può contenere tutto o parte (3 + consecutive lettere) dal nome utente.
    - **Nome della rete virtuale** : nome di rete virtuale in cui l'istanza gestita deve eseguire il provisioning. Immettere un nome di rete virtuale esistente.
    - **Nome della subnet** – nome la Subnet in cui l'istanza gestita deve eseguire il provisioning. Immettere un nome di Subnet esistente.

2. Esaminare le raccomandazioni per ogni istanza e modificare il piano tariffario, livello e le dimensioni di dati max in base alle esigenze di calcolo. Anche se le indicazioni sono attualmente limitate ai 8vcore ai 40vcore SKU, è ancora disponibile l'opzione per eseguire il provisioning 64vcore e 80vcore SKU se si desidera. Assicurarsi di deselezionare tutte le istanze che non attualmente si intende eseguire il provisioning.

    Questo processo deve creare tutti i database selezionati nella pagina HTML.

    > [!NOTE]
    > Creazione di istanze gestite in una subnet (soprattutto per la prima volta) potrebbe richiedere diverse ore. Dopo aver eseguito lo script di provisioning tramite PowerShell, è possibile controllare lo stato della distribuzione nel portale di Azure.

## <a name="next-step"></a>Passaggio successivo

- Per un elenco completo dei comandi per l'esecuzione DMA dal comando, vedere l'articolo [eseguito Data Migration Assistant da riga di comando](https://docs.microsoft.com/sql/dma/dma-commandline?view=sql-server-2017).
