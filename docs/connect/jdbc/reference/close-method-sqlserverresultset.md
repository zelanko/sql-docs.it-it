---
title: Metodo Close (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.close
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 8f3adf5b-874e-4cf2-b4ef-672dda42d77a
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: b5994cc3e2e8ed10759985571c195f783b95dac4
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/07/2019
ms.locfileid: "66800105"
---
# <a name="close-method-sqlserverresultset"></a>Metodo close (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Rilascia immediatamente le risorse JDBC e di database di questo oggetto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) anziché attendere che tale operazione venga eseguita al momento della chiusura automatica.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public void close()  
```  
  
## <a name="exceptions"></a>Eccezioni  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Questo metodo close viene specificato dal metodo close nell'interfaccia java.sql.ResultSet.  
  
 Un oggetto SQLServerResultSet viene automaticamente chiuso dall'oggetto [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) che lo ha generato quando tale oggetto SQLServerStatement viene chiuso, rieseguito o usato per recuperare il risultato successivo da una sequenza di più risultati. Un oggetto SQLServerResultSet viene anche automaticamente chiuso quando viene sottoposto a Garbage Collection.  
  
 Quando si esegue un'istruzione che genera un solo set di risultati forward-only di sola lettura di grandi dimensioni, si potrebbe essere interessati solo a qualche set di righe iniziale nel set di risultati restituito. In questo caso, l'applicazione potrebbe chiamare il metodo [cancel](../../../connect/jdbc/reference/cancel-method-sqlserverstatement.md) dell'oggetto istruzione associato prima di chiudere il set di risultati in modo da ridurre al minimo il tempo di elaborazione necessario per rimuovere le righe rimanenti non necessarie. Al momento di decidere se utilizzare o meno questa tecnica, si consiglia di tenere conto della necessità di mantenere un equilibrio tra il tempo di elaborazione salvato e il tempo e il round trip al server aggiuntivo necessari per annullare l'esecuzione.  
  
## <a name="see-also"></a>Vedere anche  
 [Membri di SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Classe SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
