---
description: Metodo getResponseBuffering (SQLServerStatement)
title: Metodo getResponseBuffering (SQLServerStatement) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerStatement.getResponseBuffering()
apilocation:
- SQLServerStatement.getResponseBuffering()
apitype: Assembly
ms.assetid: a9a9ffdd-7ce3-4e0a-907c-34d6a54e6865
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 08411235fe8e571e9f3bdaf7220f2387d3a0b5c0
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88434793"
---
# <a name="getresponsebuffering-method-sqlserverstatement"></a>Metodo getResponseBuffering (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera la modalità di memorizzazione delle risposte nel buffer per questo oggetto [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public final java.lang.String getResponseBuffering()  
```  
  
## <a name="return-value"></a>Valore restituito  
 Valore **String** che contiene un valore **full** o **adaptive** in lettere minuscole.  
  
## <a name="remarks"></a>Osservazioni  
 Il valore **adaptive** specifica la memorizzazione nel buffer della quantità di dati minima possibile, quando necessario.  
  
 Il valore **full** specifica la lettura dell'intero risultato dal server in fase di esecuzione.  
  
 **adaptive** è il valore predefinito nel driver JDBC versione 2.0 e 3.0. **full** era il valore predefinito prima della versione 2.0 del driver JDBC.  
  
 Per altre informazioni sull'uso della modalità di buffering delle risposte, vedere [Uso del buffer adattivo](../../../connect/jdbc/using-adaptive-buffering.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Metodo setResponseBuffering &#40;SQLServerStatement&#41;](../../../connect/jdbc/reference/setresponsebuffering-method-sqlserverstatement.md)   
 [Membri di SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [Classe SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
