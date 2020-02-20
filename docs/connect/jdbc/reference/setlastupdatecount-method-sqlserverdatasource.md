---
title: Metodo setLastUpdateCount (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSource.setLastUpdateCount
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 5487631a-1107-4169-84ca-b77fd09bea66
author: MightyPen
ms.author: genemi
ms.openlocfilehash: fd9776dd60e82067b0d048e2f385b2bc685b79ea
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/31/2020
ms.locfileid: "67974115"
---
# <a name="setlastupdatecount-method-sqlserverdatasource"></a>Metodo setLastUpdateCount (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Imposta un valore **booleano** che indica se la proprietà lastUpdateCount è abilitata.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public void setLastUpdateCount(boolean lastUpdateCount)  
```  
  
#### <a name="parameters"></a>Parametri  
 *lastUpdateCount*  
  
 **true** se lastUpdateCount è abilitato. In caso contrario, **false**.  
  
## <a name="remarks"></a>Osservazioni  
 Se la proprietà lastUpdateCount è impostata su **true**, [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] restituirà solo l'ultimo conteggio di aggiornamenti da un'istruzione SQL passata al server. Se la proprietà lastUpdateCount è impostata su **false**, il driver restituirà tutti i conteggi aggiornamenti, inclusi quelli restituiti dai trigger che possono essere stati attivati. Se la proprietà [lastUpdateCount](../../../connect/jdbc/reference/getlastupdatecount-method-sqlserverdatasource.md) non è impostata, il metodo getLastUpdateCount restituisce il valore predefinito **true**.  
  
## <a name="see-also"></a>Vedere anche  
 [Membri di SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Classe SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
