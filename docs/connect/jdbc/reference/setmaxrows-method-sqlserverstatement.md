---
title: Metodo setMaxRows (SQLServerStatement) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerStatement.setMaxRows
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: cccc0667-589b-4655-8ea8-14ae8b2eb9dc
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 1ff4ab9e1db2415c92d42012d45b04c57ac30b67
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67973977"
---
# <a name="setmaxrows-method-sqlserverstatement"></a>Metodo setMaxRows (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Imposta sul numero specificato il numero massimo di righe che un oggetto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) può contenere.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public final void setMaxRows(int max)  
```  
  
#### <a name="parameters"></a>Parametri  
 *max*  
  
 Valore **int** che indica il numero massimo di righe oppure 0 in assenza di un limite.  
  
## <a name="exceptions"></a>Eccezioni  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Questo metodo setMaxRows viene specificato dal metodo setMaxRows nell'interfaccia java. SQL. Statement.  
  
 Questo metodo setMaxRows non ha effetto per i cursori scorrevoli dinamici. È consigliabile che l'applicazione utilizzi la sintassi SELECT TOP N SQL per limitare il numero di righe restituito da set di risultati di dimensioni potenzialmente grandi.  
  
 Quando viene chiamato il metodo setMaxRows, [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] esegue l'istruzione SET ROWCOUNT SQL durante l'esecuzione della query dell'applicazione. In questo modo il driver JDBC limita il numero massimo di righe interessate da tutte le istruzioni [!INCLUDE[tsql](../../../includes/tsql-md.md)] eseguite dalla query specifica e non solo il numero di righe restituite dalla query stessa. Se l'applicazione deve impostare un limite solo per l'oggetto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) di livello superiore, è consigliabile che usi la sintassi SELECT TOP N SQL nella query anziché il metodo setMaxRows.  
  
 Per altre informazioni sull'istruzione SET ROWCOUNT SQL, vedere l'argomento "[SET ROWCOUNT (Transact-SQL)](https://go.microsoft.com/fwlink/?LinkId=139522)" nella documentazione online di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
## <a name="see-also"></a>Vedere anche  
 [Membri di SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [Classe SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
