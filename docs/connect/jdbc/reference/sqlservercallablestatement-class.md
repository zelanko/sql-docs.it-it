---
title: SQLServerCallableStatement (classe) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 30710a63-c05d-47d9-9cf9-c087a1c76373
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 637b56c7f64d35501be0efef30e8f2a055b5be4b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67971909"
---
# <a name="sqlservercallablestatement-class"></a>Classe SQLServerCallableStatement
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Consente di specificare il nome della stored procedure da chiamare insieme ai parametri di input e di output. Questa classe fornisce anche la possibilità di recuperare il valore di stato restituito con la sintassi ? = call( ?, ..).  
  
 **Pacchetto:** com.microsoft.sqlserver.jdbc  
  
 **Implementa:** [ISQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
 **Estende:** [SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public final class SQLServerCallableStatement  
```  
  
## <a name="remarks"></a>Remarks  
 SQLServerCallableStatement consente di specificare il nome della stored procedure da chiamare insieme ai parametri di input e di output. SQLServerCallableStatement offre inoltre la possibilità di recuperare il valore di stato restituito con `? = call( ?, ..)` la sintassi.  
  
 Questa classe supporta l'annullamento del wrapping alla classe SQLServerCallableStatement, l'interfaccia ISQLServerCallableStatement, l'interfaccia java. SQL. CallableStatement e le classi e le interfacce supportate da SQLServerPreparedStatement per l'annullamento del wrapping. Per ulteriori informazioni, vedere [wrapper e interfacce](../../../connect/jdbc/wrappers-and-interfaces.md).  
  
 Quando uno dei metodi set SQLServerCallableStatement viene chiamato per un tipo, se tale tipo è in conflitto con il tipo specificato con [registerOutParameter](../../../connect/jdbc/reference/registeroutparameter-method-sqlservercallablestatement.md), viene utilizzato il tipo specificato dall'ultimo metodo set SQLServerCallableStatement. Questo comportamento, tuttavia, può provocare errori di conversione di tipi di dati incompatibili. Se un metodo set SQLServerCallableStatement non viene chiamato, viene usato il tipo specificato tramite la prima chiamata di [registerOutParameter](../../../connect/jdbc/reference/registeroutparameter-method-sqlservercallablestatement.md).  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] JDBC Driver 3.0 è conforme all'indicazione JDBC 4.0, per cui un set di risultati e i conteggi degli aggiornamenti devono essere recuperati prima del recupero dei parametri OUT. Se i parametri OUT vengono recuperati prima dell'elaborazione completa del set di risultati e dei conteggi aggiornamenti, qualsiasi set di risultati o conteggio aggiornamenti non elaborato andrà perduto.  
  
## <a name="see-also"></a>Vedere anche  
 [Membri di SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [Informazioni di riferimento sull'API del driver JDBC](../../../connect/jdbc/reference/jdbc-driver-api-reference.md)  
  
  
