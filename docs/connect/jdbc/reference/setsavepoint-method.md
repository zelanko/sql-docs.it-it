---
title: Metodo setSavepoint () | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerConnection.setSavepoint ()
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 11013055-4fd3-45a9-b2da-28b2908dad52
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 6f6f26909a0ad7c5f33bdf997c48f88c6e7b300a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67973009"
---
# <a name="setsavepoint-method-"></a>Metodo setSavepoint ()
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Crea un punto di salvataggio senza nome nella transazione corrente e restituisce il nuovo oggetto [SQLServerSavepoint](../../../connect/jdbc/reference/sqlserversavepoint-class.md) che lo rappresenta.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public java.sql.Savepoint setSavepoint()  
```  
  
## <a name="return-value"></a>Valore restituito  
 Oggetto salvataggio.  
  
## <a name="exceptions"></a>Eccezioni  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Questo metodo setSavePoint viene specificato dal metodo setSavePoint nell'interfaccia java. SQL. Connection.  
  
## <a name="see-also"></a>Vedere anche  
 [Metodo setSavepoint &#40;SQLServerConnection&#41;](../../../connect/jdbc/reference/setsavepoint-method-sqlserverconnection.md)   
 [Membri di SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [Classe SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
