---
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
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 13ea4a88b4b7a233695e134ef79daccd608d5813
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/07/2019
ms.locfileid: "66773205"
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
  
## <a name="remarks"></a>Remarks  
 Il metodo setUser imposta il nome utente che verrà usato per la connessione a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Se il valore del nome utente non è impostato, il metodo [getUser](../../../connect/jdbc/reference/getuser-method-sqlserverdatasource.md) restituisce il valore predefinito Null.  
  
## <a name="see-also"></a>Vedere anche  
 [Membri di SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Classe SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
