---
title: Metodo getMaxCursorNameLength (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getMaxCursorNameLength
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 2cd2bed9-adf4-4bcd-ae5a-d0e3428bc709
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 53c47f912711a486ea60cf0181411e7ed68029ab
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/31/2020
ms.locfileid: "67982145"
---
# <a name="getmaxcursornamelength-method-sqlserverdatabasemetadata"></a>Metodo getMaxCursorNameLength (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera il numero massimo di caratteri consentito dal database in un nome di cursore.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public int getMaxCursorNameLength()  
```  
  
## <a name="return-value"></a>Valore restituito  
 Valore **int** che indica il numero massimo di caratteri consentito.  
  
## <a name="exceptions"></a>Eccezioni  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Osservazioni  
 Questo metodo getMaxCursorNameLength viene specificato dal metodo getMaxCursorNameLength nell'interfaccia java.sql.DatabaseMetaData.  
  
## <a name="see-also"></a>Vedere anche  
 [Metodi di SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [Membri di SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [Classe SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
