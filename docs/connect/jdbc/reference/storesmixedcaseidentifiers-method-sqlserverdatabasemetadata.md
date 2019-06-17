---
title: Metodo storesMixedCaseIdentifiers (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.storesMixedCaseIdentifiers
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: a91e5cd6-22b1-464e-aeec-665590737a74
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 6455b582fe89fc12d32b52a2c4c1edfc323bdd73
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/07/2019
ms.locfileid: "66766785"
---
# <a name="storesmixedcaseidentifiers-method-sqlserverdatabasemetadata"></a>Metodo storesMixedCaseIdentifiers (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera un valore che indica se il database non tiene conto della distinzione tra maiuscole e minuscole negli identificatori SQL con maiuscole e minuscole non racchiusi tra virgolette e li archivia in minuscolo e maiuscolo.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public boolean storesMixedCaseIdentifiers()  
```  
  
## <a name="return-value"></a>Valore restituito  
 **true** se gli identificatori vengono archiviati in minuscolo e maiuscolo. In caso contrario, **false**.  
  
## <a name="exceptions"></a>Eccezioni  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Questo metodo storesMixedCaseIdentifiers viene specificato dal metodo storesMixedCaseIdentifiers nell'interfaccia DatabaseMetaData.  
  
## <a name="see-also"></a>Vedere anche  
 [Metodi di SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [Membri di SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [Classe SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
