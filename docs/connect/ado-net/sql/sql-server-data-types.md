---
title: Tipi di dati SQL Server e ADO.NET
description: Viene descritto come usare i tipi di dati SQL Server e il modo in cui interagiscono con i tipi di dati .NET.
ms.date: 08/15/2019
ms.assetid: 81b43550-23e8-43bb-b460-7eb8ac825c33
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-kaywon
ms.openlocfilehash: d2cfd61efa1ffed78b96f4ef22e01de20f200dfb
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/08/2020
ms.locfileid: "80920970"
---
# <a name="sql-server-data-types-and-adonet"></a>Tipi di dati SQL Server e ADO.NET

[!INCLUDE[Driver_ADONET_Download](../../../includes/driver_adonet_download.md)]

Poiché SQL Server e .NET sono basati su sistemi di tipo diverso, è possibile che si verifichi una potenziale perdita di dati. Per mantenere l'integrità dei dati, il provider di dati Microsoft SqlClient per SQL Server (<xref:Microsoft.Data.SqlClient>) offre metodi di accesso tipizzati per l'utilizzo di dati di SQL Server. È possibile usare le enumerazioni nelle classi <xref:System.Data.SqlDbType> per specificare i tipi di dati <xref:Microsoft.Data.SqlClient.SqlParameter>.  
  
SQL Server 2008 introduce nuovi tipi di dati progettati per soddisfare le esigenze aziendali di utilizzo di dati di data e ora, strutturati, semistrutturati e non strutturati. Questi tipi sono presentati nella documentazione online di SQL Server 2008.  
  
I tipi di dati di SQL Server disponibili per l'utilizzo nell'applicazione dipendono dalla versione di SQL Server in uso. Per altre informazioni, vedere [Tipi di dati (motore di database)](https://go.microsoft.com/fwlink/?LinkID=107468) nella documentazione online di SQL Server.
  
## <a name="in-this-section"></a>Contenuto della sezione  
[SqlTypes e DataSet](sqltypes-dataset.md)  
Viene descritto il supporto di tipi per `SqlTypes` in `DataSet`.  
  
[Gestione dei valori NULL](handle-null-values.md)  
Illustra come usare i valori Null e la logica a tre valori.  
  
[Confronto tra GUID e valori uniqueidentifier](compare-guid-uniqueidentifier-values.md)  
Viene illustrato come usare i valori GUID e uniqueidentifier in SQL Server e .NET.  
  
[Dati relativi a data e ora](date-time-data.md)  
Descrive come usare i nuovi tipi di dati di data e ora introdotti in SQL Server 2008.  
  
[Tipi definiti dall'utente di grandi dimensioni](large-udts.md)  
Descrive come recuperare i dati dai tipi definiti dall'utente con valori di grandi dimensioni introdotti in SQL Server 2008.  
  
[Dati XML in SQL Server](xml-data-sql-server.md)  
Descrive come usare i dati XML recuperati da SQL Server.  
  
## <a name="reference"></a>Riferimento  
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
