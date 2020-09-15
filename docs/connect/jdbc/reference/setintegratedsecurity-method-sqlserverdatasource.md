---
description: Metodo setIntegratedSecurity (SQLServerDataSource)
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b172631e774f5ea9da15873a1e8a00121ab46faf
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88431853"
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
  
 **true** se la proprietà integratedSecurity è abilitata. In caso contrario, **false**.  
  
## <a name="remarks"></a>Osservazioni  
 Impostare la proprietà su "**true**" per indicare che in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] verranno usate le credenziali di Windows per autenticare l'utente dell'applicazione. Se impostata su "**true**", [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] cerca nella cache delle credenziali del computer locale le credenziali già specificate per l'accesso al computer o alla rete. Se impostata su "**false**" è necessario specificare il nome utente e la password.  
  
> [!NOTE]  
>  Questa proprietà è supportata solo nei sistemi operativi [!INCLUDE[msCoName](../../../includes/msconame_md.md)] Windows.  
  
 Per altre informazioni sull'uso dell'autenticazione integrata, vedere [Costruzione dell'URL della connessione](../../../connect/jdbc/building-the-connection-url.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Membri di SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Classe SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
