---
title: Metodo setTimestamp per valori di timestamp e calendario | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.setTimestamp (java.lang.String, java.sql.Timestamp, java.util.Calendar))
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 09dca1f9-225a-4acb-9857-9a947e0829be
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 58489b749e58981ea385842528b8eac0bca43780
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/29/2020
ms.locfileid: "67972389"
---
# <a name="settimestamp-method-javalangstring-javasqltimestamp-javautilcalendar"></a>Metodo setTimestamp (java.lang.String, java.sql.Timestamp, java.util.Calendar)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Imposta il parametro designato sui valori di timestamp e calendar specificati.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public void setTimestamp(java.lang.String sCol,  
                         java.sql.Timestamp x,  
                         java.util.Calendar c)  
```  
  
#### <a name="parameters"></a>Parametri  
 *sCol*  
  
 Valore **String** contenente il nome del parametro.  
  
 *x*  
  
 Oggetto Timestamp.  
  
 *c*  
  
 Oggetto Calendar.  
  
## <a name="exceptions"></a>Eccezioni  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Osservazioni  
 Questo metodo setTimestamp viene specificato dal metodo setTimestamp nell'interfaccia java.sql.CallableStatement.  
  
## <a name="see-also"></a>Vedere anche  
 [Metodo setTimestamp &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/settimestamp-method-sqlservercallablestatement.md)   
 [Membri di SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [Classe SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
