---
description: Metodo rowUpdated (SQLServerResultSet)
title: Metodo rowUpdated (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.rowUpdated
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 29303550-294e-4d43-b892-312b42e21271
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 35c3058b8e590dc46af09414599903702fbf315c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88432683"
---
# <a name="rowupdated-method-sqlserverresultset"></a>Metodo rowUpdated (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera informazioni sull'eventuale aggiornamento della riga corrente.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public boolean rowUpdated()  
```  
  
## <a name="return-value"></a>Valore restituito  
 **true** se la riga è stata aggiornata in maniera visibile dal proprietario o da un altro utente e vengono rilevati aggiornamenti. In caso contrario, **false**.  
  
## <a name="exceptions"></a>Eccezioni  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Osservazioni  
 Questo metodo rowUpdated viene specificato dal metodo rowUpdated nell'interfaccia java.sql.ResultSet.  
  
 Il valore restituito dipende dall'eventuale rilevamento degli aggiornamenti da parte del set di risultati.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] non rileva le righe aggiornate per qualsiasi tipo di cursore.  
  
## <a name="see-also"></a>Vedere anche  
 [Membri di SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Classe SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
