---
description: Metodo getNumericFunctions (SQLServerDatabaseMetaData)
title: Metodo getNumericFunctions (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getNumericFunctions
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 8d1c3848-bdb7-452a-862f-6421e1a7ce8b
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ac2bbbf8714057ad12d31c27a8b1c929797a6801
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88435133"
---
# <a name="getnumericfunctions-method-sqlserverdatabasemetadata"></a>Metodo getNumericFunctions (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera un elenco delimitato da virgole delle funzioni matematiche disponibili con il database.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public java.lang.String getNumericFunctions()  
```  
  
## <a name="return-value"></a>Valore restituito  
 Valore **String** contenente le funzioni matematiche disponibili.  
  
## <a name="exceptions"></a>Eccezioni  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Osservazioni  
 Questo metodo getNumericFunctions viene specificato dal metodo getNumericFunctions nell'interfaccia java.sql.DatabaseMetaData.  
  
## <a name="see-also"></a>Vedere anche  
 [Metodi di SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [Membri di SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [Classe SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
