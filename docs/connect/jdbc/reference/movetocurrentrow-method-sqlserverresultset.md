---
description: Metodo moveToCurrentRow (SQLServerResultSet)
title: Metodo moveToCurrentRow (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.moveToCurrentRow
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 9a7c754c-2d72-4207-b3bd-2afc6047fb3d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7c5b26d92a64c8c9bfa952ac04a3a924c987d5f3
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88433193"
---
# <a name="movetocurrentrow-method-sqlserverresultset"></a>Metodo moveToCurrentRow (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Sposta il cursore nella posizione memorizzata, generalmente la riga corrente.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public void moveToCurrentRow()  
```  
  
## <a name="exceptions"></a>Eccezioni  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Osservazioni  
 Questo metodo moveToCurrentRow viene specificato dal metodo moveToCurrentRow nell'interfaccia java.sql.ResultSet.  
  
 Questo metodo non ha effetto se il cursore non è sulla riga di inserimento.  
  
## <a name="see-also"></a>Vedere anche  
 [Membri di SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Classe SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
