---
title: Rimozione di una colonna da una tabella di SQL Server | Microsoft Docs
description: Rimozione di una colonna da una tabella di SQL Server tramite OLE DB Driver per SQL Server
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- columns [OLE DB]
- removing columns
- DropColumn function
- OLE DB Driver for SQL Server, columns
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 7e367c1b0664b0b43007db3a465dcbec0ffa90d9
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/29/2020
ms.locfileid: "67993994"
---
# <a name="removing-a-column-from-a-sql-server-table"></a>Rimozione di una colonna da una tabella di SQL Server
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  OLE DB Driver per SQL Server espone la funzione **ITableDefinition::DropColumn**. Questo consente ai consumer di rimuovere una colonna da una tabella di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 I consumer specificano il nome della tabella come stringa di caratteri Unicode nel membro *pwszName* dell'unione *uName* nel parametro *pTableID*. Il membro *eKind* di *pTableID* deve essere DBKIND_NAME.  
  
 Il consumer indica un nome di colonna nel membro *pwszName* dell'unione *uName* nel parametro *pColumnID*. Il nome di colonna è una stringa di caratteri Unicode. Il membro *eKind* di *pColumnID* deve essere DBKIND_NAME.  
  
## <a name="example"></a>Esempio  
  
### <a name="code"></a>Codice  
  
```  
DBID TableID;  
DBID ColumnID;  
HRESULT hr;  
  
TableID.eKind = DBKIND_NAME;  
TableID.uName.pwszName = L"MyTableName";  
  
ColumnID.eKind = DBKIND_NAME;  
ColumnID.uName.pwszName = L"MyColumnName";  
  
hr = m_pITableDefinition->DropColumn(&TableID, &ColumnID);  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Tabelle e indici](../../oledb/ole-db-tables-indexes/tables-and-indexes.md)  
  
  
