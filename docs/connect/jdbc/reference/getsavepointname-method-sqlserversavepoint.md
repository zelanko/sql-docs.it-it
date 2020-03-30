---
title: Metodo getSavepointName (SQLServerSavepoint) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerSavepoint.getSavepointName
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 6affbe5c-e836-4195-a3ba-1892cbf81907
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 8fe7df1dcba7762cded47fb5483e017ed6851054
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/29/2020
ms.locfileid: "67980210"
---
# <a name="getsavepointname-method-sqlserversavepoint"></a>Metodo getSavepointName (SQLServerSavepoint)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Ottiene il nome del punto di salvataggio.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public java.lang.String getSavepointName()  
```  
  
## <a name="return-value"></a>Valore restituito  
 Valore **String** contenente il nome del punto di salvataggio.  
  
## <a name="exceptions"></a>Eccezioni  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Osservazioni  
 Questo metodo getSavepointName viene specificato dal metodo getSavepointName nell'interfaccia java.sql.Savepoint.  
  
## <a name="see-also"></a>Vedere anche  
 [Metodi di SQLServerSavepoint](../../../connect/jdbc/reference/sqlserversavepoint-methods.md)   
 [Membri di SQLServerSavepoint](../../../connect/jdbc/reference/sqlserversavepoint-members.md)   
 [Classe SQLServerSavepoint](../../../connect/jdbc/reference/sqlserversavepoint-class.md)  
  
  
