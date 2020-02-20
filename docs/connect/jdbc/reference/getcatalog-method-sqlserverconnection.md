---
title: Metodo getCatalog (SQLServerConnection) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerConnection.getCatalog
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: e87ef65f-4b5a-4e1c-8db5-7f0932390bb0
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a0f6d74b8dee21333c1358a9f998371e38b5c0cd
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/31/2020
ms.locfileid: "67953346"
---
# <a name="getcatalog-method-sqlserverconnection"></a>Metodo getCatalog (SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera il nome di catalogo corrente di questo oggetto [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md).  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public java.lang.String getCatalog()  
```  
  
## <a name="return-value"></a>Valore restituito  
 Valore **String** contenente il nome del catalogo.  
  
## <a name="exceptions"></a>Eccezioni  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Osservazioni  
 Questo metodo getCatalog viene specificato dal metodo getCatalog nell'interfaccia java.sql.Connection.  
  
 Restituisce la proprietà del catalogo corrente dell'oggetto SQLServerConnection o Null se non è impostata. La proprietà del catalogo viene impostata in modo esplicito con il metodo [setCatalog](../../../connect/jdbc/reference/setcatalog-method-sqlserverconnection.md) oppure viene aggiornata in modo implicito leggendo la modifica dell'ambiente in TDS per il catalogo corrente.  
  
## <a name="see-also"></a>Vedere anche  
 [Membri di SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [Classe SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
