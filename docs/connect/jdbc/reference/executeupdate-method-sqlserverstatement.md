---
title: Metodo executeUpdate (SQLServerStatement) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerStatement.executeUpdate
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 10ae662a-ce3c-4b24-875c-5c2df319d93b
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 9052e28e66e6767a64b392978c6c52a42c24eaec
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/07/2019
ms.locfileid: "66804130"
---
# <a name="executeupdate-method-sqlserverstatement"></a>Metodo executeUpdate (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Esegue l'istruzione SQL specificata, che può essere un'istruzione INSERT, UPDATE o DELETE, oppure un'istruzione SQL che non restituisce nulla, ad esempio un'istruzione SQL DDL. A partire dalla versione 3.0 del driver JDBC per [!INCLUDE[msCoName](../../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], il metodo executeUpdate restituirà il numero corretto di righe aggiornate in un'operazione MERGE.  
  
## <a name="overload-list"></a>Elenco degli overload  
  
|nome|Descrizione|  
|----------|-----------------|  
|[executeUpdate (java.lang.String)](../../../connect/jdbc/reference/executeupdate-method-java-lang-string-sqlserverstatement.md)|Esegue l'istruzione SQL specificata, che può essere un'istruzione INSERT, UPDATE, DELETE o MERGE, oppure un'istruzione SQL che non restituisce nulla, ad esempio un'istruzione SQL DDL.|  
|[executeUpdate (java.lang.String, int)](../../../connect/jdbc/reference/executeupdate-method-java-lang-string-int.md)|Esegue l'istruzione SQL specificata e segnala a [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] con il flag specificato se le chiavi generate automaticamente prodotte da questo oggetto [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) devono essere rese disponibili per il recupero.|  
|[executeUpdate (java.lang.String, int&#91;&#93;)](../../../connect/jdbc/reference/executeupdate-method-java-lang-string.md)|Esegue l'istruzione SQL specificata e segnala al driver JDBC che le chiavi generate automaticamente indicate nella matrice specificata devono essere rese disponibili per il recupero.|  
|[executeUpdate (java.lang.String, java.lang.String&#91;&#93;)](../../../connect/jdbc/reference/executeupdate-method-java-lang-string-java-lang-string.md)|Esegue l'istruzione SQL specificata e segnala al driver JDBC che le chiavi generate automaticamente indicate nella matrice specificata devono essere rese disponibili per il recupero.|  
  
## <a name="see-also"></a>Vedere anche  
 [Membri di SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [Classe SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
