---
title: Metodo setResponseBuffering (SQLServerStatement) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerStatement.setResponseBuffering(String responseBufferingValue)
apilocation:
- SQLServerStatement.setResponseBuffering(String responseBufferingValue)
apitype: Assembly
ms.assetid: 9f489835-6cda-4c8c-b139-079639a169cf
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 5b4490ac15558a0f6268a3d400d197367d028b9d
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/07/2019
ms.locfileid: "66796748"
---
# <a name="setresponsebuffering-method-sqlserverstatement"></a>Metodo setResponseBuffering (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Imposta la modalità di memorizzazione delle risposte nel buffer per questo oggetto [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) su un valore String **full** o **adaptive** senza distinzione tra maiuscole e minuscole.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public final void setResponseBuffering(java.lang.String value)  
```  
  
#### <a name="parameters"></a>Parametri  
 *Valore*  
  
 Valore **String** contenente la modalità di memorizzazione delle risposte nel buffer. La modalità valida può essere una delle stringhe senza distinzione tra maiuscole e minuscole seguenti: **full** o **adaptive**.  
  
## <a name="exceptions"></a>Eccezioni  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Il valore **adaptive** specifica la memorizzazione nel buffer della quantità di dati minima possibile, quando necessario.  
  
 Il valore **full** specifica la lettura dell'intero risultato dal server in fase di esecuzione.  
  
 Adaptive è il valore predefinito nel Driver JDBC versione 2.0 e 3.0. full è il valore predefinito prima della versione 2.0 del Driver JDBC.  
  
 Il metodo [setResponseBuffering](../../../connect/jdbc/reference/setresponsebuffering-method-sqlserverstatement.md) consente di eseguire l'override della proprietà **String** della connessione **responseBuffering** per l'oggetto [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) corrente. Per altre informazioni sull'uso la modalità di memorizzazione delle risposte, vedere [Using Adaptive Buffering](../../../connect/jdbc/using-adaptive-buffering.md).  
  
 Se l'applicazione specifica un valore del parametro non valido nel metodo [setResponseBuffering](../../../connect/jdbc/reference/setresponsebuffering-method-sqlserverstatement.md), viene generato un oggetto [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Membri di SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [Classe SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)   
 [Uso del buffer adattivo](../../../connect/jdbc/using-adaptive-buffering.md)  
  
  
