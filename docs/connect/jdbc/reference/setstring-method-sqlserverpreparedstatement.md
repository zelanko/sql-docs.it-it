---
title: Metodo sestring (SQLServerPreparedStatement) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerPreparedStatement.setString
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 25dabdc9-c60f-485a-87eb-306067964765
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ca49c8e50527ab7cafce9c93c314a0e363b45402
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67972580"
---
# <a name="setstring-method-sqlserverpreparedstatement"></a>Metodo setString (SQLServerPreparedStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Imposta il parametro designato sul valore **String** specificato.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public final void setString(int index,  
                            java.lang.String str)  
```  
  
#### <a name="parameters"></a>Parametri  
 *index*  
  
 Valore **int** che indica il numero di parametro.  
  
 *str*  
  
 Valore **String**.  
  
## <a name="exceptions"></a>Eccezioni  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Questo metodo setString viene specificato dal metodo setString nell'interfaccia java.sql.PreparedStatement.  
  
## <a name="see-also"></a>Vedere anche  
 [Membri di SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)   
 [Classe SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)  
  
  
