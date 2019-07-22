---
title: Classe SQLServerXAResource | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: df957b79-536f-4db7-b6ac-3d59343559fc
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 282201b7ff3f5b2ebfe4d8a1224d4d1b39285c53
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67970087"
---
# <a name="sqlserverxaresource-class"></a>Classe SQLServerXAResource
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Rappresenta un oggetto XAResource per la gestione di transazioni distribuite XA.  
  
 **Pacchetto:** com.microsoft.sqlserver.jdbc  
  
 **Estende:** java.lang.Object  
  
 **Implementa:** javax.transaction.xa.XAResource  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public class SQLServerXAResource  
```  
  
## <a name="remarks"></a>Remarks  
 Le transazioni XA vengono implementate in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] tramite Gestione transazioni distribuite (DTC, Distributed Transaction Manager) di [!INCLUDE[msCoName](../../../includes/msconame_md.md)]. La classe SQLServerXAResource esegue chiamate a una DLL estesa di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] denominata sqljdbc_xa.dll che si interfaccia con DTC. Le chiamate XA ricevute dall'oggetto SQLServerXAResource (XA_START, XA_END, XA_PREPARE e così via) vengono mappate alle chiamate corrispondenti alle funzioni DTC.  
  
## <a name="see-also"></a>Vedere anche  
 [Membri di SQLServerXAResource](../../../connect/jdbc/reference/sqlserverxaresource-members.md)   
 [Informazioni di riferimento sull'API del driver JDBC](../../../connect/jdbc/reference/jdbc-driver-api-reference.md)  
  
  
