---
description: Metodo getExtraNameCharacters (SQLServerDatabaseMetaData)
title: Metodo getExtraNameCharacters (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getExtraNameCharacters
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: a22becfe-0f07-4a15-8d11-06d4054b2369
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7701c2fe192e5f60acf78c2e59e562c8688e6d40
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88436103"
---
# <a name="getextranamecharacters-method-sqlserverdatabasemetadata"></a>Metodo getExtraNameCharacters (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera tutti i caratteri aggiuntivi che possono essere utilizzati nei nomi di identificatore non racchiusi tra virgolette, ad esempio quelli non inclusi in a-z, A-Z, 0-9 e _.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public java.lang.String getExtraNameCharacters()  
```  
  
## <a name="return-value"></a>Valore restituito  
 Una **stringa** contenente i caratteri aggiuntivi.  
  
## <a name="exceptions"></a>Eccezioni  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Osservazioni  
 Questo metodo getExtraNameCharacters viene specificato dal metodo getExtraNameCharacters nell'interfaccia java.sql.DatabaseMetaData.  
  
 Quando si utilizza [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] con un database di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], il metodo restituisce i caratteri aggiuntivi $, # e \@.  
  
## <a name="see-also"></a>Vedere anche  
 [Metodi di SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [Membri di SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [Classe SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
