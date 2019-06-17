---
title: Metodo Truncate (SQLServerClob) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerClob.truncate
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ea3b2a03-387e-49d7-a4d6-ca6a6a354c90
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 2f07f68e179dcac33a67778dd3671442d0b78b6d
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/07/2019
ms.locfileid: "66785012"
---
# <a name="truncate-method-sqlserverclob"></a>Metodo truncate (SQLServerClob)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Tronca l'oggetto CLOB in base alla lunghezza specificata.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public void truncate(long len)  
```  
  
#### <a name="parameters"></a>Parametri  
 *len*  
  
 Lunghezza espressa in caratteri, in base alla quale deve essere troncato l'oggetto CLOB.  
  
## <a name="exceptions"></a>Eccezioni  
 java.sql.SQLException  
  
## <a name="remarks"></a>Remarks  
 Questo metodo troncamento è specificato dal metodo nell'interfaccia CLOB di troncamento.  
  
## <a name="see-also"></a>Vedere anche  
 [Metodi di SQLServerClob](../../../connect/jdbc/reference/sqlserverclob-methods.md)   
 [Membri di SQLServerClob](../../../connect/jdbc/reference/sqlserverclob-members.md)   
 [Classe SQLServerClob](../../../connect/jdbc/reference/sqlserverclob-class.md)  
  
  
