---
title: Metodo setByte (SQLServerCallableStatement) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.setByte
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 0fbb03a5-61ee-4fb8-9dea-dce5cb1a367e
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 38dea38205d2eba003f1cdeb4c8af5718311f591
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66797647"
---
# <a name="setbyte-method-sqlservercallablestatement"></a>Metodo setByte (SQLServerCallableStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Imposta il parametro designato sul valore **byte** specificato.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public void setByte(java.lang.String sCol,  
                    byte b)  
```  
  
#### <a name="parameters"></a>Parametri  
 *sCol*  
  
 Valore **String** contenente il nome del parametro.  
  
 *b*  
  
 Valore **byte**.  
  
## <a name="exceptions"></a>Eccezioni  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Questo metodo setByte viene specificato dal metodo setByte nell'interfaccia java.sql.CallableStatement.  
  
## <a name="see-also"></a>Vedere anche  
 [Membri di SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [Classe SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
