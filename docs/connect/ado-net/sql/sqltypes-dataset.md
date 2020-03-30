---
title: SqlTypes e DataSet
description: Viene descritto il supporto dei tipi per SqlTypes in DataSet.
ms.date: 08/15/2019
dev_langs:
- csharp
ms.assetid: 9172c20a-9876-4b3b-9c97-1963c02b1993
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: rothja
ms.author: jroth
ms.reviewer: v-kaywon
ms.openlocfilehash: 0a75aca978847a4e1e54f4933bd6ec7fe708a4e3
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/29/2020
ms.locfileid: "78896215"
---
# <a name="sqltypes-and-the-dataset"></a>SqlTypes e DataSet

[!INCLUDE[Driver_ADONET_Download](../../../includes/driver_adonet_download.md)]

In ADO.NET 2.0 è stato introdotto il supporto dei tipi avanzati per `DataSet` tramite lo spazio dei nomi <xref:System.Data.SqlTypes>. I tipi in <xref:System.Data.SqlTypes> sono progettati per fornire tipi di dati con la stessa semantica e la stessa precisione dei tipi di dati in un database di SQL Server. Ogni tipo di dati in <xref:System.Data.SqlTypes> dispone di un tipo di dati equivalente in SQL Server, con la stessa rappresentazione di dati sottostante.  
  
L'uso di <xref:System.Data.SqlTypes> direttamente in un <xref:System.Data.DataSet> offre diversi vantaggi quando si usano i tipi di dati di SQL Server. <xref:System.Data.SqlTypes> supporta la stessa semantica dei tipi di dati nativi di SQL Server. Specificando uno dei <xref:System.Data.SqlTypes> nella definizione di un <xref:System.Data.DataColumn> si elimina la perdita di precisione che può verificarsi durante la conversione di tipi di dati decimal o numeric in uno dei tipi di dati CLR (Common Language Runtime).  

Nell'esempio di codice seguente viene creato un oggetto <xref:System.Data.DataTable>, in cui vengono definiti esplicitamente i tipi di dati <xref:System.Data.DataColumn> usando <xref:System.Data.SqlTypes> invece dei tipi CLR. Il codice compila <xref:System.Data.DataTable> con i dati della tabella Sales.SalesOrderDetail nel database AdventureWorks in SQL Server. L'output visualizzato nella finestra della console mostra il tipo di dati di ogni colonna e i valori recuperati da SQL Server.  
  
[!code-csharp[DataWorks DataColumn_DataType#1](~/../sqlclient/doc/samples/DataColumn_DataType.cs#1)]
