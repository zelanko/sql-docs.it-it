---
title: Tipi di dati SQL Server e ADO.NET
description: Viene descritto come usare i tipi di dati SQL Server e il modo in cui interagiscono con i tipi di dati .NET.
ms.date: 08/15/2019
ms.assetid: 81b43550-23e8-43bb-b460-7eb8ac825c33
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: v-kaywon
ms.author: v-kaywon
ms.reviewer: rothja
ms.openlocfilehash: 12ad13d6788ae2b8995289100883b06c5ab6d7c6
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 10/16/2019
ms.locfileid: "72452032"
---
# <a name="sql-server-data-types-and-adonet"></a>Tipi di dati SQL Server e ADO.NET

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[Scaricare ADO.NET](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

SQL Server e .NET sono basati su sistemi di tipi diversi, il che può comportare una potenziale perdita di dati. Per mantenere l'integrità dei dati, il provider di dati Microsoft SqlClient per SQL Server (<xref:Microsoft.Data.SqlClient>) fornisce metodi di accesso tipizzati per l'utilizzo di dati SQL Server. È possibile usare le enumerazioni nelle classi <xref:System.Data.SqlDbType> per specificare <xref:Microsoft.Data.SqlClient.SqlParameter> tipi di dati.  
  
SQL Server 2008 introduce nuovi tipi di dati progettati per soddisfare le esigenze aziendali per lavorare con dati di data e ora, strutturati, semistrutturati e non strutturati. Questi tipi sono presentati nella documentazione online di SQL Server 2008.  
  
I tipi di dati SQL Server disponibili per l'utilizzo nell'applicazione dipendono dalla versione di SQL Server in uso. Per ulteriori informazioni, vedere [tipi di dati (motore di database)](https://go.microsoft.com/fwlink/?LinkID=107468) da documentazione online di SQL Server.
  
## <a name="in-this-section"></a>Contenuto della sezione  
[SqlTypes e DataSet](sqltypes-dataset.md)  
Viene descritto il supporto di tipi per `SqlTypes` in `DataSet`.  
  
[Gestione dei valori NULL](handle-null-values.md)  
Viene illustrato come utilizzare i valori null e la logica a tre valori.  
  
[Confronto tra GUID e valori uniqueidentifier](compare-guid-uniqueidentifier-values.md)  
Viene illustrato come utilizzare i valori GUID e uniqueidentifier in SQL Server e .NET.  
  
[Dati relativi a data e ora](date-time-data.md)  
Viene descritto come utilizzare i nuovi tipi di dati di data e ora introdotti in SQL Server 2008.  
  
[Tipi definiti dall'utente di grandi dimensioni](large-udts.md)  
Viene illustrato come recuperare dati da UDT con valori di grandi dimensioni introdotti in SQL Server 2008.  
  
[Dati XML in SQL Server](xml-data-sql-server.md)  
Viene descritto come utilizzare i dati XML recuperati da SQL Server.  
  
## <a name="reference"></a>Riferimento  
<xref:System.Data.DataSet>  
Descrive la classe `DataSet` e tutti i relativi membri.  
  
<xref:System.Data.SqlTypes>  
Vengono descritti lo spazio dei nomi `SqlTypes` e tutti i relativi membri.  
  
<xref:System.Data.SqlDbType>  
Descrive l'enumerazione `SqlDbType` e tutti i relativi membri.  
  
<xref:System.Data.DbType>  
Descrive l'enumerazione `DbType` e tutti i relativi membri.  
  
## <a name="next-steps"></a>Passaggi successivi
- [Parametri con valori di tabella](table-valued-parameters.md)
- [Dati binari e con valori di grandi dimensioni di SQL Server](sql-server-binary-large-value-data.md)
