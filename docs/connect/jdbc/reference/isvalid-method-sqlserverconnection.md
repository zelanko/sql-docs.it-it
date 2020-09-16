---
description: Metodo isValid (SQLServerConnection)
title: Metodo isValid (SQLServerConnection) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 3b0a8bbf-9369-4456-9ab8-1434ccacdd7e
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1b9c55645d33f9bd92e577ff9aa84b76f5948cf7
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88433353"
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
  
## <a name="remarks"></a>Osservazioni  
 Questo metodo isValid viene specificato dal metodo isValid nell'interfaccia java.sql.Connection.  
  
## <a name="see-also"></a>Vedere anche  
 [Membri di SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [Classe SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
