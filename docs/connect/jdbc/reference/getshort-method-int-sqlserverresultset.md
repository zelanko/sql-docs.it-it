---
title: Metodo getShort (int) (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.getShort (int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 0b543c92-feb8-46a4-8477-9b5f94f1cdc7
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 64c4eea3ad1663e6a5f83880de056d9e81ffe4ad
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/08/2020
ms.locfileid: "80925370"
---
# <a name="getshort-method-int-sqlserverresultset"></a>Metodo getShort (int) (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera il valore dell'indice di colonna designato nella riga corrente di questo oggetto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) come elemento **short** nel linguaggio di programmazione Java.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public short getShort(int columnIndex)  
```  
  
#### <a name="parameters"></a>Parametri  
 *columnIndex*  
  
 Valore **int** che indica l'indice di colonna.  
  
## <a name="return-value"></a>Valore restituito  
 Valore **short**.  
  
## <a name="exceptions"></a>Eccezioni  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Osservazioni  
 Questo metodo getShort viene specificato dal metodo getShort nell'interfaccia java.sql.ResultSet.  
  
 Questo metodo è supportato solo sui tipi di dati di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] che possono restituire in modo sicuro un valore integer, ad esempio smallint, tinyint e bit. L'utilizzo di questo metodo su qualsiasi altro tipo di dati genererà un'eccezione.  
  
## <a name="see-also"></a>Vedere anche  
 [Metodo getShort &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/getshort-method-sqlserverresultset.md)   
 [Membri di SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Classe SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
