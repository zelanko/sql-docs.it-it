---
description: Metodo setHostNameInCertificate (SQLServerDataSource)
title: Metodo setHostNameInCertificate (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- setHostNameInCertificate Method (SQLServerDataSource)
apilocation:
- setHostNameInCertificate Method (SQLServerDataSource)
apitype: Assembly
ms.assetid: 2bcf4f2e-a103-4374-abc4-ffad4ce8e3c0
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 886a32898b04cc8907a832d54a3051222e4d0fb7
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88431823"
---
# <a name="sethostnameincertificate-method-sqlserverdatasource"></a>Metodo setHostNameInCertificate (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Imposta il nome host da usare per convalidare il certificato Transport Layer Security (TLS), noto in precedenza come Secure Sockets Layer (SSL), di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public void setHostNameInCertificate(java.lang.String hostNameInCertificate)  
```  
  
#### <a name="parameters"></a>Parametri  
 *hostNameInCertificate*  
  
 Valore **String** contenente il nome host.  
  
## <a name="remarks"></a>Osservazioni  
 Il valore di hostNameInCertificate viene usato per la convalida del certificato TLS/SSL di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] quando il livello di comunicazione è crittografato tramite TLS. Il valore predefinito è null.  
  
 Se la proprietà hostNameInCertificate è impostata su Null o non è specificata, [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] usa il valore della proprietà serverName per la convalida del certificato TLS/SSL di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Se la proprietà hostNameInCertificate è impostata su una stringa o una stringa vuota "", tale valore verrà usato dal driver per la convalida del certificato TLS/SSL server.  
  
## <a name="see-also"></a>Vedere anche  
 [Membri di SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Classe SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
