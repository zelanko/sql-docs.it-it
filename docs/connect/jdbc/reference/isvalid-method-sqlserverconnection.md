---
title: Metodo IsValid (SQLServerConnection) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 3b0a8bbf-9369-4456-9ab8-1434ccacdd7e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 3915690475e5ce9321af7fc15498c2bde018c640
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67977133"
---
# <a name="isvalid-method-sqlserverconnection"></a>Metodo isValid (SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Indica se questo oggetto [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) non è stato chiuso ed è ancora valido.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public boolean isValid(int timeout)  
```  
  
#### <a name="parameters"></a>Parametri  
 *timeout*  
  
 Valore **int** che specifica il numero di secondi di attesa per la convalida della connessione.  
  
## <a name="return-value"></a>Valore restituito  
 **true** se la connessione è valida; **false** se la connessione non è valida o la validità della connessione non può essere determinata prima che il timeout scada.  
  
## <a name="exceptions"></a>Eccezioni  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Questo metodo IsValid viene specificato dal metodo IsValid nell'interfaccia java. SQL. Connection.  
  
## <a name="see-also"></a>Vedere anche  
 [Membri di SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [Classe SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
