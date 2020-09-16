---
description: Metodo isSparseColumnSet (SQLServerResultSetMetaData)
title: Metodo isSparseColumnSet (SQLServerResultSetMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ac363670-78ae-49f1-aeda-4fba3329a258
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 86fbbcdc34259e6b3d783d34ca77af57bcfba89f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88433373"
---
# <a name="issparsecolumnset-method-sqlserverresultsetmetadata"></a>Metodo isSparseColumnSet (SQLServerResultSetMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Indica se una colonna in un set di risultati è un set di colonne di tipo sparse.  
  
## <a name="syntax"></a>Sintassi  
  
```scr  
public boolean isSparseColumnSet(int column)  
```  
  
#### <a name="parameters"></a>Parametri  
 *column*  
  
 Indice della colonna (in base uno).  
  
## <a name="return-value"></a>Valore restituito  
 **true** se una colonna in un set di risultati è un set di colonne di tipo sparse. In caso contrario, **false**.  
  
## <a name="remarks"></a>Osservazioni  
 Questo metodo non consente di recuperare informazioni dal database.  
  
## <a name="see-also"></a>Vedere anche  
 [Metodi di SQLServerResultSetMetaData](../../../connect/jdbc/reference/sqlserverresultsetmetadata-methods.md)   
 [Membri di SQLServerResultSetMetaData](../../../connect/jdbc/reference/sqlserverresultsetmetadata-members.md)   
 [Classe SQLServerResultSetMetaData](../../../connect/jdbc/reference/sqlserverresultsetmetadata-class.md)  
  
  
