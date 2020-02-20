---
title: Metodo getConnection () | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSource.getConnection ()
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 7f520e96-5313-468f-b987-535ddaea027e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 1941f86d06672d942150c8399b6f87aa346faac0
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/31/2020
ms.locfileid: "67952642"
---
# <a name="getconnection-method-"></a>Metodo getConnection ()
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Tenta di stabilire una connessione con l'origine dati rappresentata da questo oggetto [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md).  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public java.sql.Connection getConnection()  
```  
  
## <a name="return-value"></a>Valore restituito  
 Oggetto [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md).  
  
## <a name="exceptions"></a>Eccezioni  
 java.sql.SQLException  
  
## <a name="remarks"></a>Osservazioni  
 Questo metodo getConnection viene specificato dal metodo getConnection nell'interfaccia javax.sql.DataSource.  
  
## <a name="see-also"></a>Vedere anche  
 [Metodo getConnection &#40;SQLServerDataSource&#41;](../../../connect/jdbc/reference/getconnection-method-sqlserverdatasource.md)   
 [Membri di SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Classe SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
