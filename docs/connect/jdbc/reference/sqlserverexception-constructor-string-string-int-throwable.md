---
title: Costruttore SQLServerException (java.lang.String, java.lang.String, int, java.lang.Throwable) | Microsoft Docs
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
ms.openlocfilehash: 18827d05bc5567b4566eaa006d88c249874132cf
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67971083"
---
# <a name="sqlserverexception-constructor-javalangstring-javalangstring-int-javalangthrowable"></a>Costruttore SQLServerException (java.lang.String, java.lang.String, int, java.lang.Throwable)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Inizializza una nuova istanza della classe [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md) quando vengono specificati un oggetto **stringa** , un oggetto **stringa** , un **int**e un oggetto **generabile** .

## <a name="syntax"></a>Sintassi  
  
```  
public SQLServerException(java.lang.String errText,
            SQLState errState,
            int errNum,
            java.lang.Throwable cause)
            
```  
  
#### <a name="parameters"></a>Parametri  
 *errText*  
  
 Stringa contenente il testo dell'errore.
  
 *errState*  
  
 Stringa contenente lo stato dell'errore.
 
 *errNum*  
  
 Int che contiene il codice di errore per l'eccezione.
 
 *cause*  
  
 Oggetto generabile che contiene la ragione dell'eccezione.
  
## <a name="see-also"></a>Vedere anche  
 [Costruttori di SQLServerException](../../../connect/jdbc/reference/sqlserverexception-constructors.md)   
 [Membri di SQLServerException](../../../connect/jdbc/reference/sqlserverexception-members.md)   
 [Classe SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
  
