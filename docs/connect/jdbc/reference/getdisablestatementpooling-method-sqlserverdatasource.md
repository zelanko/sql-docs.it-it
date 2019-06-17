---
title: Metodo getDisableStatementPooling (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ''
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 607d729726c421030f4f77247b4e0090c900744c
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/07/2019
ms.locfileid: "66776832"
---
# <a name="getdisablestatementpooling-method-sqlserverdatasource"></a>Metodo getDisableStatementPooling (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Restituisce il valore del **disableStatementPooling** proprietà di connessione. Questa impostazione controlla se l'istruzione di limitazione delle richieste è abilitata o meno per questa connessione.

  
## <a name="syntax"></a>Sintassi  
  
```
public boolean getDisableStatementPooling();  
```  
  
## <a name="return-value"></a>Valore restituito  
 Oggetto **booleana** che contiene il valore di **disableStatementPooling** proprietà di connessione.
  
## <a name="exceptions"></a>Eccezioni  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
 
## <a name="remarks"></a>Remarks  
 Questo metodo è disponibile dal driver JDBC versione 6.4 e progressiva.
 
## <a name="see-also"></a>Vedere anche  
 [Membri di SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Classe SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
