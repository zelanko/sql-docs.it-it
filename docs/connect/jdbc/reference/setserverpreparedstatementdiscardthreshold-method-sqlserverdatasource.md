---
title: Metodo setServerPreparedStatementDiscardThreshold (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ''
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: fb2962f6514fec7211b6d3a5ccd5f3af09a1f066
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/07/2019
ms.locfileid: "66782921"
---
# <a name="setserverpreparedstatementdiscardthreshold-method-sqlserverdatasource"></a>Metodo setServerPreparedStatementDiscardThreshold (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Imposta il valore della proprietà di connessione serverPreparedStatementDiscardThreshold. Questa impostazione Controlla quanti preparato in sospeso variabile discard istruzione azioni (sp_unprepare) possono rimanere in attesa per ogni connessione prima che venga eseguita una chiamata per pulire l'handle in sospeso nel server. Quando l'impostazione è < = 1 unprepare azioni vengono eseguite immediatamente in chiusura istruzione preparata. Se il valore è impostato su 1 > queste chiamate vengono eseguite in batch insieme per evitare il sovraccarico della chiamata al metodo sp_unprepare troppo spesso
 
## <a name="syntax"></a>Sintassi  
  
```
public void setServerPreparedStatementDiscardThreshold(int enablePrepareOnFirstPreparedStatementCall);  
```  
  
#### <a name="parameters"></a>Parametri  
 *serverPreparedStatementDiscardThreshold*  
  
 Il nuovo valore della **serverPreparedStatementDiscardThreshold** proprietà di connessione.  

## <a name="exceptions"></a>Eccezioni  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
 
## <a name="remarks"></a>Remarks  
 Questo metodo è disponibile dal driver JDBC versione 6.4 e progressiva.
 
## <a name="see-also"></a>Vedere anche  
 [Membri di SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Classe SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
