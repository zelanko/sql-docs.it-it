---
title: Quando usare il driver OLE DB per SQL Server | Microsoft Docs
description: Quando usare il driver OLE DB per SQL Server
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- OLE DB Driver for SQL Server
- MSOLEDBSQL, about OLE DB Driver for SQL Server
- data access [OLE DB Driver for SQL Server], about OLE DB Driver for SQL Server
author: pmasl
ms.author: pelopes
manager: jroth
ms.openlocfilehash: 210a15d827cb8f0a828c11c1c8fe87586cd79028
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/07/2019
ms.locfileid: "66795877"
---
# <a name="when-to-use-ole-db-driver-for-sql-server"></a>Quando usare il driver OLE DB per SQL Server
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../includes/driver_oledb_download.md)]

  Driver OLE DB per SQL Server è una tecnologia che è possibile usare per accedere ai dati in un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] database.  Per una discussione sulle diverse tecnologie di accesso ai dati, vedere [Panoramica delle tecnologie di accesso ai dati](https://go.microsoft.com/fwlink/?LinkID=179186)  
  
 Quando si decide se usare il driver OLE DB per SQL Server come tecnologia di accesso ai dati dell'applicazione, è necessario considerare diversi fattori.  
  
 Per le nuove applicazioni, se si utilizza un linguaggio di programmazione gestito, come Microsoft Visual C# o Visual Basic, e si desidera accedere alle nuove caratteristiche di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], è necessario utilizzare il provider di dati .NET Framework per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], incluso in .NET Framework.  
  
 L'uso del driver OLE DB per SQL Server è consigliabile se si sviluppa un'applicazione basata su COM e si ha l'esigenza di accedere alle nuove caratteristiche introdotte in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se non è necessario accedere alle nuove caratteristiche di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], è possibile continuare a utilizzare Windows Data Access Components (WDAC).  
  
 Per le applicazioni OLE DB esistenti, il problema principale è dato dalla necessità o meno di accedere alle nuove caratteristiche di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. In caso di un'applicazione obsoleta per la quale non sono richieste le nuove funzionalità di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], è possibile continuare a utilizzare WDAC. Se tuttavia è necessario accedere a queste funzionalità, ad esempio al [tipo di dati xml](../../t-sql/xml/xml-transact-sql.md), è consigliabile usare il driver OLE DB per SQL Server.  
  
 Entrambi Driver OLE DB per SQL Server che MDAC supportano l'isolamento di commit della transazione usando il controllo delle versioni di riga, ma solo Driver OLE DB per SQL Server supporta l'isolamento della transazione snapshot read. In termini di programmazione, l'isolamento delle transazioni Read Committed mediante il controllo delle versioni delle righe equivale a una transazione Read Committed.  
  
 Per informazioni sulle differenze tra il Driver OLE DB per SQL Server e MDAC, vedere [aggiornamento di un'applicazione al Driver OLE DB per SQL Server da MDAC](../oledb/applications/updating-an-application-to-oledb-driver-for-sql-server-from-mdac.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Driver OLE DB per SQL Server](../oledb/oledb-driver-for-sql-server.md)     
 [Procedure relative a OLE DB](../oledb/ole-db-how-to/ole-db-how-to-topics.md)  
  
  
