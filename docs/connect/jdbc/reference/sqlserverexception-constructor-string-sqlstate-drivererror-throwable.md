---
title: Costruttore SQLServerException (Java. lang. String, SQLState, DriverError, Java. lang. Throwable) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ''
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 13b0e3aea694b0cedb3594cb76650ca7c938eb55
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67971098"
---
# <a name="sqlserverexception-constructor-javalangstring-sqlstate-drivererror-javalangthrowable"></a>Costruttore SQLServerException (Java. lang. String, SQLState, DriverError, Java. lang. Throwable)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Inizializza una nuova istanza della classe [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md) quando vengono specificati un oggetto **stringa** , un oggetto **SQLSTATE** , un oggetto **drivererror** e un oggetto **generabile** .

## <a name="syntax"></a>Sintassi  
  
```  
public SQLServerException(java.lang.String errText,
            SQLState sqlState,
            DriverError driverError,
            java.lang.Throwable cause)
            
```  
  
#### <a name="parameters"></a>Parametri  
 *errText*  
  
 Stringa che include il testo dell'errore.
  
 *sqlState*  
  
 Oggetto enum che include lo stato SQL.
 
 *driverError*  
  
 Oggetto enum che include l'errore del driver.
 
 *cause*  
  
 Oggetto generabile che include la ragione dell'eccezione.
  
## <a name="see-also"></a>Vedere anche  
 [Costruttori di SQLServerException](../../../connect/jdbc/reference/sqlserverexception-constructors.md)   
 [Membri di SQLServerException](../../../connect/jdbc/reference/sqlserverexception-members.md)   
 [Classe SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
  
