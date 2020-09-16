---
description: Metodo getStatementPoolingCacheSize (SQLServerConnection)
title: Metodo getStatementPoolingCacheSize (SQLServerConnection) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerConnection.getStatementPoolingCacheSize
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ''
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 645dcaddce41a8764306f897453d082e72220836
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88434373"
---
# <a name="getstatementpoolingcachesize-method-sqlserverconnection"></a>Metodo getStatementPoolingCacheSize (SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

 Restituisce le dimensioni della cache delle istruzioni preparate per questa connessione. '0' indica che la memorizzazione nella cache non è abilitata.

## <a name="syntax"></a>Sintassi  
  
```  
  
public int getStatementPoolingCacheSize()  
```  

## <a name="return-value"></a>Valore restituito
 Valore **int** che contiene il valore della proprietà di connessione **statementPoolingCacheSize**.

## <a name="exceptions"></a>Eccezioni  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
 
## <a name="remarks"></a>Osservazioni  
 Questo metodo è disponibile dal driver JDBC versione 6.4 e successive.
 
## <a name="see-also"></a>Vedere anche  
 [Membri di SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [Classe SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
