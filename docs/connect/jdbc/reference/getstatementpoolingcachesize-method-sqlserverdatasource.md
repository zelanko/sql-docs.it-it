---
title: Metodo getStatementPoolingCacheSize (SQLServerDataSource) | Microsoft Docs
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
ms.openlocfilehash: 2a65be16b8558603dfa90611ad0057f0a0689a10
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/07/2019
ms.locfileid: "66773792"
---
# <a name="getstatementpoolingcachesize-method-sqlserverdatasource"></a>Metodo getStatementPoolingCacheSize (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Restituisce il valore del **statementPoolingCacheSize** proprietà di connessione. Restituisce le dimensioni della cache dell'istruzione preparata per la connessione. '0' indica che la memorizzazione nella cache non abilitata.
  
## <a name="syntax"></a>Sintassi  
  
```
public boolean getStatementPoolingCacheSize();  
```  
  
## <a name="return-value"></a>Valore restituito  
 Il **int** pari al **statementPoolingCacheSize** proprietà di connessione.  

## <a name="exceptions"></a>Eccezioni  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
 
## <a name="remarks"></a>Remarks  
 Questo metodo è disponibile dal driver JDBC versione 6.4 e progressiva.
 
## <a name="see-also"></a>Vedere anche  
 [Membri di SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Classe SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
