---
title: Metodo getInt (int) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.getInt (int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: c86792bb-096e-4c58-8b9e-74491ccf83a6
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 0add66584a71475b33a79760c0225e47afc34fb3
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/07/2019
ms.locfileid: "66781227"
---
# <a name="getint-method-int"></a>Metodo getInt (int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera il valore del parametro designato come **int** nel linguaggio di programmazione Java in base all'indice del parametro.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public int getInt(int index)  
```  
  
#### <a name="parameters"></a>Parametri  
 *index*  
  
 Valore **int** che specifica l'indice del parametro.  
  
## <a name="return-value"></a>Valore restituito  
 Un' **int** valore.  
  
## <a name="exceptions"></a>Eccezioni  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Questo metodo getInt viene specificato dal metodo getInt nell'interfaccia java.sql.CallableStatement.  
  
 Questo metodo è supportato solo sui tipi di dati di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] che possono restituire in modo sicuro un valore integer, ad esempio int, smallint, tinyint e bit. L'utilizzo di questo metodo su qualsiasi altro tipo di dati genererà un'eccezione.  
  
## <a name="see-also"></a>Vedere anche  
 [Metodo getInt &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/getint-method-sqlservercallablestatement.md)   
 [Membri di SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [Classe SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
