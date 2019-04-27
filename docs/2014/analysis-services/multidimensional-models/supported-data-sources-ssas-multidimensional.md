---
title: Le origini dati supportate (SSAS multidimensionale) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Analysis Services, data sources
- data sources [Analysis Services], about data sources
- Analysis Services, data sources
- connections [Analysis Services]
- SSAS, data sources
ms.assetid: c97e0f8d-7ddd-4941-8b51-e7832f30fbbe
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: a88d312d2764d04d1766371463a1735737973164
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62740966"
---
# <a name="data-sources-supported-ssas-multidimensional"></a>Data Sources Supported (SSAS Multidimensional)
  In questo argomento vengono descritti i tipi di origini dati che possono essere utilizzati in un modello multidimensionale.  
  
##  <a name="bkmk_supported_ds"></a> Origini dati supportate  
 È possibile recuperare dati dalle origini dati riportate nella tabella seguente. Il programma di installazione di [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]non consente di installare i provider elencati per ogni origine dati. Alcuni provider potrebbero già essere installati con altre applicazioni nel computer; negli altri casi sarà necessario scaricare e installare il provider.  
  
> [!NOTE]  
>  È inoltre possibile utilizzare provider di terze parti, ad esempio il provider OLE DB Oracle, per la connessione a database di terze parti, di cui verrà offerto il supporto.  
  
|||||  
|-|-|-|-|  
|Source|Versioni|Tipo di file|Providers <sup>1</sup>|  
|Database di Access|Microsoft Access 2007, 2010, 2013.|Estensione accdb o mdb|Provider OLE DB per Microsoft Jet 4.0.|  
|Database relazionali di SQL Server <sup>5</sup>|Microsoft SQL Server 2005, 2008, 2008 R2, 2012, 2014 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] <sup>2</sup>, SQL Server Parallel Data Warehouse (PDW) <sup>3</sup>|(non applicabile)|Provider OLE DB per SQL Server<br /><br /> Provider OLE DB di SQL Server Native Client<br /><br /> Provider OLE DB per SQL Server Native Client 11.0<br /><br /> Provider di dati .NET Framework per SQL Client|  
|Database relazionali Oracle|Oracle 9i, 10g, 11g.|(non applicabile)|Provider OLE DB Oracle<br /><br /> Provider di dati .NET Framework per il client Oracle<br /><br /> Provider di dati .NET Framework per SQL Server<br /><br /> Provider OLE DB MSDAORA <sup>4</sup><br /><br /> OraOLEDB<br /><br /> MSDASQL|  
|Database relazionali di Teradata|Teradata V2R6 e V12|(non applicabile)|Provider OLE DB TDOLEDB<br /><br /> Provider di dati .NET per Teradata|  
|Database relazionali di Informix|V11.10|(non applicabile)|Provider OLE DB per Informix|  
|Database relazionali di IBM DB2|8.1|(non applicabile)|DB2OLEDB|  
|Database relazionali di Sybase Adaptive Server Enterprise (ASE)|15.0.2|(non applicabile)|Provider OLE DB per Sybase|  
|Altri database relazionali|(non applicabile)|(non applicabile)|Un provider OLE DB|  
  
 <sup>1</sup> origini dati ODBC non sono supportate per soluzioni multidimensionali. Anche se la connessione viene gestita direttamente da Analysis Services, le finestre di progettazione in [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] usate per la compilazione di soluzioni non sono in grado di connettersi a un'origine dati ODBC, anche quando si usano driver MSDASQL. Se i requisiti aziendali includono un'origine dati ODBC, provare invece a compilare una soluzione tabulare.  
  
 <sup>2</sup> per altre informazioni, vedere [!INCLUDE[ssSDS](../../includes/sssds-md.md)]via [azure.microsoft.com](https://go.microsoft.com/fwlink/?LinkID=157856).  
  
 <sup>3</sup> per altre informazioni sul [!INCLUDE[ssSDS](../../includes/sssds-md.md)] PDW, vedere [SQL Server Parallel Data Warehouse](https://go.microsoft.com/fwlink/?LinkId=150895).  
  
 <sup>4</sup> in alcuni casi, tramite il provider OLE DB MSDAORA può determinare errori di connessione, in particolare con le versioni più recenti di Oracle. Se vengono visualizzati degli errori, è consigliabile utilizzare uno dei provider elencati per Oracle.  
  
 <sup>5</sup> alcune funzionalità richiedono un database relazionale di SQL Server che viene eseguito in locale. In particolare, per il writeback e l'archiviazione ROLAP viene richiesto che l'origine dati sottostante sia un database relazionale di SQL Server.  
  
## <a name="see-also"></a>Vedere anche  
 [Origini dati supportate &#40;SSAS tabulare&#41;](../tabular-models/data-sources-supported-ssas-tabular.md)   
 [Origini dati nei modelli multidimensionali](data-sources-in-multidimensional-models.md)   
 [Viste origine dati in modelli multidimensionali](data-source-views-in-multidimensional-models.md)  
  
  
