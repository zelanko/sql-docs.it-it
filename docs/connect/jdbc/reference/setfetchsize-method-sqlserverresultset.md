---
description: Metodo setFetchSize (SQLServerResultSet)
title: Metodo setFetchSize (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.setFetchSize
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 233bf4f8-4758-42d0-a80b-33e34fa78027
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d984004b4d306462e2c1345344ebc8072f775a82
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88431863"
---
# <a name="setfetchsize-method-sqlserverresultset"></a>Metodo setFetchSize (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Offre al driver JDBC un hint per il numero di righe che devono essere recuperate dal database, qualora siano necessarie più righe per questo oggetto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md).  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public void setFetchSize(int rows)  
```  
  
#### <a name="parameters"></a>Parametri  
 *rows*  
  
 Valore **int** che indica il numero di righe da recuperare.  
  
## <a name="exceptions"></a>Eccezioni  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Osservazioni  
 Questo metodo setFetchSize viene specificato dal metodo setFetchSize nell'interfaccia java.sql.ResultSet.  
  
 Se la dimensione di recupero specificata è pari a zero, il driver JDBC ignora il valore e valuta la dimensione necessaria. Il valore predefinito viene impostato dall'oggetto [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) che ha creato il set di risultati. È possibile modificare la dimensione di recupero in qualunque momento.  
  
 Questo metodo modifica la dimensione di recupero del blocco per i cursori server e viene applicato alla successiva chiamata al metodo sp_cursorfetch da parte del driver JDBC. L'impostazione della dimensione di recupero su zero ripristina la dimensione di recupero predefinita per il tipo di cursore attualmente utilizzato.  
  
## <a name="see-also"></a>Vedere anche  
 [Membri di SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Classe SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
