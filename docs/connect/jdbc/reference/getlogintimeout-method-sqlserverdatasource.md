---
title: Metodo getLoginTimeout (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSource.getLoginTimeout
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 316f067c-9e08-456a-af19-b80b0bbd4a5c
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: ec8d033bc6d9bc451eaa606a00881bd4e533aa97
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/07/2019
ms.locfileid: "66793172"
---
# <a name="getlogintimeout-method-sqlserverdatasource"></a>Metodo getLoginTimeout (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Restituisce il numero di secondi di attesa di questo oggetto [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md) durante il tentativo di stabilire una connessione.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public int getLoginTimeout()  
```  
  
## <a name="return-value"></a>Valore restituito  
 Valore **int** che rappresenta il numero di secondi di attesa.  
  
## <a name="remarks"></a>Remarks  
 Se l'applicazione non specifica in modo esplicito un valore di timeout, questo metodo restituisce un valore predefinito di 15 secondi.  
  
 Questo metodo getLoginTimeout viene specificato dal metodo getLoginTimeout nell'interfaccia javax.  
  
## <a name="see-also"></a>Vedere anche  
 [Membri di SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Classe SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
