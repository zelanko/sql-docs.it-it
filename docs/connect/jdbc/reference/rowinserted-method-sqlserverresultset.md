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
manager: jroth
ms.openlocfilehash: da746533231983d67bbfe3689d0df63086d678bc
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/07/2019
ms.locfileid: "66765380"
---
# <a name="rowinserted-method-sqlserverresultset"></a>Metodo rowInserted (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera informazioni sull'eventuale presenza di un inserimento nella riga corrente.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public boolean rowInserted()  
```  
  
## <a name="return-value"></a>Valore restituito  
 **true** se una riga è stata eseguita un inserimento e gli inserimenti vengono rilevati. In caso contrario, **false**.  
  
## <a name="exceptions"></a>Eccezioni  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Questo metodo rowUpdated viene specificato dal metodo rowUpdated nell'interfaccia ResultSet.  
  
 Il valore restituito dipende dalla possibilità dell'oggetto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) di rilevare gli inserimenti visibili.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] non rilevare le righe inserite per qualsiasi tipo di cursore.  
  
## <a name="see-also"></a>Vedere anche  
 [Membri di SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Classe SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
