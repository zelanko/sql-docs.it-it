---
title: Costruttore SQLServerException (lang, lang, int, Throwable) | Microsoft Docs
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
ms.openlocfilehash: fbd40c6edb2e4b623f0e2fbf7e00ad91dc683a04
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66766867"
---
# <a name="sqlserverexception-constructor-javalangstring-javalangstring-int-javalangthrowable"></a>Costruttore SQLServerException (lang, lang, int, Throwable)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Inizializza una nuova istanza della [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md) classe quando viene specificato un **stringa** oggetto, una **stringa** oggetto, un **int**e un **throwable** oggetto.

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
  
 Stringa che contiene lo stato dell'errore.
 
 *errNum*  
  
 Valore int che contiene il codice di errore per l'eccezione.
 
 *cause*  
  
 Un oggetto throwable che contiene la causa dell'eccezione.
  
## <a name="see-also"></a>Vedere anche  
 [Costruttori di SQLServerException](../../../connect/jdbc/reference/sqlserverexception-constructors.md)   
 [Membri di SQLServerException](../../../connect/jdbc/reference/sqlserverexception-members.md)   
 [Classe SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
  
