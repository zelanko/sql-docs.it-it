---
title: Metodo secatalog (SQLServerConnection) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerConnection.setCatalog
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 553c0603-c07d-436a-86eb-3ba6b51bd696
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 78b4d49029c6a0f2696cc93348bff7b32767bc13
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67974836"
---
# <a name="setcatalog-method-sqlserverconnection"></a>Metodo setCatalog (SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Imposta il nome di catalogo specificato per selezionare uno spazio secondario del database di questo oggetto [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) nel quale lavorare.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public void setCatalog(java.lang.String catalog)  
```  
  
#### <a name="parameters"></a>Parametri  
 *catalog*  
  
 Valore **String** contenente il nome del catalogo.  
  
## <a name="exceptions"></a>Eccezioni  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Questo metodo di decatalogazione viene specificato dal metodo secatalog nell'interfaccia java. SQL. Connection.  
  
 L'argomento *catalog* viene preceduto automaticamente da caratteri di escape in [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]. Se si usa questo metodo, viene impostata la proprietà catalog per l'oggetto Connection. Tale proprietà non viene impostata in modo implicito in altro modo.  
  
## <a name="see-also"></a>Vedere anche  
 [Membri di SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [Classe SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
