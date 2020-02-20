---
title: Valori di colonna SQL XML
description: Viene mostrato come recuperare e usare i dati XML recuperati da SQL Server.
ms.date: 08/15/2019
dev_langs:
- csharp
ms.assetid: d97ce4da-f09c-4d1e-85b7-a0ccedd7246a
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: rothja
ms.author: jroth
ms.reviewer: v-kaywon
ms.openlocfilehash: aa02072e139c2446ae67086ef43668af4403890c
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/31/2020
ms.locfileid: "75244005"
---
# <a name="sql-xml-column-values"></a>Valori di colonna SQL XML

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[Scaricare ADO.NET](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

SQL Server supporta il nuovo tipo di dati `xml`. Gli sviluppatori possono recuperare set di risultati che includono questo tipo usando il comportamento standard della classe <xref:Microsoft.Data.SqlClient.SqlCommand>. È possibile recuperare una colonna `xml` come qualsiasi colonna (in un <xref:Microsoft.Data.SqlClient.SqlDataReader>, ad esempio), ma se si vuole usare il contenuto della colonna come XML, è necessario usare un <xref:System.Xml.XmlReader>.  
  
## <a name="example"></a>Esempio  
L'applicazione console seguente seleziona due righe, ciascuna contenente una colonna `xml`, dalla tabella **Sales.Store** nel database **AdventureWorks** per un'istanza <xref:Microsoft.Data.SqlClient.SqlDataReader>. Per ogni riga, il valore della colonna `xml` viene letto usando il metodo <xref:Microsoft.Data.SqlClient.SqlDataReader.GetSqlXml%2A> di <xref:Microsoft.Data.SqlClient.SqlDataReader>. Questo valore viene archiviato in un <xref:System.Xml.XmlReader>. Si noti che è necessario usare <xref:Microsoft.Data.SqlClient.SqlDataReader.GetSqlXml%2A> anziché il metodo <xref:System.Data.IDataRecord.GetValue%2A> se si vuole impostare il contenuto in una variabile <xref:System.Data.SqlTypes.SqlXml>. <xref:System.Data.IDataRecord.GetValue%2A> restituisce il valore della colonna `xml` sotto forma di stringa.  
  
> [!NOTE]
>  Per impostazione predefinita, il database di esempio **AdventureWorks** non viene installato insieme a SQL Server. Per installarlo, è sufficiente eseguire il programma di installazione di SQL Server.  
  
[!code-csharp [SqlDataReader_GetSqlXml#1](~/../sqlclient/doc/samples/SqlDataReader_GetSqlXml.cs#1)]
  
## <a name="next-steps"></a>Passaggi successivi
- <xref:System.Data.SqlTypes.SqlXml>
- [Dati XML in SQL Server](xml-data-sql-server.md)
