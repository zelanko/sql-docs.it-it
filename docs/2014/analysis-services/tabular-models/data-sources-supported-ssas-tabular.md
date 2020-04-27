---
title: Origini dati supportate (SSAS tabulare) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: d6c2b1b3-91fc-4175-af25-509946dc7f24
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 345e733e5c1e90f637efab02a9942e307c2fb9f4
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "66067374"
---
# <a name="data-sources-supported-ssas-tabular"></a>Data Sources Supported (SSAS Tabular)
  In questo argomento vengono descritti i tipi di origini dati che possono essere utilizzati con i modelli tabulari.  
  
 In questo articolo sono contenute le sezioni seguenti:  
  
-   [Origini dati supportate](#bkmk_supported_ds)  
  
-   [Origini non supportate](#bkmk_unsupported_ds)  
  
-   [Suggerimenti per la scelta delle origini dati](#bkmk_tips)  
  
##  <a name="supported-data-sources"></a><a name="bkmk_supported_ds"></a>Origini dati supportate  
 È possibile importare dati dalle origini dati riportate nella tabella seguente. Il programma di installazione di [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]non consente di installare i provider elencati per ogni origine dati. Alcuni provider potrebbero già essere installati con altre applicazioni nel computer; negli altri casi sarà necessario scaricare e installare il provider.  
  
|||||  
|-|-|-|-|  
|Source (Sorgente)|Versioni|Tipo file|Provider <sup>1</sup>|  
|Database di Access|Microsoft Access 2003, 2007, 2010.|Estensione accdb o mdb|Provider OLE DB per ACE 14|  
|Database relazionali di SQL Server|Microsoft SQL Server 2005, 2008, 2008 R2; SQL Server 2012, Microsoft SQL Azure database <sup>2</sup>|(non applicabile)|Provider OLE DB per SQL Server<br /><br /> Provider OLE DB di SQL Server Native Client<br /><br /> Provider OLE DB per SQL Server Native Client 10.0<br /><br /> Provider di dati .NET Framework per SQL Client|  
|SQL Server Parallel data warehouse (PDW) <sup>3</sup>|2008 R2|(non applicabile)|Provider OLE DB per SQL Server PDW|  
|Database relazionali Oracle|Oracle 9i, 10g, 11g.|(non applicabile)|Provider OLE DB Oracle<br /><br /> Provider di dati .NET Framework per il client Oracle<br /><br /> Provider di dati .NET Framework per SQL Server<br /><br /> OraOLEDB<br /><br /> MSDASQL|  
|Database relazionali di Teradata|Teradata V2R6 e V12|(non applicabile)|Provider OLE DB TDOLEDB<br /><br /> Provider di dati .NET per Teradata|  
|Database relazionali di Informix||(non applicabile)|Provider OLE DB per Informix|  
|Database relazionali di IBM DB2|8.1|(non applicabile)|DB2OLEDB|  
|Database relazionali di Sybase Adaptive Server Enterprise (ASE)|15.0.2|(non applicabile)|Provider OLE DB per Sybase|  
|Altri database relazionali|(non applicabile)|(non applicabile)|Provider OLE DB o driver ODBC|  
|File di testo|(non applicabile)|Con estensione txt, tab, csv|Provider OLE DB per ACE 14 per Microsoft Access|  
|File di Microsoft Excel|Excel 97-2003, 2007 e 2010|Con estensione xlsx, xlsm, xlsb, xltx, xltm|Provider OLE DB per ACE 14|  
|[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] cartella di lavoro|Microsoft SQL Server Analysis Services 2008 R2|Con estensione xlsx, xlsm, xlsb, xltx, xltm|ASOLEDB 10.5<br /><br /> (usato solo con le cartelle di lavoro [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] pubblicate nelle farm di SharePoint con [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] installato)|  
|Cubo di Analysis Services|Microsoft SQL Server Analysis Services 2005, 2008 e 2008 R2|(non applicabile)|ASOLEDB 10|  
|Feed di dati<br /><br /> (utilizzato per importare dati dai report di Reporting Services, documenti di servizio Atom, Microsoft Azure Marketplace DataMarket e singoli feed di dati)|Formato Atom 1.0<br /><br /> Qualsiasi database o documento esposto come Windows Communication Foundation (WCF) Data Service (precedentemente ADO.NET Data Services).|Con estensione atomsvc per un documento di servizio che consente di definire uno o più feed<br /><br /> Con estensione atom per un documento di feed Web Atom|Provider di feed di dati Microsoft per [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]<br /><br /> Provider di feed di dati .NET Framework per [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]|  
|File Office Database Connection||Con estensione odc||  
  
 <sup>1</sup> è inoltre possibile utilizzare il Provider di OLE DB per ODBC.  
  
 <sup>2</sup> per ulteriori informazioni su SQL Azure, vedere [SQL Azure](https://go.microsoft.com/fwlink/?LinkID=157856)del sito Web.  
  
 <sup>3</sup> per ulteriori informazioni su SQL Server PDW, vedere il sito web [SQL Server Data warehouse parallelo 2008 R2](https://go.microsoft.com/fwlink/?LinkId=150895).  
  
 <sup>4</sup> in alcuni casi, l'utilizzo del provider OLE DB MSDAORA può causare errori di connessione, in particolare con le versioni più recenti di Oracle. Se vengono visualizzati degli errori, è consigliabile utilizzare uno dei provider elencati per Oracle.  
  
##  <a name="unsupported-sources"></a><a name="bkmk_unsupported_ds"></a>Origini non supportate  
 L'origine dati seguente non è attualmente supportata:  
  
-   I documenti del server, ad esempio i database di Access già pubblicati in SharePoint, non possono essere importati.  
  
##  <a name="tips-for-choosing-data-sources"></a><a name="bkmk_tips"></a>Suggerimenti per la scelta delle origini dati  
  
1.  L'importazione di tabelle dai database relazionali consente di risparmiare alcuni passaggi perché le relazioni di *chiave esterna* vengono utilizzate durante l'importazione per creare relazioni tra tabelle in Progettazione modelli.  
  
2.  È possibile risparmiare alcuni passaggi anche importando più tabelle e quindi eliminando quelle non necessarie. Se si importano le tabelle una alla volta, potrebbe essere ancora necessario creare manualmente le relazioni tra le tabelle.  
  
3.  Le colonne in cui sono contenuti dati simili in origini dati diverse costituiscono la base per la creazione di relazioni all'interno di Progettazione modelli. Quando si utilizzano origini dati eterogenee, scegliere tabelle con colonne di cui è possibile eseguire il mapping alle tabelle in altre origini dati in cui sono contenuti dati identici o simili.  
  
4.  I provider OLE DB offrono talvolta prestazioni migliori in termini di velocità per dati in larga scala. Quando si sceglie tra provider diversi per la stessa origine dati, provare innanzitutto il provider OLE DB.  
  
## <a name="see-also"></a>Vedi anche  
 [Origini dati &#40;SSAS tabulare&#41;](../data-sources-ssas-tabular.md)   
 [Importare dati &#40;SSAS tabulare&#41;](../import-data-ssas-tabular.md)  
  
  
