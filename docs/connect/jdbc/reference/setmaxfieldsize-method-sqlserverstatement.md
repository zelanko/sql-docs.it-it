---
description: Metodo setMaxFieldSize (SQLServerStatement)
title: Metodo setMaxFieldSize (SQLServerStatement) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerStatement.setMaxFieldSize
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 38f7fc1d-acad-4d10-9fc8-3c0669d93b07
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b63564218687d9cc12973d044f04c94ec056f615
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88431693"
---
# <a name="setmaxfieldsize-method-sqlserverstatement"></a>Metodo setMaxFieldSize (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Imposta sul numero di byte specificato il limite per il numero massimo di byte in una colonna [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) che archivia valori di tipo carattere o binari.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public final void setMaxFieldSize(int max)  
```  
  
#### <a name="parameters"></a>Parametri  
 *max*  
  
 Valore**int** che indica il numero massimo di byte.  
  
## <a name="exceptions"></a>Eccezioni  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Osservazioni  
 Questo metodo setMaxFieldSize viene specificato dal metodo setMaxFieldSize nell'interfaccia java.sql.Statement.  
  
## <a name="see-also"></a>Vedere anche  
 [Membri di SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [Classe SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
