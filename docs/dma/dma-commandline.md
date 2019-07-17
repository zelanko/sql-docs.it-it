---
title: Eseguire Data Migration Assistant dalla riga di comando (SQL Server) | Microsoft Docs
description: Informazioni su come eseguire Data Migration Assistant dalla riga di comando per valutare i database di SQL Server per la migrazione
ms.custom: ''
ms.date: 05/06/2019
ms.prod: sql
ms.prod_service: dma
ms.reviewer: ''
ms.technology: dma
ms.topic: conceptual
keywords: ''
helpviewer_keywords:
- Data Migration Assistant, Command Line
ms.assetid: ''
author: HJToland3
ms.author: rajpo
ms.openlocfilehash: ed669adc19dddc96ba953ba73f73805925968d19
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68058915"
---
# <a name="run-data-migration-assistant-from-the-command-line"></a>Eseguire Data Migration Assistant dalla riga di comando

La versione 2.1 e versioni successive, quando si installa Data Migration Assistant, viene installato anche in dmacmd.exe *% ProgramFiles %\\Microsoft Data Migration Assistant\\* . Usare dmacmd.exe per valutare i database in modalità automatica e restituire il risultato al file JSON o CSV. Questo metodo è particolarmente utile quando si valuta più database o database di grandi dimensioni. 

> [!NOTE]
> Dmacmd.exe supporta solo le valutazioni in esecuzione. In questo momento non sono supportate le migrazioni.

## <a name="assessments-using-the-command-line-interface-cli"></a>Valutazioni usando l'interfaccia della riga di comando (CLI)

```
DmaCmd.exe /AssessmentName="string"
/AssessmentDatabases="connectionString1" \["connectionString2"\]
\[/AssessmentSourcePlatform="SourcePlatform"]
\[/AssessmentTargetPlatform="TargetPlatform"\]
/AssessmentEvaluateRecommendations|/AssessmentEvaluateCompatibilityIssues
\[/AssessmentOverwriteResult\]
/AssessmentResultJson="file"|/AssessmentResultCsv="file"
```

|Argomento  |Descrizione  | Obbligatorio (Y/N)
|---------|---------|---------------|
| `/help or /?`     | Come usare il testo della Guida dmacmd.exe        | N
|`/AssessmentName`     |   Nome del progetto di valutazione   | Y
|`/AssessmentDatabases`     | Elenco delimitato da spazi delle stringhe di connessione. Nome del database (catalogo iniziale) è tra maiuscole e minuscole. | Y
|`/AssessmentSourcePlatform`     | Piattaforma di origine per la valutazione: <br>Valori supportati per la valutazione: SqlOnPrem, RdsSqlServer (impostazione predefinita) <br>Valori supportati per la valutazione della conformità di destinazione: SqlOnPrem, RdsSqlServer (impostazione predefinita), Cassandra (anteprima)   | N
|`/AssessmentTargetPlatform`     | Piattaforma di destinazione per la valutazione:  <br> Valori supportati per la valutazione: AzureSqlDatabase, ManagedSqlServer, SqlServer2012, SqlServer2014, SqlServer2016, SqlServerLinux2017 e SqlServerWindows2017 (impostazione predefinita)  <br> Valori supportati per la valutazione della conformità di destinazione: ManagedSqlServer (impostazione predefinita), COSMOS DB (anteprima)   | N
|`/AssessmentEvaluateFeatureParity`  | Eseguire le regole di parità di funzionalità. Se la piattaforma di origine è RdsSqlServer, valutazione parità delle funzionalità non è supportata per la piattaforma di destinazione AzureSqlDatabase  | N
|`/AssessmentEvaluateCompatibilityIssues`     | Eseguire le regole di compatibilità  | Y <br> (AssessmentEvaluateCompatibilityIssues o AssessmentEvaluateRecommendations è obbligatorio.)
|`/AssessmentEvaluateRecommendations`     | Eseguire funzionalità consigliate        | Y <br> (È necessario AssessmentEvaluateCompatibilityIssues o AssessmentEvaluateRecommendations)
|`/AssessmentOverwriteResult`     | Sovrascrivere il file dei risultati    | N
|`/AssessmentResultJson`     | Percorso completo del file di risultati JSON     | Y <br> (È necessario AssessmentResultJson o AssessmentResultCsv)
|`/AssessmentResultCsv`    | Percorso completo del file di risultati CSV   | Y <br> (È necessario AssessmentResultJson o AssessmentResultCsv)
|`/Action`    | Usare SkuRecommendation per ottenere le raccomandazioni dello SKU, usare AssessTargetReadiness per eseguire una valutazione della conformità di destinazione.   | N
|`/SourceConnections`    | Elenco delimitato da spazi delle stringhe di connessione. Nome del database (catalogo iniziale) è facoltativo. Se non viene specificato alcun nome di database, vengono valutati tutti i database di origine.   | Y <br> (Obbligatorio se l'azione è 'AssessTargetReadiness')
|`/TargetReadinessConfiguration`    | Percorso completo del file XML che descrive i valori per nome, le connessioni alle origini e il file dei risultati.   | Y <br> (È necessario TargetReadinessConfiguration o SourceConnections)
|`/FeatureDiscoveryReportJson`    | Percorso per l'individuazione della funzionalità report JSON. Se questo file viene generato, quindi può essere utilizzato per eseguire di nuovo la valutazione della conformità destinazione senza stabilire la connessione all'origine. | N
|`/ImportFeatureDiscoveryReportJson`    | Percorso del report JSON di individuazione funzionalità creato in precedenza. Invece di connessioni all'origine, questo file verrà utilizzato.   | N

## <a name="examples-of-assessments-using-the-cli"></a>Esempi di valutazioni usando l'interfaccia della riga di comando

**Dmacmd.exe**

  `Dmacmd.exe /? or DmaCmd.exe /help`

**Valutazione di un singolo database usando regole di compatibilità in esecuzione e l'autenticazione di Windows**

```
DmaCmd.exe /AssessmentName="TestAssessment"
/AssessmentDatabases="Server=SQLServerInstanceName;Initial
Catalog=DatabaseName;Integrated Security=true"
/AssessmentEvaluateCompatibilityIssues /AssessmentOverwriteResult
/AssessmentResultJson="C:\\temp\\Results\\AssessmentReport.json"
```

**Valutazione di un singolo database usando suggerimento di funzionalità di autenticazione e in esecuzione SQL Server**

```
DmaCmd.exe /AssessmentName="TestAssessment"
/AssessmentDatabases="Server=SQLServerInstanceName;Initial
Catalog=DatabaseName;User Id=myUsername;Password=myPassword;"
/AssessmentEvaluateRecommendations /AssessmentOverwriteResult
/AssessmentResultCsv="C:\\temp\\Results\\AssessmentReport.csv"
```

**Valutazione di un singolo database per la piattaforma di destinazione SQL Server 2012, salvare i risultati nel file con estensione JSON e CSV**

```
DmaCmd.exe /AssessmentName="TestAssessment"
/AssessmentDatabases="Server=SQLServerInstanceName;Initial
Catalog=DatabaseName;Integrated Security=true"
/AssessmentTargetPlatform="SqlServer2012"
/AssessmentEvaluateRecommendations /AssessmentOverwriteResult
/AssessmentResultJson="C:\\temp\\Results\\AssessmentReport.json"
/AssessmentResultCsv="C:\\temp\\Results\\AssessmentReport.csv"
```

**Valutazione di un singolo database per la piattaforma di destinazione Database di SQL Azure, salvare i risultati nel file con estensione JSON e CSV**

```
DmaCmd.exe /AssessmentName="TestAssessment" 
/AssessmentDatabases="Server=SQLServerInstanceName;Initial
Catalog=DatabaseName;Integrated Security=true"
/AssessmentTargetPlatform="AzureSqlDatabaseV12"
/AssessmentEvaluateCompatibilityIssues /AssessmentEvaluateFeatureParity
/AssessmentOverwriteResult 
/AssessmentResultCsv="C:\\temp\\AssessmentReport.csv" 
/AssessmentResultJson="C:\\temp\\AssessmentReport.json"
```

**Valutazione di più database**

```
DmaCmd.exe /AssessmentName="TestAssessment"
/AssessmentDatabases="Server=SQLServerInstanceName1;Initial
Catalog=DatabaseName1;Integrated Security=true"
"Server=SQLServerInstanceName1;Initial Catalog=DatabaseName2;Integrated
Security=true" "Server=SQLServerInstanceName2;Initial
Catalog=DatabaseName3;Integrated Security=true"
/AssessmentTargetPlatform="SqlServer2016"
/AssessmentEvaluateCompatibilityIssues /AssessmentOverwriteResult
/AssessmentResultCsv="C:\\temp\\Results\\AssessmentReport.csv"
/AssessmentResultJson="C:\\Results\\test2016.json"
```

**Valutazione della conformità di destinazione di un singolo database usando l'autenticazione di Windows**

```
DmaCmd.exe /Action=AssessTargetReadiness 
/AssessmentName="TestAssessment" 
/SourceConnections="Server=SQLServerInstanceName;Initial Catalog=DatabaseName;Integrated Security=true" 
/AssessmentOverwriteResult 
/AssessmentResultJson="C:\temp\Results\AssessmentReport.json"
```

**Valutazione della conformità di destinazione di un singolo database tramite autenticazione di SQL Server**

```
DmaCmd.exe /Action=AssessTargetReadiness 
/AssessmentName="TestAssessment" 
/SourceConnections="Server=SQLServerInstanceName;Initial Catalog=DatabaseName;User Id=myUsername;Password=myPassword;" /AssessmentEvaluateRecommendations 
/AssessmentOverwriteResult 
/AssessmentResultJson="C:\temp\Results\AssessmentReport.json" 

```

**Valutazione di un singolo database per la piattaforma di destinazione Database di SQL Azure, salvare i risultati nel file con estensione JSON e CSV**

```
DmaCmd.exe /AssessmentName="TestAssessment" 
/AssessmentDatabases="Server=SQLServerInstanceName;Initial
Catalog=DatabaseName;Integrated Security=true"
/AssessmentSourcePlatform="SqlOnPrem"
/AssessmentTargetPlatform="AzureSqlDatabase"
/AssessmentEvaluateCompatibilityIssues /AssessmentEvaluateFeatureParity
/AssessmentOverwriteResult 
/AssessmentResultCsv="C:\\temp\\AssessmentReport.csv" 
/AssessmentResultJson="C:\\temp\\AssessmentReport.json"

```

**Valutazione della conformità di destinazione di più database**

```
DmaCmd.exe /Action=AssessTargetReadiness
/AssessmentName="TestAssessment"
/AssessmentSourcePlatform=SourcePlatform
/AssessmentTargetPlatform=TargetPlatform
/SourceConnections="Server=SQLServerInstanceName1;Initial Catalog=DatabaseName1;Integrated Security=true" "Server=SQLServerInstanceName1;Initial Catalog=DatabaseName2;Integrated Security=true" "Server=SQLServerInstanceName2;Initial Catalog=DatabaseName3;Integrated Security=true"
/AssessmentOverwriteResult  
/AssessmentResultJson="C:\Results\test2016.json"

(/AssessmentSourcePlatform and /AssessmentTargetPlatform are optional.)
```

**Valutazione della conformità per tutti i database in un server utilizzando l'autenticazione di Windows di destinazione**

```
DmaCmd.exe /Action=AssessTargetReadiness
/AssessmentName="TestAssessment"
/SourceConnections="Server=SQLServerInstanceName;Integrated Security=true"
/AssessmentOverwriteResult
/AssessmentResultJson="C:\temp\Results\AssessmentReport.json"

```

**Valutazione della conformità di destinazione mediante l'importazione di report sull'individuazione funzionalità creata in precedenza**

```
DmaCmd.exe /Action=AssessTargetReadiness
/AssessmentName="TestAssessment"
/ImportFeatureDiscoveryReportJson="c:\temp\feature_report.json" 
/AssessmentOverwriteResult
/AssessmentResultJson="C:\temp\Results\AssessmentReport.json"

```

**Valutazione della conformità di destinazione, fornendo i file di configurazione**

```
DmaCmd.exe /Action=AssessTargetReadiness 
/TargetReadinessConfiguration=.\Config.xml
```

Contenuto del file di configurazione quando si usano le connessioni alle origini:

```
<?xml version="1.0" encoding="utf-8" ?>
<TargetReadinessConfiguration xmlns="http://microsoft.com/schemas/SqlServer/Advisor/TargetReadinessConfiguration">
  <AssessmentName>name</AssessmentName>
  <SourcePlatform>Source Platform</SourcePlatform> <!-- Optional. The default is SqlOnPrem -->
  <TargetPlatform>TargetPlatform</TargetPlatform> <!-- Optional. The default is ManagedSqlServer -->
  <SourceConnections>
    <SourceConnection>connection string 1</SourceConnection>
    <SourceConnection>connection string 2</SourceConnection>
    <!-- ... -->
    <SourceConnection>connection string n</SourceConnection>
  </SourceConnections>
  <AssessmentResultJson>path\to\file.json</AssessmentResultJson>
  <FeatureDiscoveryReportJson>path\to\featurediscoveryreport.json</FeatureDiscoveryReportJson>
  <OverwriteResult>true</OverwriteResult> <!-- or false -->
</TargetReadinessConfiguration>
```

Contenuto del file di configurazione durante l'importazione di report sull'individuazione delle funzionalità:

```
<TargetReadinessConfiguration xmlns="http://microsoft.com/schemas/SqlServer/Advisor/TargetReadinessConfiguration">
  <AssessmentName>name</AssessmentName>
  <ImportFeatureDiscoveryReportJson>path\to\featurediscoveryfile.json</ImportFeatureDiscoveryReportJson>
  <AssessmentResultJson>path\to\resultfile.json</AssessmentResultJson>
  <OverwriteResult>true</OverwriteResult><!-- or false -->
</TargetReadinessConfiguration>
```

## <a name="azure-sql-databasemanaged-instance-sku-recommendations-using-the-cli"></a>SQL/gestita di Database istanza SKU API recommendations di Azure usando l'interfaccia della riga di comando

I comandi seguenti supportano le raccomandazioni per il database singolo Database SQL di Azure e le opzioni di distribuzione di istanza gestita.

```
.\DmaCmd.exe /Action=SkuRecommendation
/SkuRecommendationInputDataFilePath="C:\TestOut\out.csv"
/SkuRecommendationTsvOutputResultsFilePath="C:\TestOut\prices.tsv"
/SkuRecommendationJsonOutputResultsFilePath="C:\TestOut\prices.json"
/SkuRecommendationOutputResultsFilePath="C:\TestOut\prices.html"
/SkuRecommendationPreventPriceRefresh=true 
```

|Argomento  |Descrizione  | Obbligatorio (Y/N)
|---------|---------|---------------|
|`/Action=SkuRecommendation` | Eseguire la valutazione dello SKU utilizzando la riga di comando DMA | Y
|`/SkuRecommendationInputDataFilePath` | Percorso completo del file del contatore delle prestazioni raccolti dai computer che ospita i database | Y
|`/SkuRecommendationTsvOutputResultsFilePath` | Percorso completo del file dei risultati TSV | Y <br> (Richiede il percorso del file TSV o JSON o HTML)
|`/SkuRecommendationJsonOutputResultsFilePath` | Percorso completo del file di risultati JSON | Y <br> (Richiede il percorso del file TSV o JSON o HTML)
|`/SkuRecommendationHtmlResultsFilePath` | Percorso completo del file di risultati HTML | Y <br> (Richiede il percorso del file TSV o JSON o HTML)
|`/SkuRecommendationPreventPriceRefresh` | Impedisce l'aggiornamento di prezzo. Usare se in esecuzione in modalità offline (ad esempio, true). | Y <br> (Selezionare entrambi in questo argomento per i prezzi statici o tutti gli argomenti seguenti devono essere selezionati per ottenere i prezzi più recenti)
|`/SkuRecommendationCurrencyCode` | La valuta in cui visualizzare i prezzi (ad esempio "USD") | Y <br> (Per i prezzi più recenti)
|`/SkuRecommendationOfferName` | L'offerta assegnare un nome (ad esempio "MS-AZR-0003P"). Per altre informazioni, vedere la [dettagli dell'offerta Microsoft Azure](https://azure.microsoft.com/support/legal/offer-details/) pagina. | Y <br> (Per i prezzi più recenti)
|`/SkuRecommendationRegionName` | L'area assegnare un nome (ad esempio "Stati Uniti occidentali") | Y <br> (Per i prezzi più recenti)
|`/SkuRecommendationSubscriptionId` | ID della sottoscrizione. | Y <br> (Per i prezzi più recenti)
|`/SkuRecommendationDatabasesToRecommend` | Elenco delimitato da spazi dei database (ad esempio, è consigliabile per "Database1" "Database2" "Database3"). I nomi sono tra maiuscole e minuscole e devono essere racchiuso tra virgolette doppie. Se omesso, vengono fornite indicazioni per tutti i database. | N
|`/AzureAuthenticationTenantId` | Il tenant di autenticazione. | Y <br> (Per i prezzi più recenti)
|`/AzureAuthenticationClientId` | L'ID client dell'app AAD usato per l'autenticazione. | Y <br> (Per i prezzi più recenti)
|`/AzureAuthenticationInteractiveAuthentication` | Impostare su true per le finestre popup. | Y <br> (Per i prezzi più recenti) <br>(Selezionare una delle opzioni di 3 autenticazione - opzione 1)
|`/AzureAuthenticationCertificateStoreLocation` | Impostare il percorso dell'archivio certificati (ad esempio "CurrentUser"). | Y <br>(Per i prezzi più recenti) <br> (Selezionare una delle opzioni di 3 autenticazione - opzione 2)
|`/AzureAuthenticationCertificateThumbprint` | Impostare l'identificazione personale del certificato. | Y <br> (Per i prezzi più recenti) <br>(Selezionare una delle opzioni di 3 autenticazione - opzione 2)
|`/AzureAuthenticationToken` | Impostare per il token di certificato. | Y <br> (Per i prezzi più recenti) <br>(Selezionare una delle opzioni di 3 autenticazione - opzione 3)

## <a name="examples-of-sku-assessments-using-the-cli"></a>Esempi di valutazioni della SKU usando l'interfaccia della riga di comando

**Dmacmd.exe**

`Dmacmd.exe /? or DmaCmd.exe /help`

**Suggerimento di SKU/istanza Gestita di database SQL di Azure con l'aggiornamento di prezzo (prezzi più recenti in get -) autenticazione interattiva** 

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
/AzureAuthenticationClientId=<Your AzureAuthenticationClientId>
/AzureAuthenticationTenantId=<Your AzureAuthenticationTenantId>
/AzureAuthenticationInteractiveAuthentication=true 
```

**Suggerimento di SKU/istanza Gestita di database SQL di Azure con l'aggiornamento di prezzo (prezzi più recenti) get - autenticazione del certificato**

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
/AzureAuthenticationClientId=<Your AzureAuthenticationClientId>
/AzureAuthenticationTenantId=<Your AzureAuthenticationTenantId>
/AzureAuthenticationCertificateStoreLocation=<Your Certificate Store Location>
/AzureAuthenticationCertificateThumbprint=<Your Certificate Thumbprint>  
```

**L'autenticazione del Token e specificare i database per consigliare di suggerimento di SKU DB SQL/istanza Gestita di Azure con l'aggiornamento di prezzo (prezzi più recenti in get)**
  
```
.\DmaCmd.exe /Action=SkuRecommendation
/SkuRecommendationInputDataFilePath="C:\TestOut\out.csv"
/SkuRecommendationTsvOutputResultsFilePath="C:\TestOut\prices.tsv"
/SkuRecommendationJsonOutputResultsFilePath="C:\TestOut\prices.json"
/SkuRecommendationOutputResultsFilePath="C:\TestOut\prices.html"
/SkuRecommendationCurrencyCode=USD
/SkuRecommendationOfferName=MS-AZR-0044p
/SkuRecommendationRegionName=UKWest
/SkuRecommendationDatabasesToRecommend=“TPCDS1G,EDW_3G,TPCDS10G”
/SkuRecommendationSubscriptionId=<Your Subscription Id>
/AzureAuthenticationClientId=<Your AzureAuthenticationClientId>
/AzureAuthenticationTenantId=<Your AzureAuthenticationTenantId>
/AzureAuthenticationToken=<Your Authentication Token> 
```

**Suggerimento di SKU/istanza Gestita di database SQL di Azure senza aggiornamento prezzo (usare statico prezzi)** 
```
.\DmaCmd.exe /Action=SkuRecommendation
/SkuRecommendationInputDataFilePath="C:\TestOut\out.csv"
/SkuRecommendationTsvOutputResultsFilePath="C:\TestOut\prices.tsv"
/SkuRecommendationJsonOutputResultsFilePath="C:\TestOut\prices.json"
/SkuRecommendationOutputResultsFilePath="C:\TestOut\prices.html"
/SkuRecommendationPreventPriceRefresh=true  
```

## <a name="see-also"></a>Vedere anche
- [Data Migration Assistant](https://aka.ms/get-dma) scaricare.
- L'articolo [identificare lo SKU del Database SQL di Azure corretto per il database locale](https://aka.ms/dma-sku-recommend-sqldb).
