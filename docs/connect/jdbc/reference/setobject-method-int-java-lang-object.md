---
title: Metodo setObject (int, java.lang.Object) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerPreparedStatement.setObject (int, java.lang.Object)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 61f19faa-3006-4a1c-974c-55951e3b3000
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e4ab210a30080472a777d151695a04ec49ff1041
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67973378"
---
# <a name="setobject-method-int-javalangobject"></a>Metodo setObject (int, java.lang.Object)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Imposta il valore del parametro designato tramite l'oggetto specificato.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public final void setObject(int index,  
                            java.lang.Object obj)  
```  
  
#### <a name="parameters"></a>Parametri  
 *index*  
  
 Valore **int** che indica il numero di parametro.  
  
 *obj*  
  
 Oggetto.  
  
## <a name="exceptions"></a>Eccezioni  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Questo metodo setObject viene specificato dal metodo setObject nell'interfaccia java.sql.PreparedStatement.  
  
 Prima di chiamare il metodo setObject, l'applicazione potrebbe impostare il parametro specificato tramite uno dei metodi seguenti:  
  
-   I metodi set\<Type> della classe SQLServerPreparedStatement o della classe SQLServerCallableStatement  
  
-   I metodi setNull della classe SQLServerPreparedStatement o della classe SQLServerCallableStatement  
  
-   Metodo [registerOutParameter](../../../connect/jdbc/reference/registeroutparameter-method-sqlservercallablestatement.md) della classe SQLServerCallableStatement  
  
 In tale caso, il tipo del parametro viene impostato automaticamente. Se l'applicazione chiama il metodo setObject con un valore obj NULL, il driver presuppone che il tipo del parametro sia un tipo impostato dal metodo chiamato in precedenza.  
  
 Se il valore obj è NULL e le informazioni sul tipo per tale parametro non possono essere determinate, il metodo setObject converte il parametro specificato in un valore CHAR prima di inviarlo al database.  
  
 A partire dal driver JDBC 3,0, il comportamento di questo metodo viene modificato dalla proprietà di connessione **sendTimeAsDatetime** ([impostazione delle proprietà di connessione](../../../connect/jdbc/setting-the-connection-properties.md)) e [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [SQLServerDataSource. setSendTimeAsDatetime](../../../connect/jdbc/reference/setsendtimeasdatetime-method-sqlserverdatasource.md).  
  
 Per ulteriori informazioni, vedere [configurazione della modalità di invio dei valori java. SQL. Time al server](../../../connect/jdbc/configuring-how-java-sql-time-values-are-sent-to-the-server.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Metodo setObject &#40;SQLServerPreparedStatement&#41;](../../../connect/jdbc/reference/setobject-method-sqlserverpreparedstatement.md)   
 [Membri di SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)   
 [Classe SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)  
  
  
