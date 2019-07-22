---
title: Esecuzione di operazioni batch | Microsoft Docs
ms.custom: ''
ms.date: 07/11/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 1a576d95-7da6-4b7b-8b32-59e5b4d354c4
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 244c20b2fb7721d117557581068791e1a2d99d14
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67956229"
---
# <a name="performing-batch-operations"></a>Esecuzione di operazioni batch
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Per garantire prestazioni migliori quando si eseguono più aggiornamenti di un database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] consente di inviare più aggiornamenti come singola unità di lavoro, denominata anche batch.  
  
 Le classi [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md), [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) e [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) possono essere usate tutte per inviare aggiornamenti in blocco. Il metodo [addBatch](../../connect/jdbc/reference/addbatch-method-sqlserverpreparedstatement.md) viene usato per aggiungere un comando. Il metodo [clearBatch](../../connect/jdbc/reference/clearbatch-method-sqlserverpreparedstatement.md) viene usato per cancellare l'elenco dei comandi. Il metodo [executeBatch](../../connect/jdbc/reference/executebatch-method-sqlserverstatement.md) viene usato per inviare tutti i comandi per l'elaborazione. Possono essere eseguite come parte di un batch solo le istruzioni DDL (Data Definition Language) e DML (Data Manipulation Language) che restituiscono un semplice conteggio di aggiornamento.  
  
 Il metodo executeBatch restituisce una matrice di valori **int** che corrispondono al conteggio aggiornamenti di ogni comando. Se uno dei comandi ha esito negativo, viene generata un'eccezione BatchUpdateException ed è necessario usare il metodo getUpdateCounts della classe BatchUpdateException per recuperare la matrice del conteggio degli aggiornamenti. Se un comando non riesce, il driver continua a elaborare i comandi rimanenti. Tuttavia, se un comando contiene un errore di sintassi sarà impossibile eseguire le istruzioni del batch.  
  
> [!NOTE]  
>  Se non è necessario usare i conteggi degli aggiornamenti, è possibile eseguire prima un'istruzione SET NOCOUNT ON in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Il traffico di rete verrà ridotto e aumenteranno le prestazioni dell'applicazione.  
  
 Come esempio viene creata la tabella seguente nel database di esempio [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)]:  
  
```sql
CREATE TABLE TestTable   
   (Col1 int IDENTITY,   
    Col2 varchar(50),   
    Col3 int);  
```  
  
 Nell'esempio seguente viene passata alla funzione una connessione aperta al database di esempio [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)], il metodo addBatch viene usato per creare le istruzioni da eseguire e viene eseguita la chiamata al metodo executeBatch per inviare il batch al database.  
  
```java
public static void executeBatchUpdate(Connection con) {  
   try {  
      Statement stmt = con.createStatement();  
      stmt.addBatch("INSERT INTO TestTable (Col2, Col3) VALUES ('X', 100)");  
      stmt.addBatch("INSERT INTO TestTable (Col2, Col3) VALUES ('Y', 200)");  
      stmt.addBatch("INSERT INTO TestTable (Col2, Col3) VALUES ('Z', 300)");  
      int[] updateCounts = stmt.executeBatch();  
      stmt.close();  
   }  
   catch (Exception e) {  
      e.printStackTrace();  
   }  
}  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Uso delle istruzioni con il driver JDBC](../../connect/jdbc/using-statements-with-the-jdbc-driver.md)  
  
  
