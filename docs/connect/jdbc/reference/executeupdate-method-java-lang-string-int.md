---
title: Metodo executeUpdate (java.lang.String, int) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerStatement.executeUpdate (java.lang.String, int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 4c52a20e-527e-4d14-9a5a-4cd195aac8ed
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 783058a764963637f2c91808424bac7bdd403c02
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/29/2020
ms.locfileid: "67954751"
---
# <a name="executeupdate-method-javalangstring-int"></a>Metodo executeUpdate (java.lang.String, int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Esegue l'istruzione SQL specificata e segnala ai [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] con il flag specificato se le chiavi generate automaticamente prodotte da questo oggetto [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) devono essere rese disponibili per il recupero.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public final int executeUpdate(java.lang.String sql,  
                               int flag)  
```  
  
#### <a name="parameters"></a>Parametri  
 *sql*  
  
 Valore **String** contenente un'istruzione SQL.  
  
 *flag*  
  
 Valore **int** che indica se le chiavi generate automaticamente devono essere rese disponibili. Deve essere una delle costanti seguenti:  
  
 RETURN_GENERATED_KEYS  
  
 NO_GENERATED_KEYS  
  
## <a name="return-value"></a>Valore restituito  
 Valore **int** che indica il numero di righe interessate oppure 0 se si usa un'istruzione DDL.  
  
## <a name="exceptions"></a>Eccezioni  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Osservazioni  
 Questo metodo executeUpdate viene specificato dal metodo executeUpdate nell'interfaccia java.sql.Statement.  
  
 Se l'esecuzione di una stored procedure restituisce un conteggio di aggiornamenti maggiore di uno o genera più set di risultati, usare il metodo [execute](../../../connect/jdbc/reference/execute-method-sqlserverstatement.md) per eseguire la stored procedure.  
  
## <a name="see-also"></a>Vedere anche  
 [Metodo executeUpdate &#40;SQLServerStatement&#41;](../../../connect/jdbc/reference/executeupdate-method-sqlserverstatement.md)   
 [Membri di SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [Classe SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
