---
title: Costruttore SQLServerException (java.lang.Object, java.lang.String, java.lang.String, StreamError, boolean) | Microsoft Docs
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
ms.openlocfilehash: 33b5d593cfc5ac4b46fdfe7dcf7a845f754d5f3d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66800921"
---
# <a name="sqlserverexception-constructor-javalangobject-javalangstring-javalangstring-streamerror-boolean"></a>Costruttore SQLServerException (java.lang.Object, java.lang.String, java.lang.String, StreamError, boolean)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Inizializza una nuova istanza della [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md) classe quando viene specificato un **oggetto**, una **stringa** oggetto, un **stringa** (oggetto), un  **StreamError** oggetti e una **booleano**.

## <a name="syntax"></a>Sintassi  
  
```  

public SQLServerException(java.lang.Object obj,
            java.lang.String errText,
            java.lang.String errState,
            StreamError streamError,
            boolean bStack)

            
```  
  
#### <a name="parameters"></a>Parametri  
 *obj*  
  
 Il buffer dei / o che ha generato l'eccezione.

 *errText*  
  
 Stringa contenente il testo dell'errore.
  
 *sqlState*  
  
 Un oggetto di enumerazione che contiene lo stato SQL.
 
 *streamError*  
  
 Un oggetto StreamError contenente i dettagli dell'errore.
 
 *bStack*  
  
 Valore booleano che indica se l'analisi dello stack deve essere generato.
  
## <a name="see-also"></a>Vedere anche  
 [Costruttori di SQLServerException](../../../connect/jdbc/reference/sqlserverexception-constructors.md)   
 [Membri di SQLServerException](../../../connect/jdbc/reference/sqlserverexception-members.md)   
 [Classe SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
  
