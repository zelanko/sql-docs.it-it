---
title: Metodo setAutoCommit (SQLServerConnection) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerConnection.setAutoCommit
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: db1e22d2-e53f-474e-8c99-cb1fff7f491a
author: MightyPen
ms.author: genemi
ms.openlocfilehash: dbf9b18fdc6b590f085b5be6babd64100006163a
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/31/2020
ms.locfileid: "67975272"
---
# <a name="setautocommit-method-sqlserverconnection"></a>Metodo setAutoCommit (SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Imposta la modalità di commit automatico per questo oggetto [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) sullo stato specificato.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public void setAutoCommit(boolean value)  
```  
  
#### <a name="parameters"></a>Parametri  
 *value*  
  
 **true** per abilitare la modalità di commit automatico per la connessione, **false** per disabilitarla.  
  
## <a name="exceptions"></a>Eccezioni  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Osservazioni  
 Questo metodo setAutoCommit viene specificato dal metodo setAutoCommit nell'interfaccia java.sql.Connection.  
  
 Se una connessione è in modalità autocommit, tutte le relative istruzioni SQL vengono eseguite e sottoposte a commit come transazioni singole. In caso contrario, le istruzioni SQL vengono raggruppate in transazioni terminate da una chiamata al metodo [commit](../../../connect/jdbc/reference/commit-method-sqlserverconnection.md) o [rollback](../../../connect/jdbc/reference/rollback-method-sqlserverconnection.md). Per impostazione predefinita, le nuove connessioni sono in modalità autocommit.  
  
 Il commit si verifica quando l'istruzione viene completata o si verifica l'esecuzione successiva, indipendentemente dall'evento che avviene per primo. In caso di istruzioni che restituiscono un oggetto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md), l'istruzione viene completata quando è stata recuperata l'ultima riga del set di risultati o quando quest'ultimo è stato chiuso. In casi avanzati, una singola istruzione potrebbe restituire più risultati oltre ai valori dei parametri di output. In queste circostanze, il commit si verifica quando sono stati recuperati tutti i risultati e i valori dei parametri di output.  
  
 Quando la modalità commit automatico è **false**, il driver JDBC avvierà in modo implicito una nuova transazione dopo ogni commit.  
  
> [!NOTE]  
>  Se questo metodo viene chiamato durante una transazione, quest'ultima viene sottoposta a commit.  
  
## <a name="see-also"></a>Vedere anche  
 [Membri di SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [Classe SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
