---
title: Livelli di isolamento (OLE DB) | Microsoft Docs
description: Livelli di isolamento (OLE DB)
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- OLE DB, transactions
- isolation levels [OLE DB]
- transactions [OLE DB]
- OLE DB Driver for SQL Server, transactions
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 2c9f3a7cd06f801555ab373e7e54fbf1b620d894
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/31/2020
ms.locfileid: "67993968"
---
# <a name="isolation-levels-ole-db"></a>Livelli di isolamento (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  I client [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] possono controllare i livelli di isolamento delle transazioni per una connessione. Per controllare il livello di isolamento delle transazioni, il consumer di OLE DB Driver per SQL Server usa:  
  
-   DBPROP_SESS_AUTOCOMMITISOLEVELS della proprietà DBPROPSET_SESSION per la modalità di autocommit predefinita del driver OLE DB per SQL Server.  
  
     L'impostazione predefinita di OLE DB Driver per SQL Server per il livello è DBPROPVAL_TI_READCOMMITTED.  
  
-   Parametro *isoLevel* del metodo **ITransactionLocal::StartTransaction** per le transazioni locali di cui viene eseguito il commit manuale.  
  
-   Parametro *isoLevel* del metodo **ITransactionDispenser::BeginTransaction** per le transazioni distribuite coordinate da MS DTC.  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] consente accesso di sola lettura nel livello di isolamento di lettura dirty. Tutti gli altri livelli limitano la concorrenza applicando blocchi agli oggetti di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Poiché il client richiede livelli di concorrenza maggiori, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] applica restrizioni superiori all'accesso simultaneo ai dati. Per gestire il livello più elevato di accesso simultaneo ai dati, il consumer del driver OLE DB per SQL Server deve controllare in modo intelligente le richieste per livelli di concorrenza specifici.  
  
> [!NOTE]  
>  In [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] è stato introdotto il livello di isolamento dello snapshot. Per altre informazioni, vedere [Uso dell'isolamento dello snapshot](../../oledb/features/working-with-snapshot-isolation.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Transazioni](../../oledb/ole-db-transactions/transactions.md)  
  
  
