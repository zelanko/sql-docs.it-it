---
title: Metodo finalize (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.finalize
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 49bc879d-822b-42da-bc20-2394865f1f0f
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 7afb8728b92ac7460173950bf42e38f968e056af
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/31/2020
ms.locfileid: "67954573"
---
# <a name="finalize-method-sqlserverresultset"></a>Metodo finalize (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Chiude in modo esplicito questo oggetto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md).  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public void finalize()  
```  
  
## <a name="remarks"></a>Osservazioni  
 Chiude il set di risultati se tale operazione non viene eseguita dall'applicazione. Questo metodo esiste solo per la conformità alla specifica JDBC. Poiché Java Virtual Machine (JVM) non garantisce l'esecuzione di un finalizzatore, le applicazioni che non consentono la chiusura in modo esplicito dei relativi set di risultati possono ancora generare un deadlock su un'altra istruzione che sta utilizzando la stessa connessione ed è bloccata su una risorsa server comune, ad esempio i blocchi a livello di riga.  
  
## <a name="see-also"></a>Vedere anche  
 [Membri di SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Classe SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
