---
title: Metodo getServerPreparedStatementDiscardThreshold (SQLServerConnection) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerConnection.getServerPreparedStatementDiscardThreshold
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ''
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 22f7bf637d20b42a7dadd3397e84c826fa277a22
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/07/2019
ms.locfileid: "66791915"
---
# <a name="getserverpreparedstatementdiscardthreshold-method-sqlserverconnection"></a>Metodo getServerPreparedStatementDiscardThreshold (SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

 Restituisce il valore del **serverPreparedStatementDiscardThreshold** proprietà di connessione. Questa impostazione Controlla quanti preparato in sospeso variabile discard istruzione azioni (sp_unprepare) possono rimanere in attesa per ogni connessione prima che venga eseguita una chiamata per pulire l'handle in sospeso nel server. Se l'impostazione è < = 1, unprepare azioni vengono eseguite immediatamente in chiusura istruzione preparata. Se è impostato su 1 >, queste chiamate vengono eseguite in batch insieme per evitare il sovraccarico della chiamata al metodo sp_unprepare troppo spesso. Il valore predefinito per questa opzione può essere modificato da getDefaultServerPreparedStatementDiscardThreshold() chiamante.

## <a name="syntax"></a>Sintassi  
  
```  
  
public int getServerPreparedStatementDiscardThreshold()  
```  

## <a name="return-value"></a>Valore restituito
 Un' **int** che contiene il valore di **serverPreparedStatementDiscardThreshold** proprietà di connessione.

## <a name="exceptions"></a>Eccezioni  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
 
## <a name="remarks"></a>Remarks  
 Questo metodo è disponibile dal driver JDBC versione 6.4 e progressiva.
 
## <a name="see-also"></a>Vedere anche  
 [Membri di SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [Classe SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
