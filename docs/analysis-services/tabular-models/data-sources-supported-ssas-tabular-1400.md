---
title: Origini dati supportate nei modelli 1400 tabulari di SQL Server Analysis Services | Microsoft Docs
ms.date: 02/12/2019
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 4c900c6f1683b9f4c96355a759c604022515d2ce
ms.sourcegitcommit: 89a7bd9ccbcb19bb92a1f4ba75576243a58584e8
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/13/2019
ms.locfileid: "56159756"
---
# <a name="data-sources-supported-in-sql-server-analysis-services-tabular-1400-models"></a>Origini dati supportate in SQL Server Analysis Services i modelli tabulari 1400

[!INCLUDE[ssas-appliesto-sql2017](../../includes/ssas-appliesto-sql2017.md)]

Questo articolo descrive i tipi di origini dati che possono essere utilizzate con i modelli tabulari di SQL Server Analysis Services (SSAS) a livello di compatibilità 1400. 

Per modelli tabulari di SSAS a livello di compatibilità 1200 e versioni precedenti, vedere [origini dati supportate nei modelli 1200 tabulari di SQL Server Analysis Services](data-sources-supported-ssas-tabular.md).

Per Azure Analysis Services, vedere [origini dati supportate in Azure Analysis Services](https://docs.microsoft.com/azure/analysis-services/analysis-services-datasource).


## <a name="cloud-data-sources"></a>Origini dati cloud

|Origine dati  |In memoria  |DirectQuery  |
|---------|---------|---------|
|Database SQL di Azure     |   Yes      |    Yes      |
|Azure SQL Data Warehouse     |   Yes      |   Yes       |
|Archiviazione BLOB di Azure     |   Yes       |    No      |
|Archiviazione tabelle di Azure    |   Yes       |    No      |
|Azure Cosmos DB     |  Yes        |  No        |
|Azure Data Lake Store (Gen1)<sup>[1](#gen2)</sup>      |   Yes       |    No      |
|Azure HDInsight HDFS    |     Yes     |   No       |
|Azure HDInsight Spark <sup> [2](#databricks)</sup>     |   Yes       |   No       |
||||

<a name="gen2">1</a> -Gen2 Azure Data Lake Store non è attualmente supportata.   
<a name="databricks">2</a> - azure Databricks tramite il connettore non è attualmente supportato di Spark.   



**Provider**   
In memoria e i modelli DirectQuery, la connessione a origini dati di Azure usano Provider di dati .NET Framework per SQL Server.

## <a name="on-premises-data-sources"></a>Origini dati locali

### <a name="supported-by-in-memory-and-directquery-models"></a>Supportato in memoria e i modelli DirectQuery

|Origine dati | Provider in memoria | Provider DirectQuery |
|  --- | --- | --- |
| SQL Server |SQL Server Native Client 11.0, Provider Microsoft OLE DB per SQL Server, Provider di dati .NET Framework per SQL Server | Provider di dati .NET Framework per SQL Server |
| SQL Server Data Warehouse |SQL Server Native Client 11.0, Provider Microsoft OLE DB per SQL Server, Provider di dati .NET Framework per SQL Server | Provider di dati .NET Framework per SQL Server |
| Oracle |Provider Microsoft OLE DB per Oracle, Provider di dati Oracle per .NET |Provider di dati Oracle per .NET | |
| Teradata |Provider OLE DB per Teradata, Provider di dati Teradata per .NET |Provider di dati Teradata per .NET | |
| | | |

> [!NOTE]
> Per i modelli in memoria, i provider OLE DB possono fornire prestazioni migliori per i dati su larga scala. Quando si sceglie tra provider diversi per la stessa origine dati, provare innanzitutto il provider OLE DB.  

### <a name="supported-by-in-memory-models-only"></a>Supportato da solo modelli in memoria

|Database  |
|---------|---------|---------|
|Database di Access     | 
|SQL Server Analysis Services     | 
|IBM Informix (beta) | 
|Documento JSON     | 
|Righe dal file binario     | 
|Database MySQL     | 
|Database PostgreSQL    | Yes | No
|SAP HANA   | Yes | No
|SAP Business Warehouse    | Yes | No
|Database di Sybase     | Yes | No
|||

|File  |  
|---------|---------|
|Cartella di lavoro di Excel     |
|Cartella     | 
|JSON | 
|Testo/CSV    | 
|Tabella XML    | 
|||

|Servizi online  |  
|---------|---------|
|Dynamics 365      |
|Exhange Online     |
|Oggetti Salesforce    | 
|Report di Salesforce     |
|Elenchi SharePoint Online     |
|||

|Altro  |  
|---------|---------|
|Active Directory      | 
|Forum di Exhange     |  
|Feed OData     | 
|Query ODBC     | 
|OLE DB  | 
|Elenco di SharePoint | 
|||

## <a name="see-also"></a>Vedere anche

[Origini dati supportate in SQL Server Analysis Services i modelli tabulari 1200](data-sources-supported-ssas-tabular.md)

[Origini dati supportate in Azure Analysis Services](https://docs.microsoft.com/azure/analysis-services/analysis-services-datasource)   
