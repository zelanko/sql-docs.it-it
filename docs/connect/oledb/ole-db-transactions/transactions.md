---
title: Transazioni (OLE DB Driver)
description: Informazioni su come OLE DB Driver per SQL Server supporta le transazioni locali. Usare Microsoft Distributed Transaction Coordinator per le transazioni distribuite.
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e146dd9bc1f560cba4bf1902909dd6b8b317698f
ms.sourcegitcommit: c95f3ef5734dec753de09e07752a5d15884125e2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/25/2020
ms.locfileid: "88861847"
---
# <a name="transactions"></a>Transazioni
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  OLE DB Driver per SQL Server implementa il supporto delle transazioni locali. Il consumer può utilizzare transazioni distribuite o coordinate tramite Microsoft Distributed Transaction Coordinator (MS DTC). Per i consumer che richiedono il controllo delle transazioni in più sessioni, il driver OLE DB per SQL Server consente di partecipare alle transazioni avviate e gestite grazie a MS DTC.  
  
 Per impostazione predefinita, il driver OLE DB per SQL Server usa una modalità di transazione con autocommit, in cui ogni azione discreta in una sessione di tipo consumer comprende una transazione completa su un'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. La modalità autocommit del driver OLE DB per SQL Server è locale e le transazioni con autocommit non coinvolgono mai più di una sessione.  
  
 Il driver OLE DB per SQL Server espone l'interfaccia **ITransactionLocal**, consentendo al consumer di usare in modo esplicito e implicito le transazioni iniziali in una singola connessione a un'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. OLE DB Driver per SQL Server non supporta le transazioni locali annidate.  
  
## <a name="in-this-section"></a>Contenuto della sezione  
  
-   [Supporto delle transazioni locali](../../oledb/ole-db-transactions/supporting-local-transactions.md)  
  
-   [Supporto di transazioni distribuite](../../oledb/ole-db-transactions/supporting-distributed-transactions.md)  
  
-   [Livelli di isolamento &#40;OLE DB&#41;](../../oledb/ole-db-transactions/isolation-levels-ole-db.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Driver OLE DB per programmazione con SQL Server](../../oledb/ole-db/oledb-driver-for-sql-server-programming.md)  
  
  
