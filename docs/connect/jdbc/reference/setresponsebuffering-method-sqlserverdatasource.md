---
title: Metodo setResponseBuffering (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSource.setResponseBuffering(String responseBufferingValue)
apilocation:
- SQLServerDataSource.setResponseBuffering(String responseBufferingValue)
apitype: Assembly
ms.assetid: c9e43ff2-8117-4dca-982d-83c863d0c8e1
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: fa4e1c6921495448ce0a1e01a972b1786a69efd9
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/07/2019
ms.locfileid: "66796759"
---
# <a name="setresponsebuffering-method-sqlserverdatasource"></a>Metodo setResponseBuffering (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Imposta la modalità di memorizzazione delle risposte nel buffer per le connessioni create tramite questo oggetto [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md).  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public void setResponseBuffering(java.lang.String value)  
```  
  
#### <a name="parameters"></a>Parametri  
 *Valore*  
  
 Valore **String** contenente la modalità di flusso e di memorizzazione nel buffer. La modalità valida può essere una delle stringhe senza distinzione tra maiuscole e minuscole seguenti: **full** o **adaptive**.  
  
## <a name="remarks"></a>Remarks  
 Il valore **full** specifica la lettura dell'intero risultato dal server in fase di esecuzione.  
  
 Il valore **adaptive** specifica la memorizzazione nel buffer della quantità di dati minima possibile, quando necessario. Il valore **adaptive** rappresenta la modalità di memorizzazione nel buffer predefinita.  
  
 Per altre informazioni sull'uso la modalità di memorizzazione delle risposte, vedere [Using Adaptive Buffering](../../../connect/jdbc/using-adaptive-buffering.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Membri di SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Classe SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
