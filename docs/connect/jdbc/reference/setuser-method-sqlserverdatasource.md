---
description: Metodo setUser (SQLServerDataSource)
title: Metodo setUser (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSource.setUser
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: d2ea7906-2d10-438d-aa51-f576eea923c7
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b887e5b0af5d4a91a8cbea2b3676fd958ac3c077
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88472178"
---
# <a name="setuser-method-sqlserverdatasource"></a>Metodo setUser (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Imposta il nome utente utilizzato per la connessione all'origine dati.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public void setUser(java.lang.String user)  
```  
  
#### <a name="parameters"></a>Parametri  
 *user*  
  
 Valore **String** contenente il nome utente.  
  
## <a name="remarks"></a>Osservazioni  
 Il metodo setUser imposta il nome utente che verrà usato per la connessione a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Se il valore del nome utente non è impostato, il metodo [getUser](../../../connect/jdbc/reference/getuser-method-sqlserverdatasource.md) restituisce il valore predefinito Null.  
  
## <a name="see-also"></a>Vedere anche  
 [Membri di SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Classe SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
