---
title: Metodo getDisableStatementPooling (SQLServerConnection) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerConnection.getDisableStatementPooling
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ''
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 9f475d3d02f671cc9c6d277cc50589c4e6980070
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/07/2019
ms.locfileid: "66776934"
---
# <a name="getdisablestatementpooling-method-sqlserverconnection"></a>Metodo getDisableStatementPooling (SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

 Restituisce il valore del **disableStatementPooling** proprietà di connessione. Questa impostazione controlla se l'istruzione di limitazione delle richieste è abilitata o meno per questa connessione.

## <a name="syntax"></a>Sintassi  
  
```  
  
public boolean getDisableStatementPooling()  
```  

## <a name="return-value"></a>Valore restituito
 Oggetto **booleana** che contiene il valore di **disableStatementPooling** proprietà di connessione.

## <a name="exceptions"></a>Eccezioni  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
 
## <a name="remarks"></a>Remarks  
 Questo metodo è disponibile dal driver JDBC versione 6.4 e progressiva.
 
## <a name="see-also"></a>Vedere anche  
 [Membri di SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [Classe SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
