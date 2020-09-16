---
description: Metodo updateArray (int, java.sql.Array)
title: Metodo updateArray (int, java.sql.Array) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.updateArray (int, java.sql.Array)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 464f7e3f-3e8a-4b2d-aebd-1c040583d52c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4456f4f39b8eeda140dd929039ec4e91001f6c5d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88478467"
---
# <a name="updatearray-method-int-javasqlarray"></a>Metodo updateArray (int, java.sql.Array)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Aggiorna la colonna designata con un oggetto Array in base all'indice della colonna.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public void updateArray(int columnIndex,  
                        java.sql.Array x)  
```  
  
#### <a name="parameters"></a>Parametri  
 *columnIndex*  
  
 Valore **int** che indica l'indice di colonna.  
  
 *x*  
  
 Oggetto Array.  
  
## <a name="exceptions"></a>Eccezioni  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Osservazioni  
 Questo metodo updateArray viene specificato dal metodo updateArray nell'interfaccia java.sql.ResultSet.  
  
## <a name="see-also"></a>Vedere anche  
 [Metodo updateArray &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/updatearray-method-sqlserverresultset.md)   
 [Membri di SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Classe SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
