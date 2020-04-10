---
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
ms.openlocfilehash: 788efd1f35643e3bcefd929f455b2c21677f7723
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/08/2020
ms.locfileid: "80927285"
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
  
  
