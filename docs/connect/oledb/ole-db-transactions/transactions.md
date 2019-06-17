---
title: Le transazioni | Microsoft Docs
description: Transazioni nel driver OLE DB per SQL Server
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- OLE DB, transactions
- transactions [OLE DB]
- OLE DB Driver for SQL Server, transactions
author: pmasl
ms.author: pelopes
manager: jroth
ms.openlocfilehash: 0c5fc4c691902415455b2d8139b34cc39438f96d
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/07/2019
ms.locfileid: "66795969"
---
# <a name="transactions"></a>Transazioni
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  Il Driver OLE DB per SQL Server implementa il supporto delle transazioni locali. Il consumer può utilizzare transazioni distribuite o coordinate tramite Microsoft Distributed Transaction Coordinator (MS DTC). Per i consumer che richiedono il controllo delle transazioni in più sessioni, il driver OLE DB per SQL Server consente di partecipare alle transazioni avviate e gestite grazie a MS DTC.  
  
 Per impostazione predefinita, il driver OLE DB per SQL Server usa una modalità di transazione con autocommit, in cui ogni azione discreta in una sessione di tipo consumer comprende una transazione completa su un'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. La modalità autocommit del driver OLE DB per SQL Server è locale e le transazioni con autocommit non coinvolgono mai più di una sessione.  
  
 Il driver OLE DB per SQL Server espone l'interfaccia **ITransactionLocal**, consentendo al consumer di usare in modo esplicito e implicito le transazioni iniziali in una singola connessione a un'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Il Driver OLE DB per SQL Server non supporta le transazioni locali nidificate.  
  
## <a name="in-this-section"></a>Contenuto della sezione  
  
-   [Supporto delle transazioni locali](../../oledb/ole-db-transactions/supporting-local-transactions.md)  
  
-   [Supporto di transazioni distribuite](../../oledb/ole-db-transactions/supporting-distributed-transactions.md)  
  
-   [I livelli di isolamento &#40;OLE DB&#41;](../../oledb/ole-db-transactions/isolation-levels-ole-db.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Driver OLE DB per programmazione con SQL Server](../../oledb/ole-db/oledb-driver-for-sql-server-programming.md)  
  
  
