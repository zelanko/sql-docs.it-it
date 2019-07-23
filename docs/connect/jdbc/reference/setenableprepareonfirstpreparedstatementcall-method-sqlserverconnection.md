---
title: Metodo setEnablePrepareOnFirstPreparedStatementCall (SQLServerConnection) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerConnection.setEnablePrepareOnFirstPreparedStatementCall
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ''
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 187a195a831955b65f4af113fb80e5f99308e1a5
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67974452"
---
# <a name="setenableprepareonfirstpreparedstatementcall-method-sqlserverconnection"></a>Metodo setEnablePrepareOnFirstPreparedStatementCall (SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

 Specifica il comportamento per un'istanza di connessione specifica. Se value è false, la prima esecuzione chiamerà sp_executesql e non prepara un'istruzione, una volta eseguita la seconda esecuzione, chiamerà sp_prepexec e configurerà effettivamente un handle di istruzione preparato. Le esecuzioni seguenti chiameranno sp_execute. Questa operazione elimina la necessità di sp_unprepare in caso di chiusura dell'istruzione preparata se l'istruzione viene eseguita una sola volta.

## <a name="syntax"></a>Sintassi  
  
```  
  
public void setEnablePrepareOnFirstPreparedStatementCall(boolean enablePrepareOnFirstPreparedStatementCall)  
```  
  
#### <a name="parameters"></a>Parametri  
 *enablePrepareOnFirstPreparedStatementCall*  
  
 Nuovo valore della proprietà di connessione **enablePrepareOnFirstPreparedStatementCall** .  
 
## <a name="exceptions"></a>Eccezioni  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
 
## <a name="remarks"></a>Remarks  
 Questo metodo è disponibile dal driver JDBC versione 6,4 e successive.
 
## <a name="see-also"></a>Vedere anche  
 [Membri di SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [Classe SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
