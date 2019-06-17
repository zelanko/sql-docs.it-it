---
title: Metodo getHostNameInCertificate (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- getHostNameInCertificate Method (SQLServerDataSource)
apilocation:
- getHostNameInCertificate Method (SQLServerDataSource)
apitype: Assembly
ms.assetid: 45ea04e2-9ea5-4171-9136-d09f8a95e128
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 1bdd2e849654c78fab2fdff8b409c204a1298834
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/07/2019
ms.locfileid: "66774482"
---
# <a name="gethostnameincertificate-method-sqlserverdatasource"></a>Metodo getHostNameInCertificate (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Restituisce il nome host utilizzato per la convalida del certificato SSL (Secure Sockets Layer) di SQL Server.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public java.lang.String getHostNameInCertificate()  
```  
  
## <a name="return-value"></a>Valore restituito  
 Valore **String** contenente il nome host oppure Null se non è impostato alcun valore.  
  
## <a name="remarks"></a>Remarks  
 Il nome host viene utilizzato per la convalida del valore del certificato SSL di SQL Server quando il livello di comunicazione è crittografato tramite SSL.  
  
 Se il nome host non è impostato, il metodo [getHostNameInCertificate](../../../connect/jdbc/reference/gethostnameincertificate-method-sqlserverdatasource.md) restituisce Null.  
  
## <a name="see-also"></a>Vedere anche  
 [Membri di SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Classe SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
