---
title: Metodo relative (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.relative
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 2bcdbb69-95fd-4ae8-8488-1a75a91fe2e0
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: b8907a5e2eb2ead5202e8aec9fd5320a6047a5f4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66797706"
---
# <a name="relative-method-sqlserverresultset"></a>Metodo relative (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Sposta il cursore del numero di righe specificato rispetto alla riga corrente, in direzione positiva o negativa.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public boolean relative(int nRows)  
```  
  
#### <a name="parameters"></a>Parametri  
 *nRows*  
  
 Valore **int** che indica il numero di righe da spostare.  
  
## <a name="return-value"></a>Valore restituito  
 **true** se il cursore si trova in una riga. In caso contrario, **false**.  
  
## <a name="exceptions"></a>Eccezioni  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Questo metodo relativo viene specificato dal relativo metodo nell'interfaccia ResultSet.  
  
 Se si tenta di spostare oltre la prima o ultima riga nel set di risultati, il cursore viene posizionato prima o dopo la prima o ultima riga. La chiamata al metodo `relative(0)` è valida, ma non modifica la posizione del cursore.  
  
 La chiamata al metodo `relative(1)` è identica alla chiamata al metodo [next](../../../connect/jdbc/reference/next-method-sqlserverresultset.md). La chiamata al metodo `relative(-1)` è identica alla chiamata al metodo [previous](../../../connect/jdbc/reference/previous-method-sqlserverresultset.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Membri di SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Classe SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
