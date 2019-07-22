---
title: Metodo createStatement (int, int) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerConnection.createStatement (int, int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 90dbf639-c3d8-4519-9300-5447c79aec17
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 84afda93fa79d226eec21cb92c16ff5ebbc55fa5
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67955319"
---
# <a name="createstatement-method-int-int"></a>Metodo createStatement (int, int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Crea un oggetto [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) che genera oggetti [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) con il tipo e la concorrenza specificati.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public java.sql.Statement createStatement(int resultSetType,  
                                          int resultSetConcurrency)  
```  
  
#### <a name="parameters"></a>Parametri  
 *resultSetType*  
  
 Valore **int** che rappresenta il tipo di set di risultati.  
  
 *resultSetConcurrency*  
  
 Valore **int** che rappresenta il tipo di concorrenza del set di risultati.  
  
## <a name="return-value"></a>Valore restituito  
 Oggetto istruzione.  
  
## <a name="exceptions"></a>Eccezioni  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Questo metodo createStatement viene specificato dal metodo createStatement nell'interfaccia java. SQL. Connection.  
  
## <a name="see-also"></a>Vedere anche  
 [Metodo createStatement &#40;SQLServerConnection&#41;](../../../connect/jdbc/reference/createstatement-method-sqlserverconnection.md)   
 [Membri di SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [Classe SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
