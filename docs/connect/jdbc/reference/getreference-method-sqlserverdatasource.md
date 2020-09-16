---
description: Metodo getReference (SQLServerDataSource)
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8916c339a4a1d6c8373e3fbaf5a130dcc168155e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88434883"
---
# <a name="getreference-method-sqlserverdatasource"></a>Metodo getReference (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Restituisce un riferimento a questo oggetto [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md).  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public javax.naming.Reference getReference()  
```  
  
## <a name="return-value"></a>Valore restituito  
 Oggetto Reference.  
  
## <a name="remarks"></a>Osservazioni  
 Questo metodo getReference viene specificato dal metodo getReference nell'interfaccia javax. naming. Referenceable.  
  
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
  
  
