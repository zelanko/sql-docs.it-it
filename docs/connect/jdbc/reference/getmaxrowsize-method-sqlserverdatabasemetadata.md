---
title: Metodo getMaxRowSize (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getMaxRowSize
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: abb5a204-76ff-4381-ab2b-896a19b202f3
author: MightyPen
ms.author: genemi
ms.openlocfilehash: b261a0f02075ffea736899dfa941a4e9f5acfb86
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67982039"
---
# <a name="getmaxrowsize-method-sqlserverdatabasemetadata"></a>Metodo getMaxRowSize (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera il numero massimo di byte consentiti dal database in una singola riga.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public int getMaxRowSize()  
```  
  
## <a name="return-value"></a>Valore restituito  
 Valore **int** che indica il numero massimo di byte consentito.  
  
## <a name="exceptions"></a>Eccezioni  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Questo metodo getMaxRowSize viene specificato dal metodo getMaxRowSize nell'interfaccia java. SQL. DatabaseMetaData.  
  
## <a name="see-also"></a>Vedere anche  
 [Metodi di SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [Membri di SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [Classe SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
