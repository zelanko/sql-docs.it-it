---
title: Metodo getStatementPoolingCacheSize (SQLServerConnection) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerConnection.getStatementPoolingCacheSize
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ''
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ea65ca1cbf69db3628c7664fb3b481b6ffaa91ee
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67979526"
---
# <a name="getstatementpoolingcachesize-method-sqlserverconnection"></a>Metodo getStatementPoolingCacheSize (SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

 Restituisce le dimensioni della cache delle istruzioni preparate per questa connessione. ' 0' indica che la memorizzazione nella cache non è abilitata.

## <a name="syntax"></a>Sintassi  
  
```  
  
public int getStatementPoolingCacheSize()  
```  

## <a name="return-value"></a>Valore restituito
 **Int** che contiene il valore della proprietà di connessione **disablestatementpooling** .

## <a name="exceptions"></a>Eccezioni  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
 
## <a name="remarks"></a>Remarks  
 Questo metodo è disponibile dal driver JDBC versione 6,4 e successive.
 
## <a name="see-also"></a>Vedere anche  
 [Membri di SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [Classe SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
