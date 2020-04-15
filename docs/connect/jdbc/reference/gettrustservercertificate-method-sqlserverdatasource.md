---
title: Metodo getTrustServerCertificate (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- getTrustServerCertificate Method (SQLServerDataSource)
apilocation:
- getTrustServerCertificate Method (SQLServerDataSource)
apitype: Assembly
ms.assetid: e4f443cc-b5d7-4859-81df-836a8642ed07
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f43719fc585a4d1a2fda23fa1111a3918365572b
ms.sourcegitcommit: 54cfeb36c9caa51ec68fa8f4a1918e305db5e00a
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/11/2020
ms.locfileid: "81219310"
---
# <a name="gettrustservercertificate-method-sqlserverdatasource"></a>Metodo getTrustServerCertificate (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Restituisce un valore **Boolean** che indica se la proprietà trustServerCertificate è abilitata.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public boolean getTrustServerCertificate()  
```  
  
## <a name="return-value"></a>Valore restituito  
 **true** se la proprietà trustServerCertificate è abilitata. In caso contrario, **false**.  
  
## <a name="remarks"></a>Osservazioni  
 Se la proprietà trustServerCertificate è impostata su **true**, il certificato Transport Layer Security (TLS), noto in precedenza come Secure Sockets Layer (SSL) di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] viene automaticamente considerato attendibile quando il livello di comunicazione è crittografato tramite TLS. In altri termini, [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] non convalida il certificato TLS/SSL di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Il valore predefinito è **false**.  
  
 Se la proprietà trustServerCertificate è impostata su **false**, il certificato TLS/SSL del server viene convalidato da [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)].  
  
## <a name="see-also"></a>Vedere anche  
 [Membri di SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Classe SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
