---
description: Metodo storesLowerCaseIdentifiers (SQLServerDatabaseMetaData)
title: Metodo storesLowerCaseIdentifiers (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.storesLowerCaseIdentifiers
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: b7dd60f5-c4f3-4b14-9a33-d95327395083
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e2d458e57a69ad8cdd4812d3c0354cd07d4a492e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88431543"
---
# <a name="storeslowercaseidentifiers-method-sqlserverdatabasemetadata"></a>Metodo storesLowerCaseIdentifiers (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera un valore che indica se il database non tiene conto della distinzione tra maiuscole e minuscole negli identificatori SQL con maiuscole e minuscole non racchiusi tra virgolette e li archivia in minuscolo.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public boolean storesLowerCaseIdentifiers()  
```  
  
## <a name="return-value"></a>Valore restituito  
 **true** se gli identificatori vengono archiviati in lettere minuscole. In caso contrario, **false**.  
  
## <a name="exceptions"></a>Eccezioni  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Osservazioni  
 Questo metodo storesLowerCaseIdentifiers viene specificato dal metodo storesLowerCaseIdentifiers nell'interfaccia java.sql.DatabaseMetaData.  
  
## <a name="see-also"></a>Vedere anche  
 [Metodi di SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [Membri di SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [Classe SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
