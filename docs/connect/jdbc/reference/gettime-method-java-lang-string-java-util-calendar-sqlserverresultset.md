---
title: Metodo getTime (java.lang.String, java.util.Calendar) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.getTime (java.lang.String, java.util.Calendar)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 13b51f77-cec9-45fc-862e-3d2bb2d718d7
author: MightyPen
ms.author: genemi
ms.openlocfilehash: b66a142789e855eaf0e4524554892ea85c7b9cbe
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/29/2020
ms.locfileid: "67979071"
---
# <a name="gettime-method-javalangstring-javautilcalendar-sqlserverresultset"></a>Metodo getTime (java.lang.String, java.util.Calendar) (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera il valore del nome della colonna designata nella riga corrente di questo oggetto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) come oggetto java.sql.Time nel linguaggio di programmazione Java, utilizzando l'oggetto Calendar specificato.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public java.sql.Time getTime(java.lang.String colName,  
                             java.util.Calendar cal)  
```  
  
#### <a name="parameters"></a>Parametri  
 *colName*  
  
 Valore **String** contenente il nome della colonna.  
  
 *cal*  
  
 Oggetto Calendar.  
  
## <a name="return-value"></a>Valore restituito  
 Oggetto Time.  
  
## <a name="exceptions"></a>Eccezioni  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Osservazioni  
 Questo metodo getTime viene specificato dal metodo getTime nell'interfaccia java.sql.ResultSet.  
  
 Questo metodo restituisce una parte dell'ora valida di un tipo di dati datetime o smalldatetime di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], con la parte della data impostata sulla data di base (1970/01/01) di Java nel fuso orario del calendario.  
  
## <a name="see-also"></a>Vedere anche  
 [Metodo getTime &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/gettime-method-sqlserverresultset.md)   
 [Membri di SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Classe SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
