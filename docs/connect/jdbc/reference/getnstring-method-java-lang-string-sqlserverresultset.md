---
title: Metodo getNString (java.lang.String) (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 546d77e2-723a-42ac-ba3f-fabf2395d376
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e0a76052ccf05927ebd598e2baa37fbf0229bf54
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67981388"
---
# <a name="getnstring-method-javalangstring-sqlserverresultset"></a>Metodo getNString (java.lang.String) (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera il valore della colonna designata nella riga corrente dell'oggetto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) come oggetto java.lang.String.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public java.lang.String getNString(java.lang.String columnLabel)  
```  
  
#### <a name="parameters"></a>Parametri  
 *columnLabel*  
  
 Valore String contenente l'etichetta della colonna.  
  
## <a name="return-value"></a>Valore restituito  
 Oggetto String.  
  
## <a name="exceptions"></a>Eccezioni  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Questo metodo getNString viene specificato dal metodo getNString nell'interfaccia java.sql.SQLServerResultSet.  
  
 Questo metodo può essere utilizzato per recuperare il valore di una colonna **nvarchar**, **nchar**, **nvarchar (max)** , **ntext**o **XML** nella riga corrente di questo oggetto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) . Se si tenta di utilizzare questo metodo per recuperare valori di altri tipi di dati, verrà generata un'eccezione.  
  
## <a name="see-also"></a>Vedere anche  
 [Metodo getNString &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/getnstring-method-sqlserverresultset.md)   
 [Membri di SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)  
  
  
