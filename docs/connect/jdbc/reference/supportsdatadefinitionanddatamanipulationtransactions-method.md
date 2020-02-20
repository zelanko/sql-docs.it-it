---
title: Metodo supportsDataDefinitionAndDataManipulationTransactions | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.supportsDataDefinitionAndDataManipulationTransactions
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: fe91c601-9bb3-4364-9131-575a94d3a1b3
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 6f6fd9ac18586c72d1be1a6a4ae5c545b0633d94
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/31/2020
ms.locfileid: "67969528"
---
# <a name="supportsdatadefinitionanddatamanipulationtransactions-method-sqlserverdatabasemetadata"></a>Metodo supportsDataDefinitionAndDataManipulationTransactions (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera un valore che indica se il database supporta sia l'istruzione di definizione dei dati sia quella di manipolazione dei dati all'interno di una transazione.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public boolean supportsDataDefinitionAndDataManipulationTransactions()  
```  
  
## <a name="return-value"></a>Valore restituito  
 **true** se supportato. In caso contrario, **false**.  
  
## <a name="exceptions"></a>Eccezioni  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Osservazioni  
 Questo metodo supportsDataDefinitionAndDataManipulationTransactions viene specificato dal metodo supportsDataDefinitionAndDataManipulationTransactions nell'interfaccia java.sql.DatabaseMetaData.  
  
## <a name="see-also"></a>Vedere anche  
 [Metodi di SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [Membri di SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [Classe SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
