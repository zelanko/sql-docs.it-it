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
ms.openlocfilehash: a90d00957310c64f908816198a47e4c3ba7293b9
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/29/2020
ms.locfileid: "67979517"
---
# <a name="getstatementpoolingcachesize-method-sqlserverdatasource"></a>Metodo getStatementPoolingCacheSize (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Restituisce il valore della proprietà di connessione **statementPoolingCacheSize**. Restituisce le dimensioni della cache delle istruzioni preparate per questa connessione. '0' indica che la memorizzazione nella cache non è abilitata.
  
## <a name="syntax"></a>Sintassi  
  
```
public boolean getStatementPoolingCacheSize();  
```  
  
## <a name="return-value"></a>Valore restituito  
 Valore **int** della proprietà di connessione **statementPoolingCacheSize**.  

## <a name="exceptions"></a>Eccezioni  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
 
## <a name="remarks"></a>Osservazioni  
 Questo metodo è disponibile dal driver JDBC versione 6.4 e successive.
 
## <a name="see-also"></a>Vedere anche  
 [Membri di SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Classe SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
