---
title: Metodo isPoolable (SQLServerStatement) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: b8a12ac5-57cb-4288-9973-c7d5cebd197c
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: a5fcc6d842299884bec758ca66f303bf3e8ed625
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/07/2019
ms.locfileid: "66796465"
---
# <a name="ispoolable-method-sqlserverstatement"></a>Metodo isPoolable (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Restituisce un valore che indica se è possibile aggiungere un'istruzione al pool di istruzioni fornito dall'utente.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public boolean isPoolable() throws SQLException  
```  
  
## <a name="return-value"></a>Valore restituito  
 **true** se l'istruzione può essere aggiunto al pool di istruzione fornito dall'utente; **false** in caso contrario.  
  
## <a name="exceptions"></a>Eccezioni  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 [setPoolable](../../../connect/jdbc/reference/setpoolable-method-sqlserverstatement.md) modifica il comportamento di inserimento in pool di un oggetto.  
  
## <a name="see-also"></a>Vedere anche  
 [Membri di SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [Classe SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
