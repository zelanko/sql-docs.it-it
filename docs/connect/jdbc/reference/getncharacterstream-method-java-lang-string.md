---
title: Metodo getNCharacterStream (Java. lang. String) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 45d2695b-0727-419d-8921-a51d6feef0aa
author: MightyPen
ms.author: genemi
ms.openlocfilehash: cc5e5e72c4b1aedcc9e10ef74ff2946f2fb2d588
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67981627"
---
# <a name="getncharacterstream-method-javalangstring"></a>Metodo getNCharacterStream (java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera il valore del parametro designato come oggetto Reader in base al nome del parametro.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public final java.io.Reader getNCharacterStream(java.lang.String columnLabel)  
```  
  
#### <a name="parameters"></a>Parametri  
 *columnLabel*  
  
 Valore **String** contenente l'etichetta della colonna.  
  
## <a name="return-value"></a>Valore restituito  
 AReaderobject.  
  
## <a name="exceptions"></a>Eccezioni  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Questo metodo deve essere utilizzato quando si accede a parametri **nchar**, **nvarchar** e **LONGNVARCHAR** .  
  
 Questo metodo getNCharacterStream viene specificato dal metodo getNCharacterStream nell'interfaccia java. SQL. CallableStatement.  
  
## <a name="see-also"></a>Vedere anche  
 [Metodo getNCharacterStream &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/getncharacterstream-method-sqlservercallablestatement.md)   
 [Membri di SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)  
  
  
