---
title: Metodo setNString (SQLServerCallableStatement) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 6494300b-7fc0-4076-8311-22d35a96cdc6
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 5891b971bcf6129ec3b5fcec4e9ae8f0301283b9
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/29/2020
ms.locfileid: "67973592"
---
# <a name="setnstring-method-sqlservercallablestatement"></a>Metodo setNString (SQLServerCallableStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Imposta il parametro designato sull'oggetto String specificato.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public final void setNString(java.lang.String parameterName, java.lang.String value)  
```  
  
#### <a name="parameters"></a>Parametri  
 *parameterName*  
  
 Valore **String** che indica il nome del parametro.  
  
 *value*  
  
 Oggetto String.  
  
## <a name="exceptions"></a>Eccezioni  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Osservazioni  
 Questo metodo deve essere usato per i tipi di dati **NCHAR**, **NVARCHAR**, **NTEXT** e **XML**.  
  
 Questo metodo setNString viene specificato dal metodo setNString nell'interfaccia java.sql.CallableStatement.  
  
## <a name="see-also"></a>Vedere anche  
 [Membri di SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [Classe SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
