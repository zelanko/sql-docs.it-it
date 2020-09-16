---
description: Metodo getHostNameInCertificate (SQLServerDataSource)
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 26e931b104c1eba44a09e1b43b51e00d2beaad70
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88435873"
---
# <a name="gethostnameincertificate-method-sqlserverdatasource"></a>Metodo getHostNameInCertificate (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Restituisce il nome host usato per convalidare il certificato Transport Layer Security (TLS) di SQL Server, noto in precedenza come Secure Sockets Layer (SSL).  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public java.lang.String getHostNameInCertificate()  
```  
  
## <a name="return-value"></a>Valore restituito  
 Valore **String** contenente il nome host oppure Null se non è impostato alcun valore.  
  
## <a name="remarks"></a>Osservazioni  
 Il nome host viene usato per la convalida del valore del certificato TLS/SSL di SQL Server quando il livello di comunicazione è crittografato tramite TLS/SSL.  
  
 Se il nome host non è impostato, il metodo [getHostNameInCertificate](../../../connect/jdbc/reference/gethostnameincertificate-method-sqlserverdatasource.md) restituisce Null.  
  
## <a name="see-also"></a>Vedere anche  
 [Membri di SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Classe SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
