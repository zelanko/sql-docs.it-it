---
title: Metodo getString (int) (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.getString (int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: bfa493c4-fe07-449b-b4d0-384e1a1fce48
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 8690984c3795bb07497a3d255d85766930c1ab07
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66773902"
---
# <a name="getstring-method-int-sqlserverresultset"></a>Metodo getString (int) (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera il valore dell'indice di colonna designato nella riga corrente di questo oggetto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) come **String** nel linguaggio di programmazione Java.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public java.lang.String getString(int columnIndex)  
```  
  
#### <a name="parameters"></a>Parametri  
 *columnIndex*  
  
 Valore **int** che indica l'indice di colonna.  
  
## <a name="return-value"></a>Valore restituito  
 Valore **String**.  
  
## <a name="exceptions"></a>Eccezioni  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Questo metodo getString viene specificato dal metodo getString nell'interfaccia java.sql.ResultSet.  
  
 Tutte le colonne in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] possono essere restituite come stringa. Pertanto, possono essere restituite una rappresentazione **String** di tutti i tipi numerici e basati su caratteri e una rappresentazione stringa esadecimale di colonne binarie quali binary, varbinary, varbinary(max), image, timestamp e uniqueidentifier.  
  
 I tipi dipendenti dai percorsi quali money, smallmoney, datetime, smalldatetime, float, real, decimal e numeric restituiranno il formato canonico toString() per il valore sottostante del tipo.  
  
 I tipi definiti dall'utente vengono restituiti come valori **String** esadecimali.  
  
## <a name="see-also"></a>Vedere anche  
 [Metodo getString &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/getstring-method-sqlserverresultset.md)   
 [Membri di SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Classe SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
