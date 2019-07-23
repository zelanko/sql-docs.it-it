---
title: Metodo toapplicationname (SQLServerDataSource) | Microsoft Docs
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
ms.openlocfilehash: 6f0f91762dd168f4136a4a476b47dfe36b749e16
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67975561"
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
  
  
