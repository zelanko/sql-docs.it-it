---
title: Metodo setIntegratedSecurity (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSource.setIntegratedSecurity
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 4c968ee4-b041-424a-bf69-cc2c4a4f51c6
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 7d922c2c2fcfadb6b7807b8d2845f8d3e6c5188c
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/07/2019
ms.locfileid: "66780448"
---
# <a name="setintegratedsecurity-method-sqlserverdatasource"></a>Metodo setIntegratedSecurity (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Imposta un valore **Boolean** che indica se la proprietà integratedSecurity è abilitata.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public void setIntegratedSecurity(boolean enable)  
```  
  
#### <a name="parameters"></a>Parametri  
 *enable*  
  
 **true** se integratedSecurity è abilitata. In caso contrario, **false**.  
  
## <a name="remarks"></a>Remarks  
 Impostare la proprietà su "**true**" per indicare che in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] verranno usate le credenziali di Windows per autenticare l'utente dell'applicazione. Se impostata su "**true**", [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] cerca nella cache delle credenziali del computer locale le credenziali già specificate per l'accesso al computer o alla rete. Se impostata su "**false**" è necessario specificare il nome utente e la password.  
  
> [!NOTE]  
>  Questa proprietà è supportata solo nei sistemi operativi [!INCLUDE[msCoName](../../../includes/msconame_md.md)] Windows.  
  
 Per altre informazioni sull'uso dell'autenticazione integrata, vedere [Building the Connection URL](../../../connect/jdbc/building-the-connection-url.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Membri di SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Classe SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
