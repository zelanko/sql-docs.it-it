---
description: Metodo usesLocalFilePerTable (SQLServerDatabaseMetaData)
title: Metodo usesLocalFilePerTable (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.usesLocalFilePerTable
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 1fafb076-2bb7-4845-9c02-788479f00ca2
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c9d597c32dfad01fcedb257b0d9213bd18a56c6b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88396257"
---
# <a name="useslocalfilepertable-method-sqlserverdatabasemetadata"></a>Metodo usesLocalFilePerTable (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera un valore che indica se il database utilizza un file per ogni tabella.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public boolean usesLocalFilePerTable()  
```  
  
## <a name="return-value"></a>Valore restituito  
 **true** usa un file per ogni tabella. In caso contrario, **false**.  
  
## <a name="exceptions"></a>Eccezioni  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Osservazioni  
 Questo metodo usesLocalFilePerTable viene specificato dal metodo usesLocalFilePerTable nell'interfaccia java.sql.DatabaseMetaData.  
  
## <a name="see-also"></a>Vedere anche  
 [Metodi di SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [Membri di SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [Classe SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
