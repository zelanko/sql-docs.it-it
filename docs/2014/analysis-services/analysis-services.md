---
title: Analysis Services | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
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
ms.openlocfilehash: 241bb57ffd0ce05f1daa289cc7ae78c365a27cc9
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/23/2019
ms.locfileid: "66062335"
---
# <a name="analysis-services"></a>Analysis Services
  [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] è un motore dati analitici online usato nelle soluzioni di Business Intelligence (BI) e di supporto decisionale che fornisce i dati analitici usati nei report aziendali e nelle applicazioni client quali i report di Reporting Services, Excel e altri strumenti di BI di terze parti. Un flusso di lavoro tipico per [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] include la creazione di un oggetto OLAP o un modello di dati tabulare, la distribuzione del modello come database in un'istanza di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], l'elaborazione del database per caricarvi dati e l'assegnazione di autorizzazioni per permettere l'accesso ai dati. Quando è pronto, il modello di dati multifunzione sarà accessibile a qualsiasi applicazione client che supporta [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] come origine dati.  
  
 Per creare un modello, usare SQL Server Data Tools (vedere [gli strumenti e applicazioni usati in Analysis Services](tools-and-applications-used-in-analysis-services.md)), scegliendo un tabulare o multidimensionale e Data Mining di modello di progetto. Il modello di progetto include cartelle per tutti gli oggetti necessari in un modello. È possibile usare le procedure guidate per creare tutti gli elementi di base, ad esempio origini dati, viste origine dati, dimensioni, cubi e ruoli.  
  
 I modelli vengono popolati con i dati dei sistemi di dati esterni, in genere data warehouse ospitati in un motore di database relazionale Oracle o SQL Server (i modelli tabulari supportano i tipi di origine dati aggiuntivi). I modelli specificano oggetti query, ad esempio cubi, ma specificano anche dimensioni che possono essere usate in più cubi, calcoli e indicatori KPI che incapsulano la logica di business e interazioni quali navigazione e comportamenti drill-through.  
  
 Per utilizzare un modello, è necessario distribuirlo in un'istanza di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] che esegue database in una modalità server specifico, rendendo i dati disponibili agli utenti autorizzati che si connettono tramite Excel o altre applicazioni.  
  
 È possibile installare un'istanza di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] in una di tre modalità server:  
  
-   Come istanza tabulare che esegue modelli tabulari.  
  
-   Come istanza multidimensionale e data mining che esegue cubi OLAP e modelli di data mining (impostazione predefinita).  
  
-   Come PowerPivot per SharePoint che esegue modelli di dati di Excel e PowerPivot in SharePoint (PowerPivot per SharePoint è un motore dati di livello intermedio che carica, esegue query e aggiorna i modelli di dati ospitati in SharePoint).  
  
 Lo stesso motore dati; tre modi diversi per utilizzarlo. Si noti che le modalità server vengono impostate durante l'installazione e non possono essere modificate in un secondo momento. Occorre installare una nuova istanza se è necessaria una modalità diversa.  
  
 La documentazione fondamentale per Analysis Services è organizzata in sezioni che corrispondono al tipo di progetto che si sta compilando. Per ulteriori informazioni su questa modalità o area funzionale, scegliere tra i seguenti collegamenti.  
  
 **Ricerca di contenuto per area**  
 ![Icona cartella File piccola](../../2014/integration-services/media/filefolder-small.gif "icona cartella File piccola") [confronto tra soluzioni tabulari e multidimensionali &#40;SSAS&#41;](comparing-tabular-and-multidimensional-solutions-ssas.md)  
  
 ![Icona cartella File piccola](../../2014/integration-services/media/filefolder-small.gif "icona cartella File piccola") [istanza di Analysis Services Management](instances/analysis-services-instance-management.md)  
  
 ![Icona cartella File piccola](../../2014/integration-services/media/filefolder-small.gif "icona cartella File piccola") [modellazione tabulare &#40;tabulare di SSAS&#41;](tabular-models/tabular-models-ssas.md)  
  
 ![Icona cartella File piccola](../../2014/integration-services/media/filefolder-small.gif "icona cartella File piccola") [modellazione multidimensionale &#40;SSAS&#41;](multidimensional-models/multidimensional-models-ssas.md)  
  
 ![Icona cartella File piccola](../../2014/integration-services/media/filefolder-small.gif "icona cartella File piccola") [Data Mining &#40;SSAS&#41;](data-mining/data-mining-ssas.md)  
  
 ![Icona cartella File piccola](../../2014/integration-services/media/filefolder-small.gif "icona cartella File piccola") [PowerPivot per SharePoint &#40;SSAS&#41;](power-pivot-sharepoint/power-pivot-for-sharepoint-ssas.md)  
  
> [!NOTE]  
>  Le funzionalità di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] variano in base all'edizione. I modelli multidimensionali e di data mining sono disponibili nell'edizione Standard, ma con un numero inferiore di funzionalità rispetto alle edizioni superiori. I modelli tabulari e PowerPivot per SharePoint sono funzionalità Premium e non sono disponibili in una licenza Standard Edition. Per ulteriori informazioni, vedere [Features Supported by the Editions of SQL Server 2014](../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Esercitazioni su Analysis Services &#40;SSAS&#41;](analysis-services-tutorials-ssas.md)   
 [Installazione di SQL Server 2014](../database-engine/install-windows/installation-for-sql-server.md)   
 [Guida per sviluppatori &#40;Analysis Services&#41;](analysis-services-developer-documentation.md)   
 [Centro risorse di SQL Server](https://go.microsoft.com/fwlink/?linkID=219676)   
 [SQLCat.com](https://go.microsoft.com/fwlink/?linkID=220963)  
  
  
