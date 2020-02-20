---
title: Metodo getEnablePrepareOnFirstPreparedStatementCall (SQLServerConnection) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerConnection.getEnablePrepareOnFirstPreparedStatementCall
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ''
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ac1cf4dbd8c8c14b5c97dbfecbe81d397c1598ce
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/31/2020
ms.locfileid: "67983440"
---
# <a name="getenableprepareonfirstpreparedstatementcall-method-sqlserverconnection"></a>Metodo getEnablePrepareOnFirstPreparedStatementCall (SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

 Restituisce il valore della proprietà di connessione **enablePrepareOnFirstPreparedStatementCall**. Se è il valore è false, la prima esecuzione chiamerà sp_executesql e non preparerà un'istruzione. La seconda esecuzione chiamerà sp_prepexec e configurerà effettivamente un handle per l'istruzione preparata. Le esecuzioni seguenti chiameranno sp_execute. Viene così eliminata la necessità di sp_unprepare alla chiusura dell'istruzione preparata se l'istruzione viene eseguita una sola volta. L'impostazione predefinita per questa opzione può essere modificata chiamando setDefaultEnablePrepareOnFirstPreparedStatementCall().

## <a name="syntax"></a>Sintassi  
  
```  
  
public boolean getEnablePrepareOnFirstPreparedStatementCall()  
```  

## <a name="return-value"></a>Valore restituito
 Valore **boolean** che contiene il valore della proprietà di connessione **enablePrepareOnFirstPreparedStatementCall**.

## <a name="exceptions"></a>Eccezioni  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
 
## <a name="remarks"></a>Osservazioni  
 Questo metodo è disponibile dal driver JDBC versione 6.4 e successive.
 
## <a name="see-also"></a>Vedere anche  
 [Membri di SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [Classe SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
