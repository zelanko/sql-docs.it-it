---
title: Tipo di connessione ODCB (SSRS) | Microsoft Docs
ms.date: 03/17/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-data
ms.topic: conceptual
ms.assetid: 24163866-f37a-4c38-982e-c3d79bf64d4c
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 31d02cdaab35dc25cf828aa22897f6b35547a558
ms.sourcegitcommit: dda9a1a7682ade466b8d4f0ca56f3a9ecc1ef44e
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 05/14/2019
ms.locfileid: "65577923"
---
# <a name="odbc-connection-type-ssrs"></a>Tipo di connessione ODBC (SSRS)
  Per includere dati da un provider di dati ODBC, è necessario disporre di un set di dati basato su un'origine dati del report di tipo ODBC. Questo tipo di origine dati predefinito è basato sull'estensione per l'elaborazione dati ODBC di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
 Usare le informazioni presenti in questo argomento per compilare un'origine dati. Per istruzioni dettagliate, vedere [Aggiungere e verificare una connessione dati &#40;Generatore report e SSRS&#41;](../../reporting-services/report-data/add-and-verify-a-data-connection-report-builder-and-ssrs.md).  
  
##  <a name="Connection"></a> Stringa di connessione  
 La stringa di connessione per l'estensione per l'elaborazione dati ODBC dipende dal driver ODBC desiderato. In una stringa di connessione tipica sono contenute coppie nome/valore supportate dal driver. Nella stringa di connessione seguente, ad esempio, viene specificato il driver ODBC per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client e il database AdventureWorks:  
  
```  
Driver={SQL Server Native Client 10.0};Server=server;Database=AdventureWorks;Trusted_Connection=yes;  
```  
  
  
##  <a name="Credentials"></a> Credenziali  
 Le credenziali sono necessarie per eseguire query, nonché per visualizzare l'anteprima del report in locale e dal server di report.  
  
 Dopo aver pubblicato il report, potrebbe essere necessario modificare le credenziali per l'origine dati affinché quando il report viene eseguito nel server di report, le autorizzazioni per il recupero dei dati risultino valide.  
  
 Se si configura l'origine dei dati ODBC per la richiesta di una password o l'inclusione della password nella stringa di connessione e un utente immette la password con caratteri speciali quali segni di punteggiatura, è possibile che alcuni driver dell'origine dati sottostante non convalidino i caratteri speciali. In tal caso, quando si elabora il report verrà visualizzato un messaggio che indica che la password non è valida. Se la modifica della password è complessa, è possibile rivolgersi all'amministratore del database per fare in modo che vengano archiviate nel server di report le credenziali appropriate come parte del nome dell'origine dei dati (DSN, Data Source Name) ODBC di sistema. Per altre informazioni, vedere "OdbcConnection.ConnectionString" nella documentazione di [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] SDK.  
  
> [!NOTE]  
>  È consigliabile non aggiungere le informazioni di accesso, ad esempio la password, alla stringa di connessione. In Generatore report è presente una scheda separata nella finestra di dialogo **Origine dati** che può essere utilizzata per immettere le credenziali.  
  
 Per altre informazioni, vedere [Connessioni dati, origini dati e stringhe di connessione &#40;Generatore report e SSRS&#41;](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md) e [Specifica di credenziali in Generatore report](https://msdn.microsoft.com/library/7412ce68-aece-41c0-8c37-76a0e54b6b53).  
  
  
##  <a name="Remarks"></a> Osservazioni  
 ODBC è una prima tecnologia di accesso ai dati che ha preceduto OLEDB. ODBC supporta solo origini dati relazionali. I provider di dati ODBC vengono chiamati *driver*. I driver ODBC vengono forniti da Microsoft e fornitori di terze parti. Ad esempio in Microsoft Office è possibile installare driver ODBC che consentono la connessione a formati di file di Office.  
  
 Prima che sia possibile compilare una stringa di connessione ODBC, è necessario avere installato i driver ODBC e sviluppare un computer o sistema DSN. Per recuperare correttamente i dati desiderati, è necessario fornire la sintassi della query supportata dal driver. Il supporto dei parametri varia in base al driver. Per altre informazioni, vedere gli argomenti specifici del driver selezionato, ad esempio [SQL Server Native Client &#40;ODBC&#41;](../../relational-databases/native-client/odbc/sql-server-native-client-odbc.md).  
  
###### <a name="platform-and-version-information"></a>Informazioni sulla piattaforma e sulla versione  
 Per altre informazioni sui provider dati ODBC specifici, vedere [Origini dei dati supportate da Reporting Services &#40;SSRS&#41;](../../reporting-services/report-data/data-sources-supported-by-reporting-services-ssrs.md) nella documentazione relativa a [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] inclusa nella [documentazione online](https://go.microsoft.com/fwlink/?linkid=121312) di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
  
##  <a name="HowTo"></a> Procedure  
 In questa sezione sono contenute istruzioni dettagliate per l'utilizzo di connessioni dati, origini dati e set di dati.  
  
 [Aggiungere e verificare una connessione dati &#40;Generatore report e SSRS&#41;](../../reporting-services/report-data/add-and-verify-a-data-connection-report-builder-and-ssrs.md)  
  
 [Creare un set di dati condiviso o un set di dati incorporato &#40;Generatore report e SSRS&#41;](../../reporting-services/report-data/create-a-shared-dataset-or-embedded-dataset-report-builder-and-ssrs.md)  
  
 [Aggiungere un filtro a un set di dati &#40;Generatore report e SSRS&#41;](../../reporting-services/report-data/add-a-filter-to-a-dataset-report-builder-and-ssrs.md)  
  
  
##  <a name="Related"></a> Sezioni correlate  
 In queste sezioni della documentazione sono incluse informazioni concettuali approfondite sui dati dei report, nonché le informazioni necessarie sulle procedure per definire, personalizzare e usare parti di un report correlate ai dati.  
  
 [Set di dati del report &#40;SSRS&#41;](../../reporting-services/report-data/report-datasets-ssrs.md)  
 Viene fornita una panoramica sull'accesso ai dati del report.  
  
 [Connessioni dati, origini dati e stringhe di connessione in Generatore report](https://msdn.microsoft.com/library/7e103637-4371-43d7-821c-d269c2cc1b34)  
 Vengono fornite informazioni sulle connessioni dati e sulle origini dati.  
  
 [Set di dati condivisi e incorporati del report &#40;Generatore report e SSRS&#41;](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)  
 Vengono fornite informazioni sui set di dati incorporati e condivisi.  
  
 [Raccolta di campi del set di dati &#40;Generatore report e SSRS&#41;](../../reporting-services/report-data/dataset-fields-collection-report-builder-and-ssrs.md)  
 Vengono fornite informazioni sulla raccolta di campi di set di dati generata dalla query.  
  
 [Origini dati supportate da Reporting Services &#40;SSRS&#41;](../../reporting-services/report-data/data-sources-supported-by-reporting-services-ssrs.md) nella documentazione relativa a [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] inclusa nella [documentazione online](https://go.microsoft.com/fwlink/?linkid=121312) di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
 Vengono fornite informazioni dettagliate sul supporto delle piattaforme e delle versioni per ogni estensione per i dati.  
  
  
## <a name="see-also"></a>Vedere anche  
 [Parametri report &#40;Generatore report e Progettazione report&#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)   
 [Filtro, raggruppamento e ordinamento di dati &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)   
 [Espressioni &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md)  
  
  
