---
title: Metodo getSelectMethod (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSource.getSelectMethod
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: b6255d2e-0028-474a-afa8-553ef092243e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d0919590ec727068b97ef66d3d0f6824aefcbe03
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/31/2020
ms.locfileid: "67980032"
---
# <a name="getselectmethod-method-sqlserverdatasource"></a>Metodo getSelectMethod (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Restituisce il tipo di cursore predefinito usato per tutti i set di risultati creati tramite questo oggetto [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md).  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public java.lang.String getSelectMethod()  
```  
  
## <a name="return-value"></a>Valore restituito  
 Valore **String** contenente il tipo di cursore predefinito.  
  
## <a name="remarks"></a>Osservazioni  
 La proprietà selectMethod specifica il tipo di cursore predefinito che viene utilizzato per un set di risultati. Questa proprietà è utile in caso di set di risultati di grandi dimensioni e se non desidera archiviare tutto il set di risultati in memoria nel lato client. Impostando la proprietà su "cursor", è possibile creare un cursore sul lato server che può recuperare i blocchi di dati più piccoli in una sola volta. Se la proprietà selectMethod non è impostata, il metodo getSelectMethod restituisce il valore predefinito "direct".  
  
## <a name="see-also"></a>Vedere anche  
 [Membri di SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Classe SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
