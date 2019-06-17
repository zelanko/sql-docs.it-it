---
title: Creazione di un set di righe con IOpenRowset | Microsoft Docs
description: Creazione di un set di righe con IOpenRowset interfaccia del Driver OLE DB per SQL Server
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- IOpenRowset interface
- rowsets [OLE DB], creating
- OLE DB Driver for SQL Server, rowsets
- OLE DB rowsets, creating
author: pmasl
ms.author: pelopes
manager: jroth
ms.openlocfilehash: 78b08a3da3da89e0db0d801945416dcdb1ff9c03
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/07/2019
ms.locfileid: "66799204"
---
# <a name="creating-a-rowset-with-iopenrowset"></a>Creazione di un set di righe con IOpenRowset
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  Il Driver OLE DB per SQL Server supporta il **IOpenRowset:: OPENROWSET** metodo con le restrizioni seguenti:  
  
-   Una vista o una tabella di base deve essere specificata in una struttura del database (DBID) a cui punta il parametro *pTableID*.  
  
-   Il membro DBID *eKind* deve indicare DBKIND_NAME.  
  
-   Il membro DBID *uName* deve specificare il nome di una vista o di una tabella di base esistente come stringa di caratteri Unicode.  
  
-   Il parametro *pIndexID* di **OpenRowset** deve essere NULL.  
  
 Il set di risultati di **IOpenRowset::OpenRowset** contiene un solo set di righe. I set di risultati che contengono un solo set di righe possono essere supportati dai cursori di [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Il supporto del cursore consente allo sviluppatore di utilizzare i meccanismi di concorrenza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
## <a name="see-also"></a>Vedere anche  
 [Set di righe](../../oledb/ole-db-rowsets/rowsets.md)  
  
  
