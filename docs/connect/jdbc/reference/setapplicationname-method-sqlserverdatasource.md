---
title: Metodo setApplicationName (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSource.setApplicationName
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 24d6e48d-53c4-4da2-a6de-1cdff463c9cd
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3853262dd5e1a62542387e9b61f8c30f5967f09b
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 12/11/2018
ms.locfileid: "53210590"
---
# <a name="setapplicationname-method-sqlserverdatasource"></a>Metodo setApplicationName (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Imposta il nome dell'applicazione.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public void setApplicationName(java.lang.String applicationName)  
```  
  
#### <a name="parameters"></a>Parametri  
 *applicationName*  
  
 Valore **String** che contiene il nome dell'applicazione.  
  
## <a name="remarks"></a>Remarks  
 Il nome dell'applicazione viene usato per identificare l'applicazione specifica nei diversi strumenti di profiling e registrazione di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Se il nome dell'applicazione non è impostato, il metodo getApplicationName restituisce la stringa non localizzata " [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] ".  
  
## <a name="see-also"></a>Vedere anche  
 [Membri di SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Classe SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
