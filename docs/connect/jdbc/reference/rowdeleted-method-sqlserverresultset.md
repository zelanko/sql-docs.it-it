---
description: Metodo rowDeleted (SQLServerResultSet)
title: Metodo rowDeleted (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.rowDeleted
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 9c6db315-e614-4604-b020-41af6a214cc1
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2e241a0eda4d67295aac47e51723e605fbae144b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88432733"
---
# <a name="rowdeleted-method-sqlserverresultset"></a>Metodo rowDeleted (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera informazioni circa l'eventuale eliminazione di una riga.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public boolean rowDeleted()  
```  
  
## <a name="return-value"></a>Valore restituito  
 **true** se una riga è stata eliminata e le eliminazioni vengono rilevate. In caso contrario, **false**.  
  
## <a name="exceptions"></a>Eccezioni  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Osservazioni  
 Questo metodo rowDeleted viene specificato dal metodo rowDeleted nell'interfaccia java.sql.ResultSet.  
  
 Una riga eliminata potrebbe lasciare uno spazio vuoto visibile in un set di risultati. Questo metodo può essere utilizzato per rilevare gli spazi vuoti in un set di risultati. Il valore restituito dipende dalla possibilità dell'oggetto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) di rilevare le eliminazioni.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] rileva le righe eliminate per tutti i tipi di cursore aggiornabili, sebbene il rilevamento sia temporaneo per i cursori forward e dinamici.  
  
## <a name="see-also"></a>Vedere anche  
 [Membri di SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Classe SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
