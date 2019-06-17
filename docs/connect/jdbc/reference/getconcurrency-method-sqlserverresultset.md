---
title: Metodo getConcurrency (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.getConcurrency
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 207e25f4-769c-4ff3-913c-3517b06208e4
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 7386a03b56b319f6299d6d52d0f1736b74a75565
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/07/2019
ms.locfileid: "66763296"
---
# <a name="getconcurrency-method-sqlserverresultset"></a>Metodo getConcurrency (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera la modalità di concorrenza di questo oggetto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md).  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public int getConcurrency()  
```  
  
## <a name="return-value"></a>Valore restituito  
 Valore **int** che indica il tipo di concorrenza. Può essere uno dei valori seguenti:  
  
 ResultSet.CONCUR_READ_ONLY  
  
 ResultSet.CONCUR_UPDATABLE  
  
## <a name="exceptions"></a>Eccezioni  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Questo metodo getConcurrency viene specificato dal metodo getConcurrency nell'interfaccia ResultSet.  
  
 La concorrenza usata è determinata dall'oggetto [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) che ha creato il set di risultati.  
  
 Questo metodo può essere utilizzato per determinare la concorrenza effettiva. Se selezionati dall'applicazione, saranno restituiti CONCUR_READ_ONLY o CONCUR_UPDATABLE. Se l'applicazione ha utilizzato la concorrenza predefinita, verrà restituito CONCUR_READ_ONLY.  
  
## <a name="see-also"></a>Vedere anche  
 [Membri di SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Classe SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
