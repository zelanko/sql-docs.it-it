---
title: Metodo rowInserted (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.rowInserted
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: e7c10372-0be8-4baa-87f7-ed6b66003357
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2b52007528ee5c3d3caaabc83b158e50156b664e
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/31/2020
ms.locfileid: "67975691"
---
# <a name="rowinserted-method-sqlserverresultset"></a>Metodo rowInserted (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera informazioni sull'eventuale presenza di un inserimento nella riga corrente.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public boolean rowInserted()  
```  
  
## <a name="return-value"></a>Valore restituito  
 **true** in presenza di un inserimento per una riga e se gli inserimenti vengono rilevati. In caso contrario, **false**.  
  
## <a name="exceptions"></a>Eccezioni  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Osservazioni  
 Questo metodo rowUpdated viene specificato dal metodo rowUpdated nell'interfaccia java.sql.ResultSet.  
  
 Il valore restituito dipende dalla possibilità dell'oggetto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) di rilevare gli inserimenti visibili.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] non rileva le righe inserite per qualsiasi tipo di cursore.  
  
## <a name="see-also"></a>Vedere anche  
 [Membri di SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Classe SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
