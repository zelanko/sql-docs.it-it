---
title: Individuazione dei metadati | Microsoft Docs
description: Individuazione dei metadati in OLE DB Driver per SQL Server
ms.custom: ''
ms.date: 06/12/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 9891e5708110be83a4ef33cb2a142accaf93ffe2
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/31/2020
ms.locfileid: "67989057"
---
# <a name="metadata-discovery"></a>Individuazione dei metadati
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  I miglioramenti apportati all'individuazione dei metadati in [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] consentono alle applicazioni del driver OLE DB per SQL Server di garantire che i metadati delle colonne o dei parametri restituiti dall'esecuzione di una query siano identici a o compatibili con il formato dei metadati specificato prima di eseguire la query. Se i metadati restituiti dopo l'esecuzione di una query non sono compatibili con il formato dei metadati specificato prima dell'esecuzione della query, viene generato un errore.  
  
 In bcp nonché nelle interfacce IBCPSession e IBCPSession2, è ora possibile specificare una lettura ritardata (individuazione dei metadati ritardata) per evitare l'individuazione dei metadati per le operazioni di esportazione di query. In questo modo, è possibile migliorare le prestazioni ed eliminare gli errori di individuazione dei metadati.  
  
 Se si sviluppa un'applicazione utilizzando il driver OLE DB per SQL Server ma si esegue la connessione a una versione del server precedente a [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)], la funzionalità di individuazione dei metadati corrisponderà alla versione del server.  
  
## <a name="remarks"></a>Osservazioni   
 Le funzioni membro OLE DB seguenti sono state migliorate in [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] per garantire una migliore individuazione dei metadati:  
  
-   IColumnsInfo::GetColumnInfo  
  
-   IColumnsRowset::GetColumnsRowset  
  
-   ICommandWithParameters:: GetParameterInfo (per altre informazioni, vedere [ICommandWithParameters](../../oledb/ole-db-interfaces/icommandwithparameters.md))  
  
 È inoltre possibile notare un miglioramento nelle prestazioni quando si specifica il formato dei metadati utilizzando IBCPSession::BCPSetBulkMode  
  
 Il miglioramento dell'individuazione dei metadati in OLE DB Driver per SQL Server è stato reso possibile dall'aggiunta di due stored procedure in [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]:  
  
-   sp_describe_first_result_set  
  
-   sp_describe_undeclared_parameters  
  
## <a name="see-also"></a>Vedere anche  
 [Driver OLE DB per funzionalità di SQL Server](../../oledb/features/oledb-driver-for-sql-server-features.md)  
  
  
