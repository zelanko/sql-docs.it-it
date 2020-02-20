---
title: Metodo getMaxColumnsInSelect (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getMaxColumnsInSelect
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 43c428df-ef91-4f55-81c3-49a4db3379cc
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 1ce02a3d3944480d5c00fa4a3b0369aed38c6d59
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/31/2020
ms.locfileid: "67982199"
---
# <a name="getmaxcolumnsinselect-method-sqlserverdatabasemetadata"></a>Metodo getMaxColumnsInSelect (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera il numero massimo di colonne consentite dal database in un elenco SELECT.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public int getMaxColumnsInSelect()  
```  
  
## <a name="return-value"></a>Valore restituito  
 Valore **int** che indica il numero massimo di colonne consentito.  
  
## <a name="exceptions"></a>Eccezioni  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Osservazioni  
 Questo metodo getMaxColumnsInSelect viene specificato dal metodo getMaxColumnsInSelect nell'interfaccia java.sql.DatabaseMetaData.  
  
## <a name="see-also"></a>Vedere anche  
 [Metodi di SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [Membri di SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [Classe SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
