---
title: Metodo getUpdateCount (SQLServerStatement) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerStatement.getUpdateCount
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: e9570228-4500-44b6-b2f1-84ac050b5112
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 6f05796220e305a0d6e06e15a58f780048d49a53
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/07/2019
ms.locfileid: "66790524"
---
# <a name="getupdatecount-method-sqlserverstatement"></a>Metodo getUpdateCount (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera il risultato corrente come conteggio aggiornamenti.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public final int getUpdateCount()  
```  
  
## <a name="return-value"></a>Valore restituito  
 Valore **int** contenente il conteggio aggiornamenti. Se il risultato restituito è un oggetto del set di risultati o se non è più disponibile alcun risultato, viene restituito -1.  
  
## <a name="exceptions"></a>Eccezioni  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Questo metodo getUpdateCount viene specificato dal metodo getUpdateCount nell'interfaccia Statement.  
  
## <a name="see-also"></a>Vedere anche  
 [Membri di SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [Classe SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
