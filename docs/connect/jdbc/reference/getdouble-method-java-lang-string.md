---
title: Metodo getDouble (java.lang.String) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.getDouble (java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 8eab6a8e-91f3-47b1-8707-5e57368ad0c6
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 81faa132ccdba32537615aeed4a34aa39e1b7c76
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/31/2020
ms.locfileid: "67983539"
---
# <a name="getdouble-method-javalangstring"></a>Metodo getDouble (java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera il valore del parametro designato come oggetto **double** nel linguaggio di programmazione Java in base al nome del parametro.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public double getDouble(java.lang.String sCol)  
```  
  
#### <a name="parameters"></a>Parametri  
 *sCol*  
  
 Valore **String** contenente il nome del parametro.  
  
## <a name="return-value"></a>Valore restituito  
 Valore **double**.  
  
## <a name="exceptions"></a>Eccezioni  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Osservazioni  
 Questo metodo getDouble viene specificato dal metodo getDouble nell'interfaccia java.sql.CallableStatement.  
  
 Questo metodo restituisce tutti i tipi di dati numerici con fedeltà **double** di Java.  
  
## <a name="see-also"></a>Vedere anche  
 [Metodo getDouble &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/getdouble-method-sqlservercallablestatement.md)   
 [Membri di SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [Classe SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
