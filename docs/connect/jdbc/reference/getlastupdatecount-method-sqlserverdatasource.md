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
ms.openlocfilehash: e0d284e02be13af60bf7d8e7d447835f7eccd90a
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/31/2020
ms.locfileid: "67982605"
---
# <a name="getlastupdatecount-method-sqlserverdatasource"></a>Metodo getLastUpdateCount (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Restituisce un valore **booleano** che indica se la proprietà lastUpdateCount è abilitata.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public boolean getLastUpdateCount()  
```  
  
## <a name="return-value"></a>Valore restituito  
 **true** se lastUpdateCount è abilitato. In caso contrario, **false**.  
  
## <a name="remarks"></a>Osservazioni  
 Se la proprietà lastUpdateCount è impostata su **true**, [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] restituirà solo l'ultimo conteggio aggiornamenti da un'istruzione SQL passata al server. Se la proprietà lastUpdateCount è impostata su **false**, il driver restituirà tutti i conteggi aggiornamenti, inclusi quelli restituiti dai trigger che possono essere stati attivati. Se la proprietà lastUpdateCount non è impostata, il metodo getLastUpdateCount restituisce il valore predefinito **true**.  
  
## <a name="see-also"></a>Vedere anche  
 [Membri di SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Classe SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
