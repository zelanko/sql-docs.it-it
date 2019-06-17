---
title: Metodo getServerName (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSource.getServerName
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 3004ed22-5d69-4dd0-8761-d39f0b7dde13
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 8fd762ff700b543345dc9c2abbba3eabf6dcb2fb
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/07/2019
ms.locfileid: "66791940"
---
# <a name="getservername-method-sqlserverdatasource"></a>Metodo getServerName (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Restituisce il nome dell'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public java.lang.String getServerName()  
```  
  
## <a name="return-value"></a>Valore restituito  
 Valore **String** contenente il nome del server o Null se non viene impostato alcun valore.  
  
## <a name="remarks"></a>Remarks  
 Il nome del server è il nome host del computer di destinazione che esegue [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Se la proprietà getServerName non è impostata, getServerName restituisce il valore predefinito Null.  
  
## <a name="see-also"></a>Vedere anche  
 [Membri di SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Classe SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
