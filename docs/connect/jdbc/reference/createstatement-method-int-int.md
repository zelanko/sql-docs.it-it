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
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/29/2020
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
 Oggetto Statement.  
  
## <a name="exceptions"></a>Eccezioni  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Osservazioni  
 Questo metodo createStatement viene specificato dal metodo createStatement nell'interfaccia java.sql.Connection.  
  
## <a name="see-also"></a>Vedere anche  
 [Metodo createStatement &#40;SQLServerConnection&#41;](../../../connect/jdbc/reference/createstatement-method-sqlserverconnection.md)   
 [Membri di SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [Classe SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
