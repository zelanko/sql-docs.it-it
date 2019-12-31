---
title: SQL Server 2014 Analysis Services | Microsoft Docs
ms.custom: ''
ms.date: 11/25/2019
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- Analysis Services, about Analysis Services - Multidimensional Data
- SSAS
- Analysis Services
- SQL Server Analysis Services, about Analysis Services - Multidimensional Data
- SQL Server Analysis Services
- multidimensional data [Analysis Services]
- SSAS, about Analysis Services - Multidimensional Data
ms.assetid: 49d186f4-4b4d-4a5a-bb1a-e2699c64a731
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: bceabba9b490be6bc2c51b4fdcce9b6b131eb0ce
ms.sourcegitcommit: 7183735e38dd94aa3b9bab2b73ccab54c916ff86
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/02/2019
ms.locfileid: "74683472"
---
# <a name="sql-server-2014-analysis-services"></a>SQL Server 2014 Analysis Services

  SQL Server 2014 Analysis Services è un motore dati analitici utilizzato nelle soluzioni di supporto decisionale e di business intelligence (BI), fornendo i dati analitici per i report aziendali e le applicazioni client quali Excel, report Reporting Services e altro strumenti di business intelligence di terze parti. 

## <a name="about-sql-server-analysis-services-documentation"></a>Informazioni SQL Server Analysis Services documentazione

La documentazione è separata dalla versione. Si è attualmente in SQL Server 2014 Analysis Services documentazione.

- Per ulteriori informazioni su SQL Server 2012 e versioni precedenti, vedere la [documentazione di SQL Server versioni precedenti](https://docs.microsoft.com/previous-versions/sql/).
- Per ulteriori informazioni su SQL Server 2014, vedere [la documentazione online di SQL Server 2014](../2014-toc/index.yml)
- Per ulteriori informazioni su SQL Server 2016 e versioni successive, vedere la [documentazione di Microsoft SQL](https://docs.microsoft.com/sql/).
- Per ulteriori informazioni su Azure Analysis Services, vedere la [documentazione di Azure Analysis Services](https://docs.microsoft.com/azure/analysis-services/).

## <a name="analysis-services-workflow"></a>Flusso di lavoro Analysis Services

Un flusso di lavoro tipico include la compilazione di un modello di dati OLAP o tabulare, la distribuzione del modello come database in un'istanza del server, l'elaborazione del database per il caricamento con i dati e l'assegnazione di autorizzazioni per consentire l'accesso ai dati. Quando è pronto, il modello di dati multifunzione sarà accessibile a qualsiasi applicazione client che supporta [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] come origine dati.  
  
 Per creare un modello, usare SQL Server Data Tools (vedere [strumenti e applicazioni usati in Analysis Services](tools-and-applications-used-in-analysis-services.md)), scegliendo un modello di progetto tabulare o multidimensionale e di data mining. Il modello di progetto include cartelle per tutti gli oggetti necessari in un modello. È possibile usare le procedure guidate per creare tutti gli elementi di base, ad esempio origini dati, viste origine dati, dimensioni, cubi e ruoli.  
  
 I modelli vengono popolati con i dati dei sistemi di dati esterni, in genere data warehouse ospitati in un motore di database relazionale Oracle o SQL Server (i modelli tabulari supportano i tipi di origine dati aggiuntivi). I modelli specificano oggetti query, ad esempio cubi, ma specificano anche dimensioni che possono essere usate in più cubi, calcoli e indicatori KPI che incapsulano la logica di business e interazioni quali navigazione e comportamenti drill-through.  
  
 Per utilizzare un modello, viene distribuito in un'istanza del server che esegue database in una modalità server specifica, rendendo i dati disponibili agli utenti autorizzati che si connettono tramite Excel o altre applicazioni.  
  
 È possibile installare un'istanza di in una delle tre modalità server:  
  
-   Come istanza tabulare che esegue modelli tabulari.  
  
-   Come istanza multidimensionale e data mining che esegue cubi OLAP e modelli di data mining (impostazione predefinita).  
  
-   Come PowerPivot per SharePoint che esegue modelli di dati di Excel e PowerPivot in SharePoint (PowerPivot per SharePoint è un motore dati di livello intermedio che carica, esegue query e aggiorna i modelli di dati ospitati in SharePoint).  
  
 Lo stesso motore dati; tre modi diversi per utilizzarlo. Si noti che le modalità server vengono impostate durante l'installazione e non possono essere modificate in un secondo momento. Occorre installare una nuova istanza se è necessaria una modalità diversa.  
  
 La documentazione fondamentale per Analysis Services è organizzata in sezioni che corrispondono al tipo di progetto che si sta compilando. Per ulteriori informazioni su questa modalità o area funzionale, scegliere tra i seguenti collegamenti.  
  
 **Sfoglia contenuto per area**  
 ![Icona della cartella file piccola](../../2014/integration-services/media/filefolder-small.gif "Icona della cartella file piccola") [confronto tra soluzioni tabulari e multidimensionali &#40;SSAS&#41;](comparing-tabular-and-multidimensional-solutions-ssas.md)  
  
 ![Icona cartella file di piccole dimensioni](../../2014/integration-services/media/filefolder-small.gif "Icona della cartella file piccola") [Analysis Services gestione istanza](instances/analysis-services-instance-management.md)  
  
 ![Icona della cartella file piccola](../../2014/integration-services/media/filefolder-small.gif "Icona della cartella file piccola") [modello tabulare &#40;SSAS tabulare&#41;](tabular-models/tabular-models-ssas.md)  
  
 ![Icona della cartella file piccola](../../2014/integration-services/media/filefolder-small.gif "Icona della cartella file piccola") [modellazione multidimensionale &#40;SSAS&#41;](multidimensional-models/multidimensional-models-ssas.md)  
  
 ![Icona della cartella file piccola](../../2014/integration-services/media/filefolder-small.gif "Icona della cartella file piccola") [Data Mining &#40;SSAS&#41;](data-mining/data-mining-ssas.md)  
  
 ![Icona cartella file di piccole dimensioni](../../2014/integration-services/media/filefolder-small.gif "Icona della cartella file piccola") [PowerPivot per SharePoint &#40;SSAS&#41;](power-pivot-sharepoint/power-pivot-for-sharepoint-ssas.md)  
  
> [!NOTE]  
>  [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]le funzionalità variano in base all'edizione. I modelli multidimensionali e di data mining sono disponibili nell'edizione Standard, ma con un numero inferiore di funzionalità rispetto alle edizioni superiori. I modelli tabulari e PowerPivot per SharePoint sono funzionalità Premium e non sono disponibili in una licenza Standard Edition. Per ulteriori informazioni, vedere [Features Supported by the Editions of SQL Server 2014](../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Analysis Services esercitazioni &#40;SSAS&#41;](analysis-services-tutorials-ssas.md)   
 [Installazione per SQL Server 2014](../database-engine/install-windows/installation-for-sql-server.md)   
 [Guida per gli sviluppatori &#40;Analysis Services&#41;](analysis-services-developer-documentation.md)   
 [Centro risorse SQL Server](https://go.microsoft.com/fwlink/?linkID=219676)   
 [SQLCat.com](https://go.microsoft.com/fwlink/?linkID=220963)  
  
  
