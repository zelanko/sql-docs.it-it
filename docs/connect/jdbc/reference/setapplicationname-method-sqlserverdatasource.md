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
manager: jroth
ms.openlocfilehash: 9f4c4707e06b25e1bb9e394c141f5fb1afa90599
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/07/2019
ms.locfileid: "66765333"
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
  
  
