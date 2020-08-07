---
title: Esegui Data Migration Assistant dalla riga di comando
description: Informazioni su come eseguire Data Migration Assistant dalla riga di comando per valutare SQL Server database per la migrazione
ms.custom: seo-lt-2019
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
author: rajeshsetlem
ms.author: rajpo
ms.openlocfilehash: 0b589d9f5bf90b78d6689ff3b37f09f15fe344b8
ms.sourcegitcommit: 21bedbae28840e2f96f5e8b08bcfc794f305c8bc
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/06/2020
ms.locfileid: "87864918"
---
# <a name="run-data-migration-assistant-from-the-command-line"></a>Esegui Data Migration Assistant dalla riga di comando

Con la versione 2,1 e successive, quando si installa Data Migration Assistant, viene installato anche dmacmd.exe in *% ProgramFiles% \\ Microsoft Data Migration Assistant \\ *. Usare dmacmd.exe per valutare i database in modalità automatica e restituire il risultato in un file JSON o CSV. Questo metodo è particolarmente utile per la valutazione di più database o database di grandi dimensioni. 

> [!NOTE]
> Dmacmd.exe supporta solo le valutazioni in esecuzione. In questo momento le migrazioni non sono supportate.

## <a name="assessments-using-the-command-line-interface-cli"></a>Valutazioni tramite l'interfaccia della riga di comando (CLI)

```
DmaCmd.exe /AssessmentName="string"
/AssessmentDatabases="connectionString1" \["connectionString2"\]
\[/AssessmentSourcePlatform="SourcePlatform"]
\[/AssessmentTargetPlatform="TargetPlatform"\]
/AssessmentEvaluateRecommendations|/AssessmentEvaluateCompatibilityIssues
\[/AssessmentOverwriteResult\]
/AssessmentResultJson="file"|/AssessmentResultCsv="file"
```

|Argomento  |Description  | Obbligatorio (Y/N)
|---------|---------|---------------|
| `/help or /?`     | Come usare dmacmd.exe testo della Guida        | N
|`/AssessmentName`     |   Nome del progetto di valutazione   | S
|`/AssessmentDatabases`     | Elenco delimitato da spazi di stringhe di connessione. Il nome del database (catalogo iniziale) fa distinzione tra maiuscole e minuscole. | S
|`/AssessmentSourcePlatform`     | Piattaforma di origine per la valutazione: <br>Valori supportati per assessment: SqlOnPrem, RdsSqlServer (impostazione predefinita) <br>Valori supportati per la valutazione della conformità della destinazione: SqlOnPrem, RdsSqlServer (impostazione predefinita), Cassandra (anteprima)   | N
|`/AssessmentTargetPlatform`     | Piattaforma di destinazione per la valutazione:  <br> Valori supportati per la valutazione: AzureSqlDatabase, ManagedSqlServer, SqlServer2012, SqlServer2014, SqlServer2016, SqlServerLinux2017 e SqlServerWindows2017 (impostazione predefinita)  <br> Valori supportati per la valutazione della conformità della destinazione: ManagedSqlServer (impostazione predefinita), CosmosDB (anteprima)   | N
|`/AssessmentEvaluateFeatureParity`  | Eseguire le regole di parità delle funzionalità. Se la piattaforma di origine è RdsSqlServer, la valutazione della parità delle funzionalità non è supportata per la piattaforma di destinazione AzureSqlDatabase  | N
|`/AssessmentEvaluateCompatibilityIssues`     | Eseguire le regole di compatibilità  | S <br> È necessario specificare AssessmentEvaluateCompatibilityIssues o AssessmentEvaluateRecommendations.
|`/AssessmentEvaluateRecommendations`     | Suggerimenti sulle funzionalità di esecuzione        | S <br> (È necessario specificare AssessmentEvaluateCompatibilityIssues o AssessmentEvaluateRecommendations)
|`/AssessmentOverwriteResult`     | Sovrascrivi il file di risultati    | N
|`/AssessmentResultJson`     | Percorso completo del file dei risultati JSON     | S <br> (È necessario specificare AssessmentResultJson o AssessmentResultCsv)
|`/AssessmentResultCsv`    | Percorso completo del file dei risultati CSV   | S <br> (È necessario specificare AssessmentResultJson o AssessmentResultCsv)
|`/AssessmentResultDma`    | Percorso completo del file dei risultati DMA   | N
|`/Action`    | Usare SkuRecommendation per ottenere le raccomandazioni dello SKU. <br> Usare AssessTargetReadiness per eseguire la valutazione della conformità della destinazione. <br> Usare AzureMigrateUpload per caricare tutti i file di valutazione DMA nel AzzessmentResultInputFolder per il caricamento bulk in Azure Migrate. tipo di azione utilizzo/Action = AzureMigrateUpload   | N
|`/SourceConnections`    | Elenco delimitato da spazi di stringhe di connessione. Il nome del database (catalogo iniziale) è facoltativo. Se non viene specificato alcun nome di database, vengono valutati tutti i database nell'origine.   | S <br> (Obbligatorio se Action è' AssessTargetReadiness ')
|`/TargetReadinessConfiguration`    | Percorso completo del file XML che descrive i valori per il nome, le connessioni di origine e il file di risultati.   | S <br> (È necessario specificare TargetReadinessConfiguration o SourceConnections)
|`/FeatureDiscoveryReportJson`    | Percorso del report JSON di individuazione delle funzionalità. Se questo file viene generato, può essere usato per eseguire nuovamente la valutazione della conformità della destinazione senza connettersi all'origine. | N
|`/ImportFeatureDiscoveryReportJson`    | Percorso del report JSON di individuazione delle funzionalità creato in precedenza. Questo file verrà usato anziché le connessioni di origine.   | N
|`/EnableAssessmentUploadToAzureMigrate`    | Consente di caricare e pubblicare i risultati della valutazione in Azure Migrate   | N
|`/AzureCloudEnvironment`    |Seleziona l'ambiente cloud di Azure a cui connettersi, il valore predefinito è il cloud pubblico di Azure. Valori supportati: Azure (impostazione predefinita), AzureChina, AzureGermany, AzureUSGovernment.   | N 
|`/SubscriptionId`    |ID sottoscrizione di Azure.   | S <br> (Obbligatorio se è specificato l'argomento EnableAssessmentUploadToAzureMigrate)
|`/AzureMigrateProjectName`    |Nome del progetto Azure Migrate in cui caricare i risultati della valutazione.   | S <br> (Obbligatorio se è specificato l'argomento EnableAssessmentUploadToAzureMigrate)
|`/ResourceGroupName`    |Azure Migrate nome del gruppo di risorse.   | S <br> (Obbligatorio se è specificato l'argomento EnableAssessmentUploadToAzureMigrate)
|`/AssessmentResultInputFolder`    |Percorso della cartella di input che contiene. File di valutazione DMA da caricare in Azure Migrate.   | S <br> (Obbligatorio se l'azione è AzureMigrateUpload)



## <a name="examples-of-assessments-using-the-cli"></a>Esempi di valutazioni usando l'interfaccia della riga di comando

**Dmacmd.exe**

  `Dmacmd.exe /? or DmaCmd.exe /help`

**Valutazione a database singolo utilizzando l'autenticazione di Windows e le regole di compatibilità esecuzione**

```
DmaCmd.exe /AssessmentName="TestAssessment"
/AssessmentDatabases="Server=SQLServerInstanceName;Initial
Catalog=DatabaseName;Integrated Security=true"
/AssessmentEvaluateCompatibilityIssues /AssessmentOverwriteResult
/AssessmentResultJson="C:\\temp\\Results\\AssessmentReport.json"
```

**Valutazione a database singolo utilizzando l'autenticazione SQL Server e la raccomandazione sulle funzionalità in esecuzione**

```
DmaCmd.exe /AssessmentName="TestAssessment"
/AssessmentDatabases="Server=SQLServerInstanceName;Initial
Catalog=DatabaseName;User Id=myUsername;Password=myPassword;"
/AssessmentEvaluateRecommendations /AssessmentOverwriteResult
/AssessmentResultCsv="C:\\temp\\Results\\AssessmentReport.csv"
```

**Valutazione a database singolo per la piattaforma di destinazione SQL Server 2012, salvare i risultati in un file con estensione JSON e CSV**

```
DmaCmd.exe /AssessmentName="TestAssessment"
/AssessmentDatabases="Server=SQLServerInstanceName;Initial
Catalog=DatabaseName;Integrated Security=true"
/AssessmentTargetPlatform="SqlServer2012"
/AssessmentEvaluateRecommendations /AssessmentOverwriteResult
/AssessmentResultJson="C:\\temp\\Results\\AssessmentReport.json"
/AssessmentResultCsv="C:\\temp\\Results\\AssessmentReport.csv"
```

**Valutazione a database singolo per il database di SQL Azure della piattaforma di destinazione, salvare i risultati in un file con estensione JSON e CSV**

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

**Valutazione della conformità della destinazione a database singolo usando l'autenticazione di Windows**

```
DmaCmd.exe /Action=AssessTargetReadiness 
/AssessmentName="TestAssessment" 
/SourceConnections="Server=SQLServerInstanceName;Initial Catalog=DatabaseName;Integrated Security=true" 
/AssessmentOverwriteResult 
/AssessmentResultJson="C:\temp\Results\AssessmentReport.json"
```

**Valutazione della conformità della destinazione a database singolo con autenticazione SQL Server**

```
DmaCmd.exe /Action=AssessTargetReadiness 
/AssessmentName="TestAssessment" 
/SourceConnections="Server=SQLServerInstanceName;Initial Catalog=DatabaseName;User Id=myUsername;Password=myPassword;" /AssessmentEvaluateRecommendations 
/AssessmentOverwriteResult 
/AssessmentResultJson="C:\temp\Results\AssessmentReport.json" 

```

**Valutazione a database singolo per il database di SQL Azure della piattaforma di destinazione, salvare i risultati in un file con estensione JSON e CSV**

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

**Valutazione della conformità della destinazione per più database**

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

**Valutazione della conformità della destinazione per tutti i database in un server tramite l'autenticazione di Windows**

```
DmaCmd.exe /Action=AssessTargetReadiness
/AssessmentName="TestAssessment"
/SourceConnections="Server=SQLServerInstanceName;Integrated Security=true"
/AssessmentOverwriteResult
/AssessmentResultJson="C:\temp\Results\AssessmentReport.json"

```

**Valutazione della conformità di destinazione importando il report di individuazione delle funzionalità creato in precedenza**

```
DmaCmd.exe /Action=AssessTargetReadiness
/AssessmentName="TestAssessment"
/ImportFeatureDiscoveryReportJson="c:\temp\feature_report.json" 
/AssessmentOverwriteResult
/AssessmentResultJson="C:\temp\Results\AssessmentReport.json"

```

**Valutazione della conformità della destinazione fornendo un file di configurazione**

```
DmaCmd.exe /Action=AssessTargetReadiness 
/TargetReadinessConfiguration=.\Config.xml
```

Contenuto del file di configurazione quando si usano le connessioni di origine:

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

Contenuto del file di configurazione durante l'importazione del report di individuazione delle funzionalità:

```
<TargetReadinessConfiguration xmlns="https://microsoft.com/schemas/SqlServer/Advisor/TargetReadinessConfiguration">
  <AssessmentName>name</AssessmentName>
  <ImportFeatureDiscoveryReportJson>path\to\featurediscoveryfile.json</ImportFeatureDiscoveryReportJson>
  <AssessmentResultJson>path\to\resultfile.json</AssessmentResultJson>
  <OverwriteResult>true</OverwriteResult><!-- or false -->
</TargetReadinessConfiguration>
```
**Valutare e caricare Azure Migrate nel cloud pubblico di Azure (impostazione predefinita)**
```
DmaCmd.exe
/Action="Assess" 
/AssessmentSourcePlatform=SqlOnPrem 
/AssessmentTargetPlatform=ManagedSqlServer
/AssessmentEvaluateCompatibilityIssues 
/AssessmentEvaluateRecommendations 
/AssessmentEvaluateFeatureParity 
/AssessmentOverwriteResult 
/AssessmentName="assess-myDatabase"
/AssessmentDatabases="Server=myServer;Initial Catalog=myDatabase;Integrated Security=true" 
/AssessmentResultDma="C:\assessments\results\assess-1.dma"
/SubscriptionId="Subscription Id" 
/AzureMigrateProjectName="Azure Migrate project ame" 
/ResourceGroupName="Resource Group name" 
/AzureAuthenticationInteractiveAuthentication
/AzureAuthenticationTenantId="Azure Tenant Id"
/EnableAssessmentUploadToAzureMigrate

```
**Caricamento batch dei file di valutazione DMA per Azure Migrate nel cloud pubblico di Azure (impostazione predefinita)**
```
DmaCmd.exe 
/Action="AzureMigrateUpload" 
/AssessmentResultInputFolder="C:\assessments\results" 
/SubscriptionId="Subscription Id" 
/AzureMigrateProjectName="Azure Migrate project name" 
/ResourceGroupName="Resource Group name" 
/AzureAuthenticationInteractiveAuthentication
/AzureAuthenticationTenantId="Azure Tenant Id"
/EnableAssessmentUploadToAzureMigrate

```
## <a name="azure-sql-database--azure-sql-managed-instance-sku-recommendations-using-the-cli"></a>Suggerimenti relativi al database SQL di Azure/Azure SQL Istanza gestita SKU usando l'interfaccia della riga di comando

Questi comandi supportano consigli per le opzioni di distribuzione di database singolo di database SQL di Azure e di Azure SQL Istanza gestita.

```
.\DmaCmd.exe /Action=SkuRecommendation
/SkuRecommendationInputDataFilePath="C:\TestOut\out.csv"
/SkuRecommendationTsvOutputResultsFilePath="C:\TestOut\prices.tsv"
/SkuRecommendationJsonOutputResultsFilePath="C:\TestOut\prices.json"
/SkuRecommendationOutputResultsFilePath="C:\TestOut\prices.html"
/SkuRecommendationPreventPriceRefresh=true 
```

|Argomento  |Description  | Obbligatorio (Y/N)
|---------|---------|---------------|
|`/Action=SkuRecommendation` | Eseguire la valutazione dello SKU usando la riga di comando DMA | S
|`/SkuRecommendationInputDataFilePath` | Percorso completo del file del contatore delle prestazioni raccolto dal computer che ospita i database | S
|`/SkuRecommendationTsvOutputResultsFilePath` | Percorso completo del file dei risultati TSV | S <br> (Richiede il formato TSV o JSON o il percorso del file HTML)
|`/SkuRecommendationJsonOutputResultsFilePath` | Percorso completo del file dei risultati JSON | S <br> (Richiede il formato TSV o JSON o il percorso del file HTML)
|`/SkuRecommendationHtmlResultsFilePath` | Percorso completo del file dei risultati HTML | S <br> (Richiede il formato TSV o JSON o il percorso del file HTML)
|`/SkuRecommendationPreventPriceRefresh` | Impedisce l'aggiornamento del prezzo. Usare se è in esecuzione in modalità offline (ad esempio, true). | S <br> (Selezionare questo argomento per i prezzi statici o tutti gli argomenti riportati di seguito devono essere selezionati per ottenere i prezzi più recenti)
|`/SkuRecommendationCurrencyCode` | La valuta in cui visualizzare i prezzi (ad esempio "USD") | S <br> (Per i prezzi più recenti)
|`/SkuRecommendationOfferName` | Nome dell'offerta (ad esempio, "MS-AZR-0003P"). Per ulteriori informazioni, vedere la pagina dei [Dettagli dell'offerta Microsoft Azure](https://azure.microsoft.com/support/legal/offer-details/) . | S <br> (Per i prezzi più recenti)
|`/SkuRecommendationRegionName` | Nome dell'area (ad esempio "Westus") | S <br> (Per i prezzi più recenti)
|`/SkuRecommendationSubscriptionId` | ID della sottoscrizione. | S <br> (Per i prezzi più recenti)
|`/SkuRecommendationDatabasesToRecommend` | Elenco di database separati da spazi da consigliare (ad esempio "Database1" "Database2" "Database3"). I nomi fanno distinzione tra maiuscole e minuscole e devono essere racchiusi tra virgolette doppie. Se omesso, vengono fornite indicazioni per tutti i database. | N
|`/AzureAuthenticationTenantId` | Tenant di autenticazione. | S <br> (Per i prezzi più recenti)
|`/AzureAuthenticationClientId` | ID client dell'app AAD usata per l'autenticazione. | S <br> (Per i prezzi più recenti)
|`/AzureAuthenticationInteractiveAuthentication` | Impostare su true per visualizzare la finestra. | S <br> (Per i prezzi più recenti) <br>(Scegliere una delle 3 opzioni di autenticazione-opzione 1)
|`/AzureAuthenticationCertificateStoreLocation` | Impostare sul percorso dell'archivio certificati, ad esempio "CurrentUser". | S <br>(Per i prezzi più recenti) <br> (Scegliere una delle 3 opzioni di autenticazione-opzione 2)
|`/AzureAuthenticationCertificateThumbprint` | Impostare sull'identificazione personale del certificato. | S <br> (Per i prezzi più recenti) <br>(Scegliere una delle 3 opzioni di autenticazione-opzione 2)
|`/AzureAuthenticationToken` | Impostare sul token del certificato. | S <br> (Per i prezzi più recenti) <br>(Scegliere una delle 3 opzioni di autenticazione-opzione 3)

## <a name="examples-of-sku-assessments-using-the-cli"></a>Esempi di valutazioni dello SKU con l'interfaccia della riga di comando

**Dmacmd.exe**

`Dmacmd.exe /? or DmaCmd.exe /help`

**Database SQL di Azure/raccomandazione SKU di Azure SQL Istanza gestita con aggiornamento prezzi (ottenere i prezzi più recenti)-autenticazione interattiva** 

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

**Database SQL di Azure/raccomandazione SKU di Azure SQL Istanza gestita con aggiornamento prezzi (ottenere i prezzi più recenti)-autenticazione del certificato**

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

**Database SQL di Azure/Azure SQL Istanza gestita raccomandazione con aggiornamento prezzi (ottenere i prezzi più recenti)-autenticazione token e specificare i database da consigliare**
  
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

**Database SQL di Azure/raccomandazione SKU di Azure SQL Istanza gestita senza aggiornamento prezzi (usare i prezzi statici)** 
```
.\DmaCmd.exe /Action=SkuRecommendation
/SkuRecommendationInputDataFilePath="C:\TestOut\out.csv"
/SkuRecommendationTsvOutputResultsFilePath="C:\TestOut\prices.tsv"
/SkuRecommendationJsonOutputResultsFilePath="C:\TestOut\prices.json"
/SkuRecommendationOutputResultsFilePath="C:\TestOut\prices.html"
/SkuRecommendationPreventPriceRefresh=true  
```

## <a name="see-also"></a>Vedere anche
- Download [Data Migration Assistant](https://aka.ms/get-dma) .
- L'articolo [identifica lo SKU del database SQL di Azure appropriato per il database locale](https://aka.ms/dma-sku-recommend-sqldb).
