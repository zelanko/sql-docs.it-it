---
title: Installazione di esempio della copia bulk
description: Descrive le tabelle usate negli esempi di copia bulk e fornisce script SQL per la creazione delle tabelle nel database AdventureWorks.
ms.date: 09/30/2019
dev_langs:
- sql
ms.assetid: d4dde6ac-b8b6-4593-965a-635c8fb2dadb
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: rothja
ms.author: jroth
ms.reviewer: v-kaywon
ms.openlocfilehash: 4b156f3f9deeb6f74393631555c0fc8ad0e9acf2
ms.sourcegitcommit: 610e49c3e1fa97056611a85e31e06ab30fd866b1
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/07/2020
ms.locfileid: "78897041"
---
# <a name="bulk-copy-example-setup"></a>Installazione di esempio della copia bulk

[!INCLUDE[Driver_ADONET_Download](../../../includes/driver_adonet_download.md)]

La classe <xref:Microsoft.Data.SqlClient.SqlBulkCopy> può essere usata per scrivere dati solo in tabelle di SQL Server. Negli esempi di codice illustrati in questo argomento viene usato il database di esempio di SQL Server, **AdventureWorks**. Per evitare di modificare le tabelle esistenti, gli esempi di codice scrivono i dati in tabelle che è prima necessario creare.  
  
Le tabelle **BulkCopyDemoMatchingColumns** e **BulkCopyDemoDifferentColumns** sono entrambe basate sulla tabella **Production.Products** di **AdventureWorks**. Negli esempi di codice che usano queste tabelle, i dati vengono aggiunti dalla tabella **Production.Products** a una di queste tabelle di esempio. La tabella **BulkCopyDemoDifferentColumns** viene usata quando l'esempio illustra come eseguire il mapping delle colonne dall'origine dati alla tabella di destinazione. **BulkCopyDemoMatchingColumns** viene usata per la maggior parte degli altri esempi.  
  
Alcuni esempi di codice illustrano come usare una sola classe <xref:Microsoft.Data.SqlClient.SqlBulkCopy> per scrivere in più tabelle. Per questi esempi, vengono usate le tabelle **BulkCopyDemoOrderHeader** e **BulkCopyDemoOrderDetail** come tabelle di destinazione. Queste tabelle sono basate sulle tabelle **Sales.SalesOrderHeader** e **Sales.SalesOrderDetail** del database **AdventureWorks**.  
  
> [!NOTE]
>  Negli esempi di codice di **SqlBulkCopy** viene illustrata la sintassi che consente di usare solo **SqlBulkCopy**. Se le tabelle di origine e di destinazione si trovano nella stessa istanza di SQL Server, è più semplice e rapido usare un'istruzione Transact-SQL `INSERT … SELECT` per copiare i dati.  
  
## <a name="table-setup"></a>Impostazione delle tabelle  
Per creare le tabelle necessarie per il corretto funzionamento degli esempi di codice, è necessario eseguire le seguenti istruzioni Transact-SQL in un database di SQL Server.  
  
```sql
USE AdventureWorks  
  
IF EXISTS (SELECT * FROM dbo.sysobjects   
 WHERE id = object_id(N'[dbo].[BulkCopyDemoMatchingColumns]')  
 AND OBJECTPROPERTY(id, N'IsUserTable') = 1)  
    DROP TABLE [dbo].[BulkCopyDemoMatchingColumns]  
  
CREATE TABLE [dbo].[BulkCopyDemoMatchingColumns]([ProductID] [int] IDENTITY(1,1) NOT NULL,  
    [Name] [nvarchar](50) NOT NULL,  
    [ProductNumber] [nvarchar](25) NOT NULL,  
 CONSTRAINT [PK_ProductID] PRIMARY KEY CLUSTERED  
(  
    [ProductID] ASC  
) ON [PRIMARY]) ON [PRIMARY]  
  
IF EXISTS (SELECT * FROM dbo.sysobjects   
 WHERE id = object_id(N'[dbo].[BulkCopyDemoDifferentColumns]')  
 AND OBJECTPROPERTY(id, N'IsUserTable') = 1)  
    DROP TABLE [dbo].[BulkCopyDemoDifferentColumns]  
  
CREATE TABLE [dbo].[BulkCopyDemoDifferentColumns]([ProdID] [int] IDENTITY(1,1) NOT NULL,  
    [ProdNum] [nvarchar](25) NOT NULL,  
    [ProdName] [nvarchar](50) NOT NULL,  
 CONSTRAINT [PK_ProdID] PRIMARY KEY CLUSTERED  
(  
    [ProdID] ASC  
) ON [PRIMARY]) ON [PRIMARY]  
  
IF EXISTS (SELECT * FROM dbo.sysobjects   
 WHERE id = object_id(N'[dbo].[BulkCopyDemoOrderHeader]')  
 AND OBJECTPROPERTY(id, N'IsUserTable') = 1)  
    DROP TABLE [dbo].[BulkCopyDemoOrderHeader]  
  
CREATE TABLE [dbo].[BulkCopyDemoOrderHeader]([SalesOrderID] [int] IDENTITY(1,1) NOT NULL,  
    [OrderDate] [datetime] NOT NULL,  
    [AccountNumber] [nvarchar](15) NULL,  
 CONSTRAINT [PK_SalesOrderID] PRIMARY KEY CLUSTERED  
(  
    [SalesOrderID] ASC  
) ON [PRIMARY]) ON [PRIMARY]  
  
IF EXISTS (SELECT * FROM dbo.sysobjects   
 WHERE id = object_id(N'[dbo].[BulkCopyDemoOrderDetail]')  
 AND OBJECTPROPERTY(id, N'IsUserTable') = 1)  
    DROP TABLE [dbo].[BulkCopyDemoOrderDetail]  
  
CREATE TABLE [dbo].[BulkCopyDemoOrderDetail]([SalesOrderID] [int] NOT NULL,  
    [SalesOrderDetailID] [int] NOT NULL,  
    [OrderQty] [smallint] NOT NULL,  
    [ProductID] [int] NOT NULL,  
    [UnitPrice] [money] NOT NULL,  
 CONSTRAINT [PK_LineNumber] PRIMARY KEY CLUSTERED  
(  
    [SalesOrderID] ASC,  
    [SalesOrderDetailID] ASC  
) ON [PRIMARY]) ON [PRIMARY]  
```  
  
## <a name="next-steps"></a>Passaggi successivi
- [Operazioni di copia bulk in SQL Server](bulk-copy-operations-sql-server.md)
