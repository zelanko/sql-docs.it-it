---
title: Livelli di isolamento (OLE DB) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- OLE DB, transactions
- isolation levels [OLE DB]
- transactions [OLE DB]
- SQL Server Native Client OLE DB provider, transactions
ms.assetid: d70ee72c-6e2a-4bcd-9456-4a697a866361
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: c3535360e120e0f9c61a8cfb7cb578e531e92572
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81280288"
---
# <a name="isolation-levels-ole-db"></a>Livelli di isolamento (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  I client [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] possono controllare i livelli di isolamento delle transazioni per una connessione. Per controllare il livello [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] di isolamento delle transazioni, il consumer del provider OLE DB Native Client utilizza:To control transaction-isolation level, the Native Client OLE DB provider consumer uses:  
  
-   DBPROPSET_SESSION DBPROP_SESS_AUTOCOMMITISOLEVELS di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proprietà per la modalità di commit automatico predefinito del provider OLE DB del client nativo.  
  
     Il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provider OLE DB Native Client predefinito per il livello è DBPROPVAL_TI_READCOMMITTED.  
  
-   Parametro *isoLevel* del metodo **ITransactionLocal::StartTransaction** per le transazioni locali di cui viene eseguito il commit manuale.  
  
-   Parametro *isoLevel* del metodo **ITransactionDispenser::BeginTransaction** per le transazioni distribuite coordinate da MS DTC.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] consente accesso di sola lettura nel livello di isolamento di lettura dirty. Tutti gli altri livelli limitano la concorrenza applicando blocchi agli oggetti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Poiché il client richiede livelli di concorrenza maggiori, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] applica restrizioni superiori all'accesso simultaneo ai dati. Per mantenere il massimo livello di accesso [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] simultaneo ai dati, il consumer del provider OLE DB Native Client deve controllare in modo intelligente le richieste per livelli di concorrenza specifici.  
  
> [!NOTE]  
>  In [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] è stato introdotto il livello di isolamento dello snapshot. Per altre informazioni, vedere [Uso dell'isolamento dello snapshot](../../relational-databases/native-client/features/working-with-snapshot-isolation.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Transazioni](../../relational-databases/native-client-ole-db-transactions/transactions.md)  
  
  
