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
manager: jroth
ms.openlocfilehash: aaf2b256329c66b6169593f71f4e85439aff21ab
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/07/2019
ms.locfileid: "66788258"
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
  
-   Il [registerOutParameter](../../../connect/jdbc/reference/registeroutparameter-method-sqlservercallablestatement.md) metodo della classe SQLServerCallableStatement  
  
 In tale caso, il tipo del parametro viene impostato automaticamente. Se l'applicazione chiama il metodo setObject con un valore obj NULL, il driver presuppone che il tipo del parametro sia un tipo impostato dal metodo chiamato in precedenza.  
  
 Se il valore obj è NULL e le informazioni sul tipo per tale parametro non possono essere determinate, il metodo setObject converte il parametro specificato in un valore CHAR prima di inviarlo al database.  
  
 A partire [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Driver JDBC 3.0, il comportamento di questo metodo viene modificato per il **sendTimeAsDatetime** proprietà di connessione ([impostando le proprietà di connessione](../../../connect/jdbc/setting-the-connection-properties.md)) e [ Setsendtimeasdatetime](../../../connect/jdbc/reference/setsendtimeasdatetime-method-sqlserverdatasource.md).  
  
 Per altre informazioni, vedere [Java configurazione come valori vengono inviati al Server](../../../connect/jdbc/configuring-how-java-sql-time-values-are-sent-to-the-server.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Metodo setObject &#40;SQLServerPreparedStatement&#41;](../../../connect/jdbc/reference/setobject-method-sqlserverpreparedstatement.md)   
 [Membri di SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)   
 [Classe SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)  
  
  
