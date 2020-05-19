---
title: Rimozione di una colonna da una tabella di SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- columns [OLE DB]
- removing columns
- DropColumn function
- SQL Server Native Client OLE DB provider, columns
ms.assetid: 210811b7-cbd6-421e-bc6e-df9482236768
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 8cde1faf93713a72f9fa69f056250b4e5357c538
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/01/2020
ms.locfileid: "82704534"
---
# <a name="removing-a-column-from-a-sql-server-table"></a>Rimozione di una colonna da una tabella di SQL Server
  Il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provider di OLE DB di Native Client espone la funzione **ITableDefinition::D ropcolumn** . Questo consente ai consumer di rimuovere una colonna da una tabella di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
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
 [Tabelle e indici](tables-and-indexes.md)  
  
  
