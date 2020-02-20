---
title: Aggiunta di una colonna a una tabella di SQL Server | Microsoft Docs
description: Aggiunta di una colonna a una tabella di SQL Server tramite OLE DB Driver per SQL Server
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- columns [OLE DB]
- AddColumn function
- OLE DB Driver for SQL Server, columns
- adding columns
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 2c6cd539e499f80342a30371d047c9870c4fda08
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/31/2020
ms.locfileid: "67994097"
---
# <a name="adding-a-column-to-a-sql-server-table"></a>Aggiunta di una colonna a una tabella di SQL Server
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  OLE DB Driver per SQL Server espone la funzione **ITableDefinition::AddColumn**. Questo consente ai consumer di aggiungere una colonna a una tabella di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 Quando si aggiunge una colonna a una tabella di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], il consumer di OLE DB Driver per SQL Server presenta i vincoli seguenti:  
  
-   Se DBPROP_COL_AUTOINCREMENT è VARIANT_TRUE, DBPROP_COL_NULLABLE deve essere VARIANT_FALSE.  
  
-   Se la colonna viene definita usando il tipo di dati **timestamp** di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], DBPROP_COL_NULLABLE deve essere VARIANT_FALSE.  
  
-   Per qualsiasi altra definizione di colonna, DBPROP_COL_NULLABLE deve essere VARIANT_TRUE.  
  
 I consumer specificano il nome della tabella come stringa di caratteri Unicode nel membro *pwszName* dell'unione *uName* nel parametro *pTableID*. Il membro *eKind* di*pTableID* deve essere DBKIND_NAME.  
  
 Il nome della nuova colonna viene specificato come stringa di caratteri Unicode nel membro *pwszName* dell'unione *uName* nel membro *dbcid* del parametro DBCOLUMNDESC *pColumnDesc*. Il membro *eKind* deve essere DBKIND_NAME.  
  
## <a name="see-also"></a>Vedere anche  
 [Tabelle e indici](../../oledb/ole-db-tables-indexes/tables-and-indexes.md)   
 [ALTER TABLE &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-table-transact-sql.md)  
  
  
