---
title: Costruttore SQLServerException (lang, SQLState, DriverError, Throwable) | Microsoft Docs
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
manager: jroth
ms.openlocfilehash: 726cbd2c1a2106168532b34bd64db269a2031ac4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66800912"
---
# <a name="sqlserverexception-constructor-javalangstring-sqlstate-drivererror-javalangthrowable"></a>Costruttore SQLServerException (lang. Throwable SQLState, DriverError)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Inizializza una nuova istanza della [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md) classe quando viene specificato un **stringa** oggetto, una **sqlstate** oggetto, un **drivererror** oggetto e un **throwable** oggetto.

## <a name="syntax"></a>Sintassi  
  
```  
public SQLServerException(java.lang.String errText,
            SQLState sqlState,
            DriverError driverError,
            java.lang.Throwable cause)
            
```  
  
#### <a name="parameters"></a>Parametri  
 *errText*  
  
 Stringa che contiene il testo dell'errore.
  
 *sqlState*  
  
 Un oggetto di enumerazione che contiene lo stato SQL.
 
 *driverError*  
  
 Un oggetto di enumerazione che contiene l'errore di driver.
 
 *cause*  
  
 Un oggetto throwable che contiene la causa dell'eccezione.
  
## <a name="see-also"></a>Vedere anche  
 [Costruttori di SQLServerException](../../../connect/jdbc/reference/sqlserverexception-constructors.md)   
 [Membri di SQLServerException](../../../connect/jdbc/reference/sqlserverexception-members.md)   
 [Classe SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
  
