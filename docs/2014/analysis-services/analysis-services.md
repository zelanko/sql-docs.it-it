---
title: SQL Server 2014 Analysis Services - Documenti Microsoft
ms.custom: ''
ms.date: 04/06/2020
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
ms.openlocfilehash: 986356e6ebf7697bf0b425553f6803659a0fc5cb
ms.sourcegitcommit: 8f99d15c5b23d9f3c08a77e2b8bea5772f570493
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/07/2020
ms.locfileid: "80760308"
---
# <a name="sql-server-2014-analysis-services"></a>SQL Server 2014 Analysis Services

  SQL Server 2014 Analysis Services è un motore di dati analitici utilizzato nel supporto decisionale e nelle soluzioni di business intelligence (BI), che fornisce i dati analitici per i report aziendali e le applicazioni client, ad esempio Excel, i report di Reporting Services reporting e altri strumenti di business intelligence di terze parti. 

## <a name="about-sql-server-analysis-services-documentation"></a>Documentazione di SQL Server Analysis Services

La documentazione è separata dalla versione. Si è attualmente nella documentazione di SQL Server 2014 Analysis Services.

- Per ulteriori informazioni su SQL Server 2012 e versioni precedenti, vedere la documentazione relativa alle versioni precedenti di [SQL Server.](https://docs.microsoft.com/previous-versions/sql/)
- Per ulteriori informazioni su SQL Server 2014, vedere [la documentazione in linea di SQL Server 2014](../2014-toc/index.yml)
- Per ulteriori informazioni su SQL Server 2016 e versioni successive, vedere la [documentazione](https://docs.microsoft.com/analysis-services/)di Analysis Services .
- Per altre informazioni su Azure Analysis Services, vedere la documentazione di Azure Analysis Services.To learn more about Azure Analysis Services, see [Azure Analysis Services Documentation.](https://docs.microsoft.com/azure/analysis-services/)

## <a name="analysis-services-workflow"></a>Flusso di lavoro di Analysis ServicesAnalysis Services workflow

Un flusso di lavoro tipico include la creazione di un modello di dati OLAP o tabulare, la distribuzione del modello come database in un'istanza del server, l'elaborazione del database per caricarlo con i dati e quindi l'assegnazione delle autorizzazioni per consentire l'accesso ai dati. Quando è pronto, il modello di dati multifunzione sarà accessibile a qualsiasi applicazione client che supporta [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] come origine dati.  
  
 Per creare un modello, usare SQL Server Data ToolsSQL Server Data Tools (vedere [Strumenti e applicazioni usate in Analysis ServicesAnalysis Services),](tools-and-applications-used-in-analysis-services.md)scegliendo un modello di progetto tabulare o multidimensionale e di data mining. Il modello di progetto include cartelle per tutti gli oggetti necessari in un modello. È possibile usare le procedure guidate per creare tutti gli elementi di base, ad esempio origini dati, viste origine dati, dimensioni, cubi e ruoli.  
  
 I modelli vengono popolati con i dati dei sistemi di dati esterni, in genere data warehouse ospitati in un motore di database relazionale Oracle o SQL Server (i modelli tabulari supportano i tipi di origine dati aggiuntivi). I modelli specificano oggetti query, ad esempio cubi, ma specificano anche dimensioni che possono essere usate in più cubi, calcoli e indicatori KPI che incapsulano la logica di business e interazioni quali navigazione e comportamenti drill-through.  
  
 Per utilizzare un modello, viene distribuito in un'istanza del server che esegue i database in una determinata modalità server, rendendo i dati disponibili agli utenti autorizzati che si connettono tramite Excel o altre applicazioni.  
  
 È possibile installare un'istanza in una delle tre modalità server seguenti:You can install an instance in one of three server modes:  
  
-   Come istanza tabulare che esegue modelli tabulari.  
  
-   Come istanza multidimensionale e data mining che esegue cubi OLAP e modelli di data mining (impostazione predefinita).  
  
-   Come PowerPivot per SharePoint che esegue modelli di dati di Excel e PowerPivot in SharePoint (PowerPivot per SharePoint è un motore dati di livello intermedio che carica, esegue query e aggiorna i modelli di dati ospitati in SharePoint).  
  
 Lo stesso motore dati; tre modi diversi per utilizzarlo. Si noti che le modalità server vengono impostate durante l'installazione e non possono essere modificate in un secondo momento. Occorre installare una nuova istanza se è necessaria una modalità diversa.  
  
 La documentazione fondamentale per Analysis Services è organizzata in sezioni che corrispondono al tipo di progetto che si sta compilando. Per ulteriori informazioni su questa modalità o area funzionale, scegliere tra i seguenti collegamenti.  
  
 **Sfoglia i contenuti per Area**  
 Icona cartella file di piccole dimensioni [che confrontano le soluzioni tabulari e multidimensionali &#40;i&#41;SSASSmall](comparing-tabular-and-multidimensional-solutions-ssas.md) ![File Folder Icon](../../2014/integration-services/media/filefolder-small.gif "Icona della cartella file piccola") Comparing Tabular and Multidimensional Solutions &#40;SSAS&#41;  
  
 [Gestione delle istanze](instances/analysis-services-instance-management.md) di ![Small File Folder Icon](../../2014/integration-services/media/filefolder-small.gif "Icona della cartella file piccola") Analysis Services  
  
 Piccola ![cartella file icona tabulare](../../2014/integration-services/media/filefolder-small.gif "Icona della cartella file piccola") [modellazione &#40;SSAS&#41;tabulare](tabular-models/tabular-models-ssas.md)  
  
 ![Piccola cartella file Icona](../../2014/integration-services/media/filefolder-small.gif "Icona della cartella file piccola") [multidimensionale Modellazione &#40;&#41;SSAS](multidimensional-models/multidimensional-models-ssas.md)  
  
 Piccole&#41;di data mining &#40;SSAS per l'icona della cartella di ![fileSmall File Folder Icon](../../2014/integration-services/media/filefolder-small.gif "Icona della cartella file piccola") [Data Mining &#40;SSAS&#41;](data-mining/data-mining-ssas.md)  
  
 ![Icona cartella file di piccole](../../2014/integration-services/media/filefolder-small.gif "Icona della cartella file piccola") dimensioni [PowerPivot per SharePoint &#40;&#41;SSAS](power-pivot-sharepoint/power-pivot-for-sharepoint-ssas.md)  
  
> [!NOTE]  
>  Le funzionalità di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] variano in base all'edizione. I modelli multidimensionali e di data mining sono disponibili nell'edizione Standard, ma con un numero inferiore di funzionalità rispetto alle edizioni superiori. I modelli tabulari e PowerPivot per SharePoint sono funzionalità Premium e non sono disponibili in una licenza Standard Edition. Per ulteriori informazioni, vedere [Features Supported by the Editions of SQL Server 2014](../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Esercitazioni di Analysis Services &#40;&#41;SSAS](analysis-services-tutorials-ssas.md)   
 [Installazione per SQL Server 2014](../database-engine/install-windows/installation-for-sql-server.md)   
 [Guida per sviluppatori &#40;&#41;di Analysis Services](analysis-services-developer-documentation.md)   
 [Centro risorse di SQL Server](https://go.microsoft.com/fwlink/?linkID=219676)   
 [SQLCat.com](https://go.microsoft.com/fwlink/?linkID=220963)  
  
  
