---
title: Metodo getTime (int) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.getTime (int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 6c13dea2-511f-48dc-b3db-2d3b72ccc9de
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 454848e471548fbd47e5a0f7985b97546ef87457
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/07/2019
ms.locfileid: "66778980"
---
# <a name="gettime-method-int"></a>Metodo getTime (int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera il valore del parametro designato come oggetto java.sql.Time nel linguaggio di programmazione Java in base all'indice del parametro.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public java.sql.Time getTime(int index)  
```  
  
#### <a name="parameters"></a>Parametri  
 *index*  
  
 Valore **int** che specifica l'indice del parametro.  
  
## <a name="return-value"></a>Valore restituito  
 Un oggetto di runtime.  
  
## <a name="exceptions"></a>Eccezioni  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Questo metodo getTime viene specificato dal metodo getTime nell'interfaccia java.sql.CallableStatement.  
  
 Vedere il grafico denominato "Conversioni dei metodi di richiamo" nella [informazioni sulle conversioni di tipi di dati](../../../connect/jdbc/understanding-data-type-conversions.md) per vedere quali [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] i tipi di dati possono essere recuperati con questo metodo.  
  
## <a name="see-also"></a>Vedere anche  
 [Metodo getTime &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/gettime-method-sqlservercallablestatement.md)   
 [Membri di SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [Classe SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
