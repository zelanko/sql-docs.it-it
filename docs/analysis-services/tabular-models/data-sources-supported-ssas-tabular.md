---
title: Origini dati supportate nei modelli 1200 tabulari di SQL Server Analysis Services | Microsoft Docs
ms.date: 07/02/2019
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: a1ef7ae48e3d1500d08c9adba5e39db6214125c5
ms.sourcegitcommit: d9c5b9ab3c282775ed61712892eeb3e150ccc808
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/05/2019
ms.locfileid: "67597355"
---
# <a name="data-sources-supported-in-sql-server-analysis-services-tabular-1200-models"></a>Origini dati supportate in SQL Server Analysis Services i modelli tabulari 1200
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  
Questo articolo descrive i tipi di origini dati che possono essere utilizzate con modelli tabulari di SQL Server Analysis Services a 1200 e livello di compatibilità inferiore. 

Per i modelli con i livelli di compatibilità 1400, vedere [origini dati supportate nei modelli 1400 tabulari di SQL Server Analysis Services](data-sources-supported-ssas-tabular-1400.md).

Per Azure Analysis Services, vedere [origini dati supportate in Azure Analysis Services](https://docs.microsoft.com/azure/analysis-services/analysis-services-datasource).
  
##  <a name="bkmk_supported_ds"></a> Origini dati supportate per i modelli tabulari in memoria  
Il programma di installazione di [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]non consente di installare i provider elencati per ogni origine dati. Alcuni provider potrebbero essere installati con altre applicazioni nel computer. In altri casi, potrebbe essere necessario scaricare e installare il provider.  
  
|||||  
|-|-|-|-|  
|`Source`|Versioni|Tipo di file|Provider|  
|Database di Access|Microsoft Access 2010 e versioni successive.|Estensione accdb o mdb|14 provider OLE DB per ACE <sup> [1](#dnu)</sup>|  
|Database relazionali di SQL Server|SQL Server 2008 e versioni successive, SQL Server Data Warehouse 2008 e versioni successive, Azure SQL Database, Azure SQL Data Warehouse, Analitica piattaforma di strumenti analitici<br /><br /> <br /><br /> Analitica piattaforma di strumenti analitici era precedentemente noto come SQL Server Parallel Data Warehouse (PDW). Originariamente la connessione a PDW da Analysis Services richiedeva un provider di dati speciale. Questo provider è stato sostituito in SQL Server 2012. A partire da SQL Server 2012, per le connessioni a PDW/piattaforma di strumenti analitici viene usato SQL Server Native Client. |(non applicabile)|Provider OLE DB per SQL Server<br /><br /> Provider OLE DB di SQL Server Native Client<br /><br /> Provider OLE DB per SQL Server Native Client 10.0<br /><br /> Provider di dati .NET Framework per SQL Client|  
|Database relazionali Oracle|Oracle 9i e versioni successive.|(non applicabile)|Provider OLE DB Oracle<br /><br /> Provider di dati .NET Framework per il client Oracle<br /><br /> Provider di dati .NET Framework per SQL Server<br /><br /> OraOLEDB<br /><br /> MSDASQL|  
|Database relazionali di Teradata|Teradata V2R6 e versioni successive|(non applicabile)|Provider OLE DB TDOLEDB<br /><br /> Provider di dati .NET per Teradata|  
|Database relazionali di Informix||(non applicabile)|Provider OLE DB per Informix|  
|Database relazionali di IBM DB2|8.1|(non applicabile)|DB2OLEDB|  
|Database relazionali di Sybase Adaptive Server Enterprise (ASE)|15.0.2|(non applicabile)|Provider OLE DB per Sybase|  
|Altri database relazionali|(non applicabile)|(non applicabile)|Provider OLE DB o driver ODBC|  
|File di testo|(non applicabile)|Con estensione txt, tab, csv|14 provider OLE DB per ACE <sup> [1](#dnu)</sup> |  
|File di Microsoft Excel|Excel 2010 e versioni successive|Con estensione xlsx, xlsm, xlsb, xltx, xltm|14 provider OLE DB per ACE <sup> [1](#dnu)</sup>|  
|[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] cartella di lavoro|Microsoft SQL Server 2008 e versioni successive di Analysis Services|Con estensione xlsx, xlsm, xlsb, xltx, xltm|ASOLEDB 10.5<br /><br /> (usato solo con le cartelle di lavoro [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] pubblicate nelle farm di SharePoint con [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] installato)|  
|Cubo di Analysis Services|Microsoft SQL Server 2008 e versioni successive di Analysis Services|(non applicabile)|ASOLEDB 10|  
|Feed di dati<br /><br /> (utilizzato per importare dati dai report di Reporting Services, documenti di servizio Atom, Microsoft Azure Marketplace DataMarket e singoli feed di dati)|Formato Atom 1.0<br /><br /> Qualsiasi database o documento esposto come Windows Communication Foundation (WCF) Data Service (precedentemente ADO.NET Data Services).|`.atomsvc` per un documento di servizio che definisce uno o più feed<br /><br /> Con estensione atom per un documento di feed Web Atom|Provider di feed di dati Microsoft per [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]<br /><br /> Provider di feed di dati .NET Framework per [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]|  
|File Office Database Connection||Con estensione odc||  
 
<a name="dnu">[1] </a> Using **provider OLE DB ACE 14** per connettersi ai tipi di dati file **non è consigliabile**. Se è necessario mantenere i modelli con livello di compatibilità tabulare 1200 e versioni precedenti, esportare i dati in un tipo di file csv, importare nel database SQL e quindi connettersi a e importare dal database. Tuttavia, è consigliabile eseguire l'aggiornamento a livello di compatibilità 1400 tabulare (SQL Server 2017 e versioni successive) e usare **recupera dati** in SSDT selezionare e importare l'origine dati di file. Ottieni utilizzi i dati strutturati connessioni all'origine dati fornite dal motore dati di Power Query, che sono più stabile rispetto alle connessioni di provider OLE DB ACE 14.  


##  <a name="bkmk_supported_ds_dq"></a> Origini dati supportate per i modelli DirectQuery  
 DirectQuery rappresenta un'alternativa alla modalità di archiviazione in memoria perché instrada le query ai sistemi di dati di backend e restituisce i risultati direttamente da tali sistemi anziché archiviare tutti i dati all'interno del modello (e nella RAM una volta caricato il modello). Poiché Analysis Services deve formulare query nella sintassi di query nativo del database, un sottoinsieme più piccolo di origini dati è supportato per questa modalità.  
  
Origine dati   |Versioni  |Provider
---------|---------|---------
Microsoft SQL Server    |  2008 e versioni successive      |       Provider OLE DB per SQL Server, provider OLE DB di SQL Server Native Client, provider di dati .NET Framework per SQL Client  
Database SQL di Microsoft Azure    |   All      |  Provider OLE DB per SQL Server, provider OLE DB di SQL Server Native Client, provider di dati .NET Framework per SQL Client            
Microsoft Azure SQL Data Warehouse     |   All     |  Provider OLE DB di SQL Server Native Client, provider di dati .NET Framework per SQL Client       
Piattaforma di strumenti analitici Microsoft SQL     |   All      |  Provider OLE DB per SQL Server, provider OLE DB di SQL Server Native Client, provider di dati .NET Framework per SQL Client       
|Microsoft SQL Server Always Encrypted <sup>[2](#ae)</sup> | 2016 e versioni successive. 2014 e versioni precedenti solo Enterprise edition. | Provider di dati .NET Framework per SQL Client
|Database SQL di Azure di Always Encrypted <sup> [2](#ae)</sup>| All | Provider di dati .NET Framework per SQL Client
Database relazionali Oracle     |  Oracle 9i e versioni successive       |  Provider OLE DB Oracle       
Database relazionali di Teradata    |  Teradata V2R6 e versioni successive     | Provider di dati .NET per Teradata    


### <a name="using-sql-server-analysis-services-with-always-encrypted"></a>Con SQL Server Analysis Services con Always Encrypted

<a name="ae">[2] </a> SQL Server Analysis Services può fungere da client a un database usando [Always Encrypted](../../relational-databases/security/encryption/always-encrypted-database-engine.md) in SQL Server o Database SQL di Azure nelle condizioni seguenti: 

*  Chiavi master della colonna proteggere le colonne crittografate devono essere certificati, archiviati nell'archivio certificati Windows. Chiavi master della colonna archiviate in Azure Key Vault non sono supportate.   
*  Il computer Windows in cui è installato Analysis Services ha installati i certificati di chiave master della colonna necessari. Per altre informazioni, vedere [creazione di chiavi Master della colonna in Windows Store di certificato](../../relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted.md#creating-column-master-keys-in-windows-certificate-store).
*  L'origine dati Analysis Services viene utilizzato per connettersi a SQL si basa su .net Framework provider e l'impostazione di crittografia di colonna proprietà dell'origine dati deve essere abilitato. .NET framework 4.6.1 o versioni successive deve essere presente nel server di Analysis Services.
*  L'origine dati di SQL Server o Database SQL deve essere un *provider* tipo origine dati supportato da livello di compatibilità 1200. Non funzionerà con Power Query *strutturati* zdroje dat, introdotti nel livello di compatibilità 1400.
  
##  <a name="bkmk_tips"></a> Suggerimenti per la scelta delle origini dati  
  
L'importazione di tabelle dai database relazionali consente di risparmiare alcuni passaggi perché le relazioni di *chiave esterna* vengono utilizzate durante l'importazione per creare relazioni tra tabelle in Progettazione modelli.  
  
È possibile risparmiare alcuni passaggi anche importando più tabelle e quindi eliminando quelle non necessarie. Se si importano le tabelle una alla volta, potrebbe essere ancora necessario creare manualmente le relazioni tra le tabelle.  
  
Le colonne in cui sono contenuti dati simili in origini dati diverse costituiscono la base per la creazione di relazioni all'interno di Progettazione modelli. Quando si utilizzano origini dati eterogenee, scegliere tabelle con colonne di cui è possibile eseguire il mapping alle tabelle in altre origini dati in cui sono contenuti dati identici o simili.  
  
Provider OLE DB offrono talvolta prestazioni più veloci per i dati su larga scala. Quando si sceglie tra provider diversi per la stessa origine dati, provare innanzitutto il provider OLE DB.  

## <a name="see-also"></a>Vedere anche

[Origini dati supportate in SQL Server Analysis Services i modelli tabulari 1400](data-sources-supported-ssas-tabular-1400.md)

[Origini dati supportate in Azure Analysis Services](https://docs.microsoft.com/azure/analysis-services/analysis-services-datasource)   
