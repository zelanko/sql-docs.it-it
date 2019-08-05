---
title: Tipo di connessione Oracle (SSRS, Server di report di Power BI e Generatore report) | Microsoft Docs
ms.date: 07/26/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-data
ms.topic: conceptual
ms.assetid: 9db86dd2-beda-42d8-8af7-2629d58a8e3d
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 2942ad1432b2674ab0b9906b5ab6e2f07be83ae7
ms.sourcegitcommit: a154b3050b6e1993f8c3165ff5011ff5fbd30a7e
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 07/30/2019
ms.locfileid: "68632081"
---
# <a name="oracle-connection-type-ssrs-power-bi-report-server-and-report-builder"></a>Tipo di connessione Oracle (SSRS, Server di report di Power BI e Generatore report)

Per usare dati di un database Oracle nel report è necessario avere un set di dati basato su un'origine dati del report di tipo Oracle. Questo tipo di origine dati predefinita usa il provider di dati Oracle direttamente e richiede un componente software client Oracle. Questo articolo illustra come scaricare e installare i driver per Reporting Services, Server di report di Power BI e Generatore report.

## <a name="64-bit-drivers-for-the-report-servers"></a>driver a 64 bit per i server di report

Server di report di Power BI e SQL Server Reporting Services 2016 e 2017 utilizzano tutti ODP.NET gestiti. I passaggi seguenti sono necessari solo per quando si usano i driver 18x più recenti. Si presuppone che i file siano stati installati in c:\oracle64.

1. Nel sito di download Oracle, installare Oracle [64 bit ODAC Oracle Universal Installer (OUI)](https://www.oracle.com/technetwork/topics/dotnet/downloads/odacdeploy-4242173.html). 
2. Registrare il client gestito ODP.NET nella GAC: C:\oracle64\product\18.0.0\client_1\odp.net\bin\4\OraProvCfg.exe/Action: GAC/ProviderPath: C:\oracle64\product\18.0.0\client_1\odp.net\managed\common\Oracle.ManagedDataAccess.dll
3. Aggiungere le voci client gestite di ODP.NET a Machine. config: C:\oracle64\product\18.0.0\client_1\odp.net\bin\4\OraProvCfg.exe/Action: config/Force/Product: odpm/frameworkVersion: v 4.0.30319/ProductVersion: 4.122.18.3

## <a name="32-bit-drivers-for-report-builder"></a>driver a 32 bit per Generatore report
I passaggi seguenti sono necessari solo per quando si usano i driver 18x più recenti. Si presuppone che i file siano stati installati in c:\oracle32.

1. Nel sito di download Oracle, installare Oracle [32 bit ODAC Oracle Universal Installer (OUI)](https://www.oracle.com/technetwork/topics/dotnet/downloads/odacdev-4242174.html).
2. Registrare il client gestito ODP.NET nella GAC: C:\oracle32\product\18.0.0\client_1\odp.net\bin\4\OraProvCfg.exe/Action: GAC/ProviderPath: C:\oracle32\product\18.0.0\client_1\odp.net\managed\common\Oracle.ManagedDataAccess.dll
3. Aggiungere le voci client gestite di ODP.NET a Machine. config: C:\oracle32\product\18.0.0\client_1\odp.net\bin\4\OraProvCfg.exe/Action: config/Force/Product: odpm/frameworkVersion: v 4.0.30319/ProductVersion: 4.122.18.3

 Usare le informazioni presenti in questo argomento per compilare un'origine dati. Per istruzioni dettagliate, vedere [Aggiungere e verificare una connessione dati &#40;Generatore report e SSRS&#41;](../../reporting-services/report-data/add-and-verify-a-data-connection-report-builder-and-ssrs.md).  
  
##  <a name="Connection"></a> Stringa di connessione  
 Contattare l'amministratore del database per ottenere le informazioni di connessione e le credenziali da utilizzare per connettersi all'origine dati. La stringa di connessione di esempio seguente specifica un database Oracle nel server "Oracle18" che usa Unicode. Il nome del server deve corrispondere a quello definito nel file di configurazione Tnsnames.ora come nome dell'istanza del server Oracle.  
  
```  
Data Source="Oracle"; Unicode="True"  
```  
  
 Per altri esempi di stringhe di connessione, vedere [Connessioni dati, origini dati e stringhe di connessione in Generatore report](data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md).  
  
##  <a name="Credentials"></a> Credenziali  
 Le credenziali sono necessarie per eseguire query, nonché per visualizzare l'anteprima del report in locale e dal server di report.  
  
 Dopo aver pubblicato il report, potrebbe essere necessario modificare le credenziali per l'origine dati affinché quando il report viene eseguito nel server di report, le autorizzazioni per il recupero dei dati risultino valide.  
  
 Per altre informazioni, vedere [Specificare le credenziali e le informazioni sulla connessione per le origini dati del report](specify-credential-and-connection-information-for-report-data-sources.md).  
  
  
##  <a name="Query"></a> Query  
 Per creare un set di dati, è possibile selezionare una stored procedure in un elenco a discesa oppure creare una query SQL. Per compilare una query, è necessario utilizzare la finestra Progettazione query basata su testo. Per altre informazioni, vedere [Interfaccia utente di Progettazione query basata su testo &#40;Generatore report &#41;](../../reporting-services/report-data/text-based-query-designer-user-interface-report-builder.md).  
  
 È possibile specificare le stored procedure che restituiscono solo un set di risultati. Le query basate su cursori non sono supportate.  
  
##  <a name="Parameters"></a> Parametri  
 Se la query include variabili di query, i parametri di report corrispondenti verranno generati automaticamente. I parametri denominati sono supportati da questa estensione. Per Oracle versione 9 o successive, i parametri multivalore sono supportati.  
  
 I parametri di report vengono creati con valori di proprietà predefiniti che all'occorrenza possono essere modificati. Ad esempio, i dati di ogni parametro di report sono di tipo **Text**. Dopo aver creato i parametri di report, potrebbe essere necessario modificare i valori predefiniti. Per ulteriori informazioni, vedere la pagina relativa al [Parametri report &#40;Generatore report e Progettazione report&#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md).  
  
  
##  <a name="Remarks"></a> Osservazioni  
 Prima di poter connettere un'origine dati Oracle, l'amministratore di sistema deve installare la versione del provider di dati .NET per Oracle che supporta il recupero di dati dal database Oracle. Il provider di dati deve essere installato nello stesso computer di Generatore report e anche nel server di report.  
  
 Per ulteriori informazioni, vedere quanto segue:  
  
-   [Come utilizzare Reporting Services per configurare e accedere a un'origine dati Oracle](https://support.microsoft.com/kb/834305)  
-   [Come aggiungere autorizzazioni per l'entità di sicurezza SERVIZIO DI RETE](https://support.microsoft.com/kb/870668)  
  
### <a name="alternate-data-extensions"></a>Estensioni per i dati alternative 
 
 È inoltre possibile recuperare dati da un database Oracle tramite un tipo di origine dati OLE DB. Per altre informazioni, vedere [Tipo di connessione OLE DB &#40;SSRS&#41;](../../reporting-services/report-data/ole-db-connection-type-ssrs.md).  

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions" 
### <a name="report-models"></a>Modelli di report  

 È possibile creare anche modelli basati su un database Oracle.  
::: moniker-end
   
### <a name="platform-and-version-information"></a>Informazioni sulla piattaforma e sulla versione  

 Per altre informazioni sulle piattaforme e le versioni supportate, vedere [Origini dati supportate da Reporting Services &#40;SSRS&#41;](../../reporting-services/report-data/data-sources-supported-by-reporting-services-ssrs.md).  

  
## <a name="see-also"></a>Vedere anche

 [Parametri report &#40;Generatore report e Progettazione report&#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)   
 [Filtro, raggruppamento e ordinamento di dati &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)   
 [Espressioni &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md)  
  
  
