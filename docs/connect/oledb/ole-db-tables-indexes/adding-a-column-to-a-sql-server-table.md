---
title: Aggiungere una colonna a una tabella di SQL Server (OLE DB Driver) | Microsoft Docs
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
ms.openlocfilehash: ce22cc49060451e7d47a1f9452f1c10a134ae610
ms.sourcegitcommit: 591bbf4c7e4e2092f8abda6a2ffed263cb61c585
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/22/2020
ms.locfileid: "86943143"
---
# <a name="adding-a-column-to-a-sql-server-table"></a>Aggiunta di una colonna a una tabella di SQL Server
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  OLE DB Driver per SQL Server espone la funzione **ITableDefinition::AddColumn**. Questo consente ai consumer di aggiungere una colonna a una tabella di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 Quando si aggiunge una colonna a una tabella di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], il consumer di OLE DB Driver per SQL Server presenta i vincoli seguenti:  
  
-   Se DBPROP_COL_AUTOINCREMENT è VARIANT_TRUE, DBPROP_COL_NULLABLE deve essere VARIANT_FALSE.  
  
-   Se la colonna viene definita usando il tipo di dati [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]timestamp**di**, DBPROP_COL_NULLABLE deve essere VARIANT_FALSE.  
  
-   Per qualsiasi altra definizione di colonna, DBPROP_COL_NULLABLE deve essere VARIANT_TRUE.  
  
 I consumer specificano il nome della tabella come stringa di caratteri Unicode nel membro *pwszName* dell'unione *uName* nel parametro *pTableID*. Il membro *eKind* di*pTableID* deve essere DBKIND_NAME.  
  
 Il nome della nuova colonna viene specificato come stringa di caratteri Unicode nel membro *pwszName* dell'unione *uName* nel membro *dbcid* del parametro DBCOLUMNDESC *pColumnDesc*. Il membro *eKind* deve essere DBKIND_NAME.  
  
## <a name="see-also"></a>Vedere anche  
 [Tabelle e indici](../../oledb/ole-db-tables-indexes/tables-and-indexes.md)   
 [ALTER TABLE &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-table-transact-sql.md)  
  
  
