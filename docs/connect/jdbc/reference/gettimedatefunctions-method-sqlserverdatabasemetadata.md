---
description: Metodo getTimeDateFunctions (SQLServerDatabaseMetaData)
title: Metodo getTimeDateFunctions (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getTimeDateFunctions
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: a56e08ae-6f4e-4dc6-b175-ff457d0d7a81
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a5a47aab1bf388c5975f5d639a0de6c45f79eb3d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88434103"
---
# <a name="gettimedatefunctions-method-sqlserverdatabasemetadata"></a>Metodo getTimeDateFunctions (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera un elenco delimitato da virgole delle funzioni data e ora disponibili con il database.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public java.lang.String getTimeDateFunctions()  
```  
  
## <a name="return-value"></a>Valore restituito  
 Valore **String** contenente un elenco delle funzioni di ora e data.  
  
## <a name="exceptions"></a>Eccezioni  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Osservazioni  
 Questo metodo getTimeDateFunctions viene specificato dal metodo getTimeDateFunctions nell'interfaccia java.sql.DatabaseMetaData.  
  
## <a name="see-also"></a>Vedere anche  
 [Metodi di SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [Membri di SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [Classe SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
