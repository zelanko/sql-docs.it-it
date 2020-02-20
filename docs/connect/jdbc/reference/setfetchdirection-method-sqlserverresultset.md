---
title: Metodo setFetchDirection (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.setFetchDirection
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 4ee82290-508d-4bff-a5c5-8a56338deef8
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d801a0184259ae22f86ea5ec23391ef78b23ce38
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/31/2020
ms.locfileid: "67974272"
---
# <a name="setfetchdirection-method-sqlserverresultset"></a>Metodo setFetchDirection (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Specifica un hint per la direzione di elaborazione delle righe in questo oggetto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md).  
  
> [!NOTE]  
>  Questo metodo non è attualmente supportato da [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]. Se si utilizza questo metodo, nel driver JDBC l'impostazione viene memorizzata, ma non viene utilizzata per effettuare operazioni.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public void setFetchDirection(int direction)  
```  
  
#### <a name="parameters"></a>Parametri  
 *direction*  
  
 Valore **int** che indica la direzione di recupero suggerita. I possibili valori sono i seguenti:  
  
 ResultSet.FETCH_FORWARD  
  
 ResultSet.FETCH_REVERSE  
  
 ResultSet.FETCH_UNKNOWN  
  
## <a name="exceptions"></a>Eccezioni  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Osservazioni  
 Questo metodo setFetchDirection viene specificato dal metodo setFetchDirection nell'interfaccia java.sql.ResultSet.  
  
 Il valore iniziale di questo metodo è determinato dall'oggetto [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) che ha prodotto questo oggetto SQLServerResultSet. È possibile modificare la direzione di recupero in qualunque momento.  
  
> [!NOTE]  
>  L'utilizzo di questo metodo quando il tipo di cursore è forward only non ha effetto.  
  
## <a name="see-also"></a>Vedere anche  
 [Membri di SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Classe SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
