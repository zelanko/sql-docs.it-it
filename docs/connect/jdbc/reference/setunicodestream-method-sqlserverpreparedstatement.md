---
title: Metodo setUnicodeStream (SQLServerPreparedStatement) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerPreparedStatement.setUnicodeStream
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 0a413e83-e0a4-41f8-9fe0-33ce4d368ee4
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a80dddc28fbca156fe31a7620f1d1b0460359a75
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67972166"
---
# <a name="setunicodestream-method-sqlserverpreparedstatement"></a>Metodo setUnicodeStream (SQLServerPreparedStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Imposta il numero di parametro designato sul flusso di input specificato, che disporrà del numero specificato di byte.  
  
> [!NOTE]  
>  Questo metodo è stato deprecato dalla specifica JDBC e, chiamandolo, verrà generata un'eccezione relativa a una mancata implementazione.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public final void setUnicodeStream(int n,  
                                   java.io.InputStream x,  
                                   int length)  
```  
  
#### <a name="parameters"></a>Parametri  
 *n*  
  
 Valore **int** che indica il numero di parametro.  
  
 *x*  
  
 Oggetto InputStream.  
  
 *length*  
  
 Numero di byte.  
  
## <a name="exceptions"></a>Eccezioni  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Questo metodo setUnicodeStream viene specificato dal Metodo setUnicodeStream nell'interfaccia java. SQL. PreparedStatement.  
  
## <a name="see-also"></a>Vedere anche  
 [Membri di SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)   
 [Classe SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)  
  
  
