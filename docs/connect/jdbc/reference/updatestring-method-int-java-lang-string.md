---
title: Metodo updateString (int, java.lang.String) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.updateString (int, java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: f8d2f620-0cdf-4a3b-8af4-5e8c4462a42d
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ad0f00eb57bfcf417e45a99ab6b9210ff2277e78
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/31/2020
ms.locfileid: "67998244"
---
# <a name="updatestring-method-int-javalangstring"></a>Metodo updateString (int, java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Aggiorna la colonna designata con un valore **String** in base all'indice di colonna.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public void updateString(int index,  
                         java.lang.String x)  
```  
  
#### <a name="parameters"></a>Parametri  
 *index*  
  
 Valore **int** che indica l'indice di colonna.  
  
 *x*  
  
 Oggetto **String**.  
  
## <a name="exceptions"></a>Eccezioni  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Osservazioni  
 Questo metodo updateString viene specificato dal metodo updateString nell'interfaccia java.sql.ResultSet.  
  
## <a name="see-also"></a>Vedere anche  
 [Metodo updateString &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/updatestring-method-sqlserverresultset.md)   
 [Membri di SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Classe SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
