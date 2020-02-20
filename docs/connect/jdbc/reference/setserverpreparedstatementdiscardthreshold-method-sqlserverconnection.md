---
title: Metodo setServerPreparedStatementDiscardThreshold (SQLServerConnection) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerConnection.setServerPreparedStatementDiscardThreshold
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ''
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 8f66746b15e96f49d96b428e8cf8844eeea12a12
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/31/2020
ms.locfileid: "67972924"
---
# <a name="setserverpreparedstatementdiscardthreshold-method-sqlserverconnection"></a>Metodo setServerPreparedStatementDiscardThreshold (SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

 Specifica il comportamento per un'istanza di connessione specifica. Questa impostazione consente di controllare il numero di azioni di annullamento di istruzioni preparate (sp_unprepare) in sospeso per ogni connessione prima che venga eseguita una chiamata per pulire gli handle in sospeso nel server. Quando l'impostazione è <= 1, le azioni di annullamento della preparazione vengono eseguite immediatamente alla chiusura dell'istruzione preparata. Se il valore è impostato su > 1, queste chiamate vengono eseguite in batch per evitare il sovraccarico di chiamate troppo frequenti di sp_unprepare.


## <a name="syntax"></a>Sintassi  
  
```  
  
public void setServerPreparedStatementDiscardThreshold(boolean thresholdValue)  
```  

#### <a name="parameters"></a>Parametri  
 *thresholdValue*  
 
 Nuovo valore della proprietà di connessione **serverPreparedStatementDiscardThreshold**.  
 
## <a name="exceptions"></a>Eccezioni  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
 
## <a name="remarks"></a>Osservazioni  
 Questo metodo è disponibile dal driver JDBC versione 6.4 e successive.
 
## <a name="see-also"></a>Vedere anche  
 [Membri di SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [Classe SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
