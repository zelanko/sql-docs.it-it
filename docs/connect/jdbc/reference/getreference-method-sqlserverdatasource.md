---
title: Metodo getReference (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSource.getReference
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: b3fb1a97-86ee-4977-adca-c35ae199dbb3
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 50eace66b5f792ce9876d56dab8768555a43392f
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/07/2019
ms.locfileid: "66775609"
---
# <a name="getreference-method-sqlserverdatasource"></a>Metodo getReference (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Restituisce un riferimento a questo oggetto [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md).  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public javax.naming.Reference getReference()  
```  
  
## <a name="return-value"></a>Valore restituito  
 Un oggetto di riferimento.  
  
## <a name="remarks"></a>Remarks  
 Questo metodo getReference viene specificato dal metodo getReference nell'interfaccia Referenceable.  
  
 Prima di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] JDBC Driver 3.0, se l'oggetto SQLServerDataSource.setTrustStorePassword veniva chiamato su un oggetto SQLServerDataSource, la password era disponibile nell'oggetto restituito da SQLServerDataSource.getReference, e questo poteva essere usato per eseguire connessioni aggiuntive. Nel driver JDBC 3.0 sarà necessario impostare la password sull'oggetto restituito da SQLServerDataSource.getReference, prima di eseguire connessioni con l'oggetto.  
  
 Inoltre, se si imposta SQLServerDataSource.setTrustStorePassword prima di associare le proprietà delle origini dati, la chiamata a SQLServerDataSource.setTrustStorePassword deve essere effettuata prima di ottenere la connessione. Ad esempio,  
  
```  
ctx = new InitialContext(System.getProperties());  
  
SQLServerDataSource ds1 = (SQLServerDataSource) ctx.lookup(jndiName);  
  
ds1.setTrustStorePassword("XXXXX");  
Connection con = ds1.getConnection("user", "XXXXXX");  
  
ctx.rebind(jndiName, ds1);  
SQLServerDataSource ds2 = (SQLServerDataSource) ctx.lookup(jndiName);  
ds2.setTrustStorePassword("XXXXX");   // reset the truststore password  
con = ds2.getConnection("user", "XXXXXX");   // provide userid and password again  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Membri di SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Classe SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
