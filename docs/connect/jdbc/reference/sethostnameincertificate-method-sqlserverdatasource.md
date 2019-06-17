---
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
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: cde4c07a6a611fd6cd97324c46eae1e2ddc379ce
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/07/2019
ms.locfileid: "66764365"
---
# <a name="sethostnameincertificate-method-sqlserverdatasource"></a>Metodo setHostNameInCertificate (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Imposta il nome host da usare per la convalida del certificato SSL (Secure Sockets Layer) di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public void setHostNameInCertificate(java.lang.String hostNameInCertificate)  
```  
  
#### <a name="parameters"></a>Parametri  
 *hostNameInCertificate*  
  
 Valore **String** contenente il nome host.  
  
## <a name="remarks"></a>Remarks  
 Il valore di hostNameInCertificate viene usato per la convalida del certificato SSL di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] quando il livello di comunicazione è crittografato tramite SSL. Il valore predefinito è null.  
  
 Se la proprietà hostNameInCertificate è impostata su Null o non è specificata, [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] usa il valore della proprietà serverName per la convalida del certificato SSL di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Se la proprietà hostNameInCertificate è impostata su una stringa o una stringa vuota "", tale valore verrà utilizzato dal driver per la convalida del certificato SSL server.  
  
## <a name="see-also"></a>Vedere anche  
 [Membri di SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Classe SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
