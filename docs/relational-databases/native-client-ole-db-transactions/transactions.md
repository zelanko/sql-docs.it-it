---
title: Transazioni | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- OLE DB, transactions
- transactions [OLE DB]
- SQL Server Native Client OLE DB provider, transactions
ms.assetid: 3b41e33a-c1ca-4b2a-9464-312b0ed3ca89
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: d54dbe8e3df6e930ebd026e638d0a21f2f88f32e
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/07/2019
ms.locfileid: "73772563"
---
# <a name="transactions"></a>Transazioni
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Il provider OLE DB [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client implementa il supporto per le transazioni locali. Il consumer può utilizzare transazioni distribuite o coordinate tramite Microsoft Distributed Transaction Coordinator (MS DTC). Per i consumer che richiedono il controllo delle transazioni che si estende su più sessioni, il provider [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] native client OLE DB può unire in join le transazioni avviate e gestite da MS DTC.  
  
 Per impostazione predefinita, il provider di OLE DB [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] native client utilizza una modalità di transazione con autocommit, in cui ogni azione discreta in una sessione del consumer comprende una transazione completa su un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. La modalità autocommit del provider OLE DB [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client è locale e le transazioni autocommit non si estendono mai a più di una singola sessione.  
  
 Il provider di OLE DB [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client espone l'interfaccia **ITransactionLocal** , consentendo al consumer di utilizzare le transazioni in modo esplicito e implicito in una singola connessione a un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Il provider di OLE DB [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] native client non supporta le transazioni locali nidificate.  
  
## <a name="in-this-section"></a>Contenuto della sezione  
  
-   [Supporto delle transazioni locali](../../relational-databases/native-client-ole-db-transactions/supporting-local-transactions.md)  
  
-   [Supporto di transazioni distribuite](../../relational-databases/native-client-ole-db-transactions/supporting-distributed-transactions.md)  
  
-   [Livelli &#40;di isolamento OLE DB&#41;](../../relational-databases/native-client-ole-db-transactions/isolation-levels-ole-db.md)  
  
## <a name="see-also"></a>Vedere anche  
 [SQL Server Native Client &#40;OLE DB&#41;](../../relational-databases/native-client/ole-db/sql-server-native-client-ole-db.md)  
  
  
