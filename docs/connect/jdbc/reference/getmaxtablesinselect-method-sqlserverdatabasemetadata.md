---
title: Metodo getMaxTablesInSelect (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getMaxTablesInSelect
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: f5291217-2a0c-4daa-9e39-9f348fc911f7
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 51db61a1ea139878269e90291d27b2acce778d86
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/07/2019
ms.locfileid: "66792344"
---
# <a name="getmaxtablesinselect-method-sqlserverdatabasemetadata"></a>Metodo getMaxTablesInSelect (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera il numero massimo di tabelle consentite dal database in un'istruzione SELECT.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public int getMaxTablesInSelect()  
```  
  
## <a name="return-value"></a>Valore restituito  
 Valore **int** che indica il numero massimo di tabelle consentito.  
  
## <a name="exceptions"></a>Eccezioni  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Questo metodo getMaxTablesInSelect viene specificato dal metodo getMaxTablesInSelect nell'interfaccia DatabaseMetaData.  
  
## <a name="see-also"></a>Vedere anche  
 [Metodi di SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [Membri di SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [Classe SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
