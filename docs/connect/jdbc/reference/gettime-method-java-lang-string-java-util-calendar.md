---
title: Metodo getTime (java.lang.String, java.util.Calendar) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.getTime (java.lang.String, java.util.Calendar)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 3d4c67c2-a3c8-4a26-a159-89c5d63fda0b
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 6b9d74778d3ff1fc62b5549fbea7e0f97bf1e477
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66778875"
---
# <a name="gettime-method-javalangstring-javautilcalendar"></a>Metodo getTime (java.lang.String, java.util.Calendar)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera il valore del parametro designato come oggetto java.sql.Time nel linguaggio di programmazione Java, in base al nome del parametro, utilizzando l'oggetto Calendar specificato.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public java.sql.Time getTime(java.lang.String sCol,  
                             java.util.Calendar cal)  
```  
  
#### <a name="parameters"></a>Parametri  
 *sCol*  
  
 Valore **String** contenente il nome del parametro.  
  
 *cal*  
  
 Un oggetto calendario.  
  
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
  
  
