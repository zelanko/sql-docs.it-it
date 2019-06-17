---
title: Metodo getLastUpdateCount (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSource.getLastUpdateCount
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 4c4fbb24-0b02-42da-928c-a903bb591cc7
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 4b6bab492f3383248e7b92fc2ca69d11a30c804f
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/07/2019
ms.locfileid: "66793228"
---
# <a name="getlastupdatecount-method-sqlserverdatasource"></a>Metodo getLastUpdateCount (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Restituisce un valore **booleano** che indica se la proprietà lastUpdateCount è abilitata.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public boolean getLastUpdateCount()  
```  
  
## <a name="return-value"></a>Valore restituito  
 **true** se lastUpdateCount è abilitata. In caso contrario, **false**.  
  
## <a name="remarks"></a>Remarks  
 Se la proprietà lastUpdateCount è impostata su **true**, [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] restituirà solo l'ultimo conteggio aggiornamenti da un'istruzione SQL passata al server. Se la proprietà lastUpdateCount è impostata su **false**, il driver restituirà tutti i conteggi aggiornamenti, inclusi quelli restituiti dai trigger che possono essere stati attivati. Se la proprietà lastUpdateCount non è impostata, il metodo getLastUpdateCount restituisce il valore predefinito **true**.  
  
## <a name="see-also"></a>Vedere anche  
 [Membri di SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Classe SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
