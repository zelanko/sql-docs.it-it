---
description: Metodo setTrustServerCertificate (SQLServerDataSource)
title: Metodo setTrustServerCertificate (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- setTrustServerCertificate Method (SQLServerDataSource)
apilocation:
- setTrustServerCertificate Method (SQLServerDataSource)
apitype: Assembly
ms.assetid: 6c37b518-147e-4cd9-9eff-b48a3f5888c6
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1fb76148ae8c63dd30bd1532ec74d545bcc3388d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88355097"
---
# <a name="settrustservercertificate-method-sqlserverdatasource"></a>Metodo setTrustServerCertificate (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Imposta un valore **Boolean** che indica se la proprietà trustServerCertificate è abilitata.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public void setTrustServerCertificate(boolean trustServerCertificate)  
```  
  
#### <a name="parameters"></a>Parametri  
 *trustServerCertificate*  
  
 **true** se il certificato Transport Layer Security (TLS), precedentemente noto come Secure Sockets Layer (SSL), del server deve essere considerato automaticamente attendibile quando il livello di comunicazione viene crittografato tramite TLS. In caso contrario, **false**.  
  
## <a name="remarks"></a>Osservazioni  
 Se la proprietà trustServerCertificate è impostata su **true**, il certificato TLS/SSL di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] viene automaticamente considerato attendibile quando il livello di comunicazione è crittografato tramite TLS. In altri termini, [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] non convalida il certificato TLS/SSL di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Il valore predefinito è **false**.  
  
 Se la proprietà trustServerCertificate è impostata su **false**, il certificato TLS/SSL del server viene convalidato da [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)].  
  
## <a name="see-also"></a>Vedere anche  
 [Membri di SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Classe SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
