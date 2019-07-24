---
title: Metodo executeUpdate (java.lang.String, int[]) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerStatement.executeUpdate (java.lang.String, int[])
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 7b3d5b60-4285-4047-b13e-106754ca0d98
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 059f463c6a448c6ae2ab302542a50cde1f533db8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67954709"
---
# <a name="executeupdate-method-javalangstring-int"></a>Metodo executeUpdate (java.lang.String, int[])
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Esegue l'istruzione SQL specificata e segnala a [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] che le chiavi generate automaticamente indicate nella matrice specificata devono essere rese disponibili per il recupero.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public final int executeUpdate(java.lang.String sql,  
                               int[] columnIndexes)  
```  
  
#### <a name="parameters"></a>Parametri  
 *sql*  
  
 Valore **String** contenente un'istruzione SQL.  
  
 *columnIndexes*  
  
 Matrice di valori int che indicano gli indici di colonna delle chiavi generate automaticamente che devono essere resi disponibili.  
  
## <a name="return-value"></a>Valore restituito  
 Valore **int** che indica il numero di righe interessate oppure 0 se si usa un'istruzione DDL.  
  
## <a name="exceptions"></a>Eccezioni  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Questo metodo executeUpdate viene specificato dal metodo executeUpdate nell'interfaccia java.sql.Statement.  
  
 Se l'esecuzione di una stored procedure restituisce un conteggio di aggiornamenti maggiore di uno o genera più set di risultati, usare il metodo [execute](../../../connect/jdbc/reference/execute-method-sqlserverstatement.md) per eseguire la stored procedure.  
  
## <a name="see-also"></a>Vedere anche  
 [Metodo executeUpdate &#40;SQLServerStatement&#41;](../../../connect/jdbc/reference/executeupdate-method-sqlserverstatement.md)   
 [Membri di SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [Classe SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
