---
description: Metodo getMaxTableNameLength (SQLServerDatabaseMetaData)
title: Metodo getMaxTableNameLength (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getMaxTableNameLength
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 5c51218f-c6e8-49f4-ad09-292e849ca43a
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2cd6418ac069b97483fb7f0e37ae188941053967
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88435483"
---
# <a name="getmaxtablenamelength-method-sqlserverdatabasemetadata"></a>Metodo getMaxTableNameLength (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera il numero massimo di caratteri consentito dal database in un nome di tabella.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public int getMaxTableNameLength()  
```  
  
## <a name="return-value"></a>Valore restituito  
 Valore **int** che indica il numero massimo di caratteri consentito.  
  
## <a name="exceptions"></a>Eccezioni  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Osservazioni  
 Questo metodo getMaxTableNameLength viene specificato dal metodo getMaxTableNameLength nell'interfaccia java.sql.DatabaseMetaData.  
  
## <a name="see-also"></a>Vedere anche  
 [Metodi di SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [Membri di SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [Classe SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
