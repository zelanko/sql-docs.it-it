---
title: Metodo getDatabaseMinorVersion (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getDatabaseMinorVersion
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 18163668-60d6-4d54-aaf1-c338b8c90f2a
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3f0dc89feb46c0210a07730e00cda84e3008387e
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/08/2020
ms.locfileid: "80923224"
---
# <a name="getdatabaseminorversion-method-sqlserverdatabasemetadata"></a>Metodo getDatabaseMinorVersion (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera il numero della versione secondaria del database sottostante.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public int getDatabaseMinorVersion()  
```  
  
## <a name="return-value"></a>Valore restituito  
 Valore **int** che indica la versione secondaria del database.  
  
## <a name="exceptions"></a>Eccezioni  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Osservazioni  
 Questo metodo getDatabaseMinorVersion viene specificato dal metodo getDatabaseMinorVersion nell'interfaccia java.sql.DatabaseMetaData.  
  
## <a name="see-also"></a>Vedere anche  
 [Metodi di SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [Membri di SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [Classe SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
