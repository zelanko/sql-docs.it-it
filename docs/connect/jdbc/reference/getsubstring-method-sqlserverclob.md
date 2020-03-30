---
title: Metodo getSubString (SQLServerClob) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerClob.getSubString
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: bf915590-a883-4403-befa-5b5bb42f34d8
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 73b82c550c78d409accd423b485fc7b9825dbc8c
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/29/2020
ms.locfileid: "67979330"
---
# <a name="getsubstring-method-sqlserverclob"></a>Metodo getSubString (SQLServerClob)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Restituisce una copia della sottostringa specificata nell'oggetto CLOB in base alla posizione di inizio specificata e al numero di caratteri da copiare.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public java.lang.String getSubString(long pos,  
                                     int length)  
```  
  
#### <a name="parameters"></a>Parametri  
 *pos*  
  
 Primo carattere della sottostringa da estrarre. Il primo carattere si trova nella posizione 1.  
  
 *length*  
  
 Numero di caratteri consecutivi da copiare.  
  
## <a name="return-value"></a>Valore restituito  
 Valore **String** che rappresenta la sottostringa specificata nell'oggetto CLOB.  
  
## <a name="exceptions"></a>Eccezioni  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Osservazioni  
 Questo metodo getSubString viene specificato dal metodo getSubString nell'interfaccia java.sql.Clob.  
  
 Se si tenta di ottenere zero caratteri da un oggetto CLOB Null o di lunghezza zero, viene restituita una stringa vuota. Se si tenta di ottenere un numero qualsiasi di caratteri in qualsiasi posizione diversa da 1 in un oggetto CLOB di lunghezza zero, verrà generata un'eccezione di posizione.  
  
## <a name="see-also"></a>Vedere anche  
 [Metodi di SQLServerClob](../../../connect/jdbc/reference/sqlserverclob-methods.md)   
 [Membri di SQLServerClob](../../../connect/jdbc/reference/sqlserverclob-members.md)   
 [Classe SQLServerClob](../../../connect/jdbc/reference/sqlserverclob-class.md)  
  
  
