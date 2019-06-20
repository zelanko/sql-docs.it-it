---
title: Metodo (lang) getNString | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: b351e999-85bf-498b-915a-f91d89134bce
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: d99c9bf56a6856d953f30f7bd094b205d18bde8e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66762853"
---
# <a name="getnstring-method-javalangstring"></a>Metodo getNString (java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera il valore di designato **NCHAR**, **NVARCHAR**, o **LONGNVARCHAR** parametro sotto forma di stringa in Java linguaggio di programmazione.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public final java.lang.String getNString(java.lang.String parameterName)  
```  
  
#### <a name="parameters"></a>Parametri  
 *parameterName*  
  
 Valore **String** contenente il nome del parametro.  
  
## <a name="return-value"></a>Valore restituito  
 AStringobject.  
  
## <a name="exceptions"></a>Eccezioni  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Questo metodo getNString viene specificato dal metodo getNString nell'interfaccia java.sql.CallableStatement.  
  
## <a name="see-also"></a>Vedere anche  
 [Metodo getNString &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/getnstring-method-sqlservercallablestatement.md)   
 [Metodi di SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-methods.md)  
  
  
