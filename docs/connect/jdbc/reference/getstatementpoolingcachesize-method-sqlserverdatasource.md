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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2ef133c2c661cd9c4778d6ca9b3efec8e51d5a5d
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/08/2020
ms.locfileid: "80926224"
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
  
  
