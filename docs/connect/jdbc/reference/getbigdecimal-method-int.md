---
title: Metodo getBigDecimal (int) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.getBigDecimal Method (int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: f74030d8-3789-463b-b414-2eb01cef8a30
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 01eccd5aafe5b66ed93bebc320fa3f9d425350ff
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67953943"
---
# <a name="getbigdecimal-method-int"></a>Metodo getBigDecimal (int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera il valore del parametro designato come oggetto java.math.BigDecimal con la massima precisione in base all'indice del parametro.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public java.math.BigDecimal getBigDecimal(int index)  
```  
  
#### <a name="parameters"></a>Parametri  
 *index*  
  
 Valore **int** che specifica l'indice del parametro.  
  
## <a name="return-value"></a>Valore restituito  
 Oggetto BigDecimal.  
  
## <a name="exceptions"></a>Eccezioni  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Questo metodo getBigDecimal viene specificato dal Metodo getBigDecimal nell'interfaccia java. SQL. CallableStatement.  
  
## <a name="see-also"></a>Vedere anche  
 [Metodo getBigDecimal &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/getbigdecimal-method-sqlservercallablestatement.md)   
 [Membri di SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [Classe SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
