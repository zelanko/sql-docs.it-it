---
description: Metodo supportsSelectForUpdate (SQLServerDatabaseMetaData)
title: Metodo supportsSelectForUpdate (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.supportsSelectForUpdate
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 721bc8e3-36c0-4fa6-8561-4f8d54c8265a
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 653e9fdbc8b0b2092819751ddf4070eed0ea0873
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88450193"
---
# <a name="supportsselectforupdate-method-sqlserverdatabasemetadata"></a>Metodo supportsSelectForUpdate (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera un valore che indica se il database supporta istruzioni SELECT FOR UPDATE.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public boolean supportsSelectForUpdate()  
```  
  
## <a name="return-value"></a>Valore restituito  
 **true** se supportato. In caso contrario, **false**.  
  
## <a name="exceptions"></a>Eccezioni  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Osservazioni  
 Questo metodo supportsSelectForUpdate viene specificato dal metodo supportsSelectForUpdate nell'interfaccia java.sql.DatabaseMetaData.  
  
## <a name="see-also"></a>Vedere anche  
 [Metodi di SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [Membri di SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [Classe SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
