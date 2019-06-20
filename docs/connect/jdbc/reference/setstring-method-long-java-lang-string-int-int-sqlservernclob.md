---
title: Metodo setString (long, java.lang.String, int, int) - NClob | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 2d5e9f50-15b2-4c76-8bfc-3b5be49c2781
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: ad49b4a5e675d4ff6635583e0b64a1e57434ff22
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66762271"
---
# <a name="setstring-method-long-javalangstring-int-int-sqlservernclob"></a>Metodo setString (long, java.lang.String, int, int) (SQLServerNClob)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Scrive la stringa specificata nell'oggetto NCLOB a partire dalla posizione specificata e in base all'offset e alla lunghezza specificati.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
int setString(long pos,  
              java.lang.String str,  
              int offset,  
              int len)  
```  
  
#### <a name="parameters"></a>Parametri  
 *pos*  
  
 Posizione di inizio della scrittura nell'oggetto **NCLOB**. La prima posizione è 1.  
  
 *str*  
  
 Stringa da scrivere nell'oggetto **NCLOB**.  
  
 *offset*  
  
 Offset in *str* in base al quale iniziare la lettura dei caratteri da scrivere.  
  
 *len*  
  
 Numero di caratteri da scrivere.  
  
## <a name="exceptions"></a>Eccezioni  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Questo metodo setString viene specificato dal metodo setString nell'interfaccia java.sql.NClob.  
  
## <a name="see-also"></a>Vedere anche  
 [Metodi di SQLServerNClob](../../../connect/jdbc/reference/sqlservernclob-methods.md)   
 [Membri di SQLServerNClob](../../../connect/jdbc/reference/sqlservernclob-members.md)   
 [Classe SQLServerNClob](../../../connect/jdbc/reference/sqlservernclob-class.md)  
  
  
