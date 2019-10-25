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
author: v-kaywon
ms.author: v-kaywon
ms.reviewer: rothja
ms.openlocfilehash: d8dc9d5100f71fed39c1e4166882230451dd139e
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 10/16/2019
ms.locfileid: "72451933"
---
# <a name="sql-xml-column-values"></a>Valori di colonna SQL XML

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[Scaricare ADO.NET](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

SQL Server supporta il nuovo tipo di dati `xml`. Gli sviluppatori possono recuperare set di risultati che includono questo tipo usando il comportamento standard della classe <xref:Microsoft.Data.SqlClient.SqlCommand>. È possibile recuperare una colonna `xml` come qualsiasi colonna venga recuperata (in un <xref:Microsoft.Data.SqlClient.SqlDataReader>, ad esempio), ma se si desidera utilizzare il contenuto della colonna come XML, è necessario utilizzare un <xref:System.Xml.XmlReader>.  
  
## <a name="example"></a>Esempio  
L'applicazione console seguente seleziona due righe, ciascuna contenente una colonna `xml`, dalla tabella **Sales.Store** nel database **AdventureWorks** per un'istanza <xref:Microsoft.Data.SqlClient.SqlDataReader>. Per ogni riga, il valore della colonna `xml` viene letto usando il <xref:Microsoft.Data.SqlClient.SqlDataReader.GetSqlXml%2A> metodo di <xref:Microsoft.Data.SqlClient.SqlDataReader>. Il valore viene archiviato in un <xref:System.Xml.XmlReader>. Si noti che è necessario utilizzare <xref:Microsoft.Data.SqlClient.SqlDataReader.GetSqlXml%2A> anziché il metodo <xref:System.Data.IDataRecord.GetValue%2A> se si desidera impostare il contenuto su una variabile <xref:System.Data.SqlTypes.SqlXml>.  <xref:System.Data.IDataRecord.GetValue%2A> restituisce il valore della colonna `xml` sotto forma di stringa.  
  
> [!NOTE]
>  Per impostazione predefinita, il database di esempio **AdventureWorks** non viene installato insieme a SQL Server. Per installarlo, è possibile eseguire SQL Server installazione.  
  
[!code-csharp[DataWorks SqlDataReader_GetSqlXml#1](~/../sqlclient/doc/samples/SqlDataReader_GetSqlXml.cs#1)]
  
## <a name="next-steps"></a>Passaggi successivi
- <xref:System.Data.SqlTypes.SqlXml>
- [Dati XML in SQL Server](xml-data-sql-server.md)
