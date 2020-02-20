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
ms.openlocfilehash: 87d7f85799524e3ac7c0e4d99608ce1d82b8f2fc
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/31/2020
ms.locfileid: "67979936"
---
# <a name="getserverpreparedstatementdiscardthreshold-method-sqlserverconnection"></a>Metodo getServerPreparedStatementDiscardThreshold (SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

 Restituisce il valore della proprietà di connessione **serverPreparedStatementDiscardThreshold**. Questa impostazione consente di controllare il numero di azioni di annullamento di istruzioni preparate (sp_unprepare) in sospeso per ogni connessione prima che venga eseguita una chiamata per pulire gli handle in sospeso nel server. Se l'impostazione è <= 1, le azioni di annullamento della preparazione vengono eseguite immediatamente alla chiusura dell'istruzione preparata. Se questo valore è impostato su > 1, queste chiamate vengono eseguite in batch per evitare il sovraccarico di chiamate troppo frequenti di sp_unprepare. L'impostazione predefinita per questa opzione può essere modificata chiamando getDefaultServerPreparedStatementDiscardThreshold().

## <a name="syntax"></a>Sintassi  
  
```  
  
public int getServerPreparedStatementDiscardThreshold()  
```  

## <a name="return-value"></a>Valore restituito
 Valore **int** che contiene il valore della proprietà di connessione **serverPreparedStatementDiscardThreshold**.

## <a name="exceptions"></a>Eccezioni  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
 
## <a name="remarks"></a>Osservazioni  
 Questo metodo è disponibile dal driver JDBC versione 6.4 e successive.
 
## <a name="see-also"></a>Vedere anche  
 [Membri di SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [Classe SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
