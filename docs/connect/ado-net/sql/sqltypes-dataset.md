---
title: SqlTypes e DataSet
description: Viene descritto il supporto dei tipi per SqlTypes nel DataSet.
ms.date: 08/15/2019
dev_langs:
- csharp
ms.assetid: 9172c20a-9876-4b3b-9c97-1963c02b1993
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: v-kaywon
ms.author: v-kaywon
ms.reviewer: rothja
ms.openlocfilehash: 70efb8615a70677c709abd6d9129c63de9420ffc
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 10/16/2019
ms.locfileid: "72451980"
---
# <a name="sqltypes-and-the-dataset"></a>SqlTypes e DataSet

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[Scaricare ADO.NET](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

In ADO.NET 2,0 è stato introdotto il supporto dei tipi avanzati per la `DataSet` tramite lo spazio dei nomi <xref:System.Data.SqlTypes>. I tipi in <xref:System.Data.SqlTypes> sono progettati per fornire tipi di dati con la stessa semantica e la stessa precisione dei tipi di dati in un database SQL Server. Ogni tipo di dati in <xref:System.Data.SqlTypes> dispone di un tipo di dati equivalente in SQL Server, con la stessa rappresentazione di dati sottostante.  
  
L'utilizzo di <xref:System.Data.SqlTypes> direttamente in una <xref:System.Data.DataSet> conferisce diversi vantaggi quando si utilizzano i tipi di dati di SQL Server. <xref:System.Data.SqlTypes> supporta la stessa semantica di SQL Server tipi di dati nativi. Specificando uno dei <xref:System.Data.SqlTypes> nella definizione di un <xref:System.Data.DataColumn> si elimina la perdita di precisione che può verificarsi durante la conversione di tipi di dati Decimal o numeric in uno dei tipi di dati Common Language Runtime (CLR).  

Nell'esempio di codice seguente viene creato un oggetto <xref:System.Data.DataTable>, in cui vengono definiti esplicitamente i tipi di dati <xref:System.Data.DataColumn> usando <xref:System.Data.SqlTypes> invece dei tipi CLR. Il codice compila <xref:System.Data.DataTable> con i dati della tabella Sales.SalesOrderDetail nel database AdventureWorks in SQL Server. L'output visualizzato nella finestra della console mostra il tipo di dati di ogni colonna e i valori recuperati da SQL Server.  
  
[!code-csharp[DataWorks DataColumn_DataType#1](~/../sqlclient/doc/samples/DataColumn_DataType.cs#1)]
