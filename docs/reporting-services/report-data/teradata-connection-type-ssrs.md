---
title: Tipo di connessione Teradata | Microsoft Docs
ms.date: 03/17/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-data
ms.topic: conceptual
ms.assetid: b02779c2-a6b9-453c-815f-adad53353952
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 7fffacee190197125cf283be6ad9263dfae1f1d1
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/29/2020
ms.locfileid: "77081705"
---
# <a name="teradata-connection-type-ssrs"></a>Tipo di connessione Teradata (SSRS)
  Per includere dati da Teradata nel report, è necessario disporre di un set di dati basato su un'origine dati del report di tipo Teradata. Questo tipo di origine dati predefinito è basato sull'estensione per l'elaborazione dati del provider gestito .NET per Teradata.  
  
 Usare le informazioni presenti in questo argomento per compilare un'origine dati. Per istruzioni dettagliate, vedere [Aggiungere e verificare una connessione dati &#40;Generatore report e SSRS&#41;](../../reporting-services/report-data/add-and-verify-a-data-connection-report-builder-and-ssrs.md).  
  
##  <a name="connection-string"></a><a name="Connection"></a> Stringa di connessione  
 Contattare l'amministratore del database per ottenere le informazioni di connessione e le credenziali da utilizzare per connettersi all'origine dati. Nell'esempio di stringa di connessione seguente viene specificata un'origine dati Teradata sul server identificato da un indirizzo IP:  
  
```  
data source=<IP Address>  
```  
  
 Per altri esempi di stringhe di connessione, vedere l'articolo sulla [creazione di stringhe di connessione dati in Generatore report e SSRS](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md).  
  
##  <a name="credentials"></a><a name="Credentials"></a> Credenziali  
 Le credenziali sono necessarie per eseguire query, nonché per visualizzare l'anteprima del report in locale e dal server di report.  
  
 Dopo aver pubblicato il report, potrebbe essere necessario modificare le credenziali per l'origine dati affinché quando il report viene eseguito nel server di report, le autorizzazioni per il recupero dei dati risultino valide.  
  
 Per altre informazioni, vedere [Creare stringhe di connessione dati - Generatore report e SSRS](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md) o [Specificare le credenziali e le informazioni sulla connessione per le origini dati del report](specify-credential-and-connection-information-for-report-data-sources.md).  
  
  
##  <a name="remarks"></a><a name="Remarks"></a> Osservazioni  
 Prima che sia possibile connettersi a un'origine dati Teradata, l'amministratore di sistema deve aver installato la versione corretta del provider di dati .NET per Teradata che supporta il recupero di dati da Teradata. Il provider di dati deve essere installato nello stesso computer di Generatore report e anche nel server di report.  
  
 Non tutte le modalità di recapito report sono supportate da questo provider di dati. Il recapito di report tramite sottoscrizioni guidate dai dati non è supportato per questa estensione per l'elaborazione dati. Per altre informazioni, vedere [Usare un'origine dati esterna per i dati del Sottoscrittore &#40;sottoscrizione guidata dai dati&#41;](../../reporting-services/subscriptions/use-an-external-data-source-for-subscriber-data-data-driven-subscription.md).  
  
  
##  <a name="report-models"></a><a name="Models"></a> Modelli di report  
 Per creare un set di dati da un modello di report basato su un'origine dati Teradata, il modello deve essere progettato in Progettazione modelli in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] e deve essere pubblicato su un server di report.  
  
  
##  <a name="related-sections"></a><a name="Related"></a> Sezioni correlate  
 In queste sezioni della documentazione sono incluse informazioni concettuali approfondite sui dati dei report, nonché le informazioni necessarie sulle procedure per definire, personalizzare e usare parti di un report correlate ai dati.  
  
 [Set di dati del report &#40;SSRS&#41;](../../reporting-services/report-data/report-datasets-ssrs.md)  
 Viene fornita una panoramica sull'accesso ai dati del report.  
  
 [Creare stringhe di connessione dati - Generatore report e SSRS](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md)  
 Vengono fornite informazioni sulle connessioni dati e sulle origini dati.  
  
 [Set di dati condivisi e incorporati del report &#40;Generatore report e SSRS&#41;](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)  
 Vengono fornite informazioni sui set di dati incorporati e condivisi.  
  
 [Raccolta di campi del set di dati &#40;Generatore report e SSRS&#41;](../../reporting-services/report-data/dataset-fields-collection-report-builder-and-ssrs.md)  
 Vengono fornite informazioni sulla raccolta di campi generata dalla query del set di dati.  
  
 [Origini dati supportate da Reporting Services &#40;SSRS&#41;](../../reporting-services/report-data/data-sources-supported-by-reporting-services-ssrs.md) Fornisce informazioni approfondite sul supporto di piattaforme e versioni per ogni estensione per i dati.  
 
  
## <a name="see-also"></a>Vedere anche  
 [Parametri report &#40;Generatore report e Progettazione report&#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)   
 [Filtro, raggruppamento e ordinamento di dati &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)   
 [Espressioni &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md)  
  
  
