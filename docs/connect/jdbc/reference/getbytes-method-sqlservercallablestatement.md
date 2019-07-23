---
title: Metodo GetBytes (SQLServerCallableStatement) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.getBytes
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: b6e88cea-54b3-4d18-a9af-db54abf19f45
author: MightyPen
ms.author: genemi
ms.openlocfilehash: b8db05472492e7893dd7874e137baaa5cf8fd89e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68213730"
---
# <a name="getbytes-method-sqlservercallablestatement"></a>Metodo getBytes (SQLServerCallableStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera il valore del parametro designato come matrice di byte.  
  
## <a name="overload-list"></a>Elenco degli overload  
  
|nome|Descrizione|  
|----------|-----------------|  
|[getBytes (int)](../../../connect/jdbc/reference/getbytes-method-int.md)|Recupera il valore del parametro designato come matrice di valori byte in base all'indice del parametro.|  
|[getBytes (java.lang.String)](../../../connect/jdbc/reference/getbytes-method-java-lang-string.md)|Recupera il valore del parametro designato come matrice di valori byte in base al nome del parametro.|  
  
## <a name="remarks"></a>Remarks  
 In una versione precedente di [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] è possibile usare SQLServerCallableStatement.getBytes per convertire valori tra matrici di byte e il tipo di dati di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] **date**, **time**, **datetime2** o **datetimeoffset**. In questa versione l'utilizzo del metodo con questi tipi di dati provoca un'eccezione indicante che la conversione non è supportata.  
  
## <a name="see-also"></a>Vedere anche  
 [Membri di SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [Classe SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
