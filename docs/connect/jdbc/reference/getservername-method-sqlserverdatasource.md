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
ms.openlocfilehash: 487d214dbdd6974442749dd0cff6ac24fe9d1977
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/31/2020
ms.locfileid: "67979949"
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
  
## <a name="remarks"></a>Osservazioni  
 Il nome del server è il nome host del computer di destinazione che esegue [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Se la proprietà getServerName non è impostata, getServerName restituisce il valore predefinito Null.  
  
## <a name="see-also"></a>Vedere anche  
 [Membri di SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Classe SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
