---
title: Metodo getFetchDirection (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.getFetchDirection
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 5ab385c2-e18c-4b75-ac2d-2402af5c52a5
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f56893764392236d563fa2b9a236f55e67e13595
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/31/2020
ms.locfileid: "67983250"
---
# <a name="getfetchdirection-method-sqlserverresultset"></a>Metodo getFetchDirection (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera la direzione di recupero di questo oggetto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md).  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public int getFetchDirection()  
```  
  
## <a name="return-value"></a>Valore restituito  
 Valore **int** che indica la direzione di recupero corrente.  
  
## <a name="exceptions"></a>Eccezioni  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Osservazioni  
 Questo metodo getFetchDirection viene specificato dal metodo getFetchDirection nell'interfaccia java.sql.ResultSet.  
  
 Questo metodo restituisce FETCH_FORWARD per i cursori forward-only, l'ultima impostazione eseguita da una chiamata al metodo [setFetchDirection](../../../connect/jdbc/reference/setfetchdirection-method-sqlserverresultset.md) per altri tipi di cursore, mentre restituisce FETCH_UNKNOWN per questi tipi di cursore se il metodo setFetchDirection non è mai stato chiamato.  
  
## <a name="see-also"></a>Vedere anche  
 [Membri di SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Classe SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
