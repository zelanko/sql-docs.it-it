---
title: Tipi di dati SQL Server e ADO.NET
description: Viene descritto come usare i tipi di dati SQL Server e il modo in cui interagiscono con i tipi di dati .NET.
ms.date: 08/15/2019
ms.assetid: 81b43550-23e8-43bb-b460-7eb8ac825c33
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: rothja
ms.author: jroth
ms.reviewer: v-kaywon
ms.openlocfilehash: 46edb611f29c447f7e1ca2228212ef3e0d594fff
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/31/2020
ms.locfileid: "75244036"
---
# <a name="sql-server-data-types-and-adonet"></a>Tipi di dati SQL Server e ADO.NET

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[Scaricare ADO.NET](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

Poiché SQL Server e .NET sono basati su sistemi di tipo diverso, è possibile che si verifichi una potenziale perdita di dati. Per mantenere l'integrità dei dati, il provider di dati Microsoft SqlClient per SQL Server (<xref:Microsoft.Data.SqlClient>) offre metodi di accesso tipizzati per l'utilizzo di dati di SQL Server. È possibile usare le enumerazioni nelle classi <xref:System.Data.SqlDbType> per specificare i tipi di dati <xref:Microsoft.Data.SqlClient.SqlParameter>.  
  
SQL Server 2008 introduce nuovi tipi di dati progettati per soddisfare le esigenze aziendali di utilizzo di dati di data e ora, strutturati, semistrutturati e non strutturati. Questi tipi sono presentati nella documentazione online di SQL Server 2008.  
  
I tipi di dati di SQL Server disponibili per l'utilizzo nell'applicazione dipendono dalla versione di SQL Server in uso. Per altre informazioni, vedere [Tipi di dati (motore di database)](https://go.microsoft.com/fwlink/?LinkID=107468) nella documentazione online di SQL Server.
  
## <a name="in-this-section"></a>Contenuto della sezione  
[SqlTypes e DataSet](sqltypes-dataset.md)  
Viene descritto il supporto di tipi per `SqlTypes` in `DataSet`.  
  
[Gestione dei valori NULL](handle-null-values.md)  
Illustra come usare i valori Null e la logica a tre valori.  
  
[Confronto tra GUID e valori uniqueidentifier](compare-guid-uniqueidentifier-values.md)  
Illustra come usare valori GUID e uniqueidentifier in SQL Server e .NET.  
  
[Dati relativi a data e ora](date-time-data.md)  
Descrive come usare i nuovi tipi di dati di data e ora introdotti in SQL Server 2008.  
  
[Tipi definiti dall'utente di grandi dimensioni](large-udts.md)  
Descrive come recuperare i dati dai tipi definiti dall'utente con valori di grandi dimensioni introdotti in SQL Server 2008.  
  
[Dati XML in SQL Server](xml-data-sql-server.md)  
Descrive come usare i dati XML recuperati da SQL Server.  
  
## <a name="reference"></a>Informazioni di riferimento  
<xref:System.Data.DataSet>  
Descrive la classe `DataSet` e tutti i relativi membri.  
  
<xref:System.Data.SqlTypes>  
Descrive lo spazio dei nomi `SqlTypes` e tutti i relativi membri.  
  
<xref:System.Data.SqlDbType>  
Descrive l'enumerazione `SqlDbType` e tutti i relativi membri.  
  
<xref:System.Data.DbType>  
Descrive l'enumerazione `DbType` e tutti i relativi membri.  
  
## <a name="next-steps"></a>Passaggi successivi
- [Parametri con valori di tabella](table-valued-parameters.md)
- [Dati binari e con valori di grandi dimensioni di SQL Server](sql-server-binary-large-value-data.md)
