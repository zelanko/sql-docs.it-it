---
title: Uso di una stored procedure con parametri di output | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 1c006f27-7e99-43d5-974c-7b782659290c
author: MightyPen
ms.author: genemi
ms.openlocfilehash: efafaa709666620e7237f2481c392aba25dfd5f8
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/29/2020
ms.locfileid: "69026830"
---
# <a name="using-a-stored-procedure-with-output-parameters"></a>Uso di una stored procedure con parametri di output

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Una stored procedure [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] che è possibile chiamare è una procedura che restituisce uno o più parametri OUT, ovvero parametri usati dalla stored procedure per restituire i dati all'applicazione chiamante. [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] rende disponibile la classe [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md), che è possibile usare per chiamare stored procedure di questo tipo ed elaborare i dati restituiti da queste.

Quando si chiama questo tipo di stored procedure usando il driver JDBC, è necessario usare la sequenza di escape SQL `call` insieme al metodo [prepareCall](../../connect/jdbc/reference/preparecall-method-sqlserverconnection.md) della classe [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md). La sintassi della sequenza di escape `call` con parametri OUT è la seguente:

`{call procedure-name[([parameter][,[parameter]]...)]}`

> [!NOTE]  
> Per altre informazioni sulle sequenze di escape SQL, vedere [Uso delle sequenze di escape SQL](../../connect/jdbc/using-sql-escape-sequences.md).

Quando si costruisce la sequenza di escape `call`, specificare i parametri OUT usando il carattere ? (punto interrogativo), che funge da segnaposto per i valori di parametro che verranno restituiti dalla stored procedure. Per specificare il valore di un parametro OUT, è necessario specificare il tipo di dati di ogni parametro usando il metodo [registerOutParameter](../../connect/jdbc/reference/registeroutparameter-method-sqlservercallablestatement.md) della classe SQLServerCallableStatement prima di eseguire la stored procedure.

Il valore specificato per il parametro OUT nel metodo registerOutParameter deve essere uno dei tipi di dati JDBC presenti in java.sql.Types, che a sua volta corrisponde a uno dei tipi di dati di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nativi. Per altre informazioni sui tipi di dati JDBC e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vedere [Informazioni sui tipi di dati del driver JDBC](../../connect/jdbc/understanding-the-jdbc-driver-data-types.md).

Quando si passa un valore al metodo registerOutParameter per un parametro OUT, è necessario specificare non solo il tipo di dati da usare per il parametro, ma anche la posizione ordinale o il nome del parametro nella stored procedure. Ad esempio, se la stored procedure contiene un unico parametro OUT, il valore ordinale sarà 1. Se la stored procedure contiene due parametri, il primo valore ordinale sarà 1 e il secondo sarà 2.

> [!NOTE]  
> Il driver JDBC non supporta l'uso dei tipi di dati di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] CURSOR, SQLVARIANT, TABLE e TIMESTAMP come parametri OUT.

Come esempio, viene creata la seguente stored procedure nel database di esempio [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)]:

```sql
CREATE PROCEDURE GetImmediateManager  
   @employeeID INT,  
   @managerID INT OUTPUT  
AS  
BEGIN  
   SELECT @managerID = ManagerID
   FROM HumanResources.Employee
   WHERE EmployeeID = @employeeID  
END
```

Questa stored procedure restituisce un unico parametro OUT (managerID), che è rappresentato da un numero intero, in base al parametro IN specificato (employeeID), anch'esso rappresentato da un numero intero. Il valore restituito nel parametro OUT è ManagerID, a sua volta basato sul valore EmployeeID contenuto nella tabella HumanResources.Employee.

Nell'esempio seguente viene passata alla funzione una connessione aperta al database di esempio [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] e viene usato il metodo [execute](../../connect/jdbc/reference/execute-method-sqlserverstatement.md) per la chiamata alla stored procedure GetImmediateManager:

```java
public static void executeStoredProcedure(Connection con) throws SQLException {  
    try(CallableStatement cstmt = con.prepareCall("{call dbo.GetImmediateManager(?, ?)}");) {  
        cstmt.setInt(1, 5);  
        cstmt.registerOutParameter(2, java.sql.Types.INTEGER);  
        cstmt.execute();  
        System.out.println("MANAGER ID: " + cstmt.getInt(2));  
    }  
}
```

In questo esempio vengono utilizzate le posizioni ordinali per identificare i parametri. In alternativa, è possibile identificare un parametro utilizzando il relativo nome anziché la posizione ordinale. Nell'esempio di codice seguente viene modificato l'esempio precedente per illustrare l'utilizzo di parametri denominati in un'applicazione Java. Si noti che i nomi dei parametri corrispondono ai nomi dei parametri nella definizione della stored procedure:

```java
public static void executeStoredProcedure(Connection con) throws SQLException {  
    try(CallableStatement cstmt = con.prepareCall("{call dbo.GetImmediateManager(?, ?)}"); ) {  
        cstmt.setInt("employeeID", 5);  
        cstmt.registerOutParameter("managerID", java.sql.Types.INTEGER);  
        cstmt.execute();  
        System.out.println("MANAGER ID: " + cstmt.getInt("managerID"));  
    }  
}
```

> [!NOTE]  
> In questi esempi viene usato il metodo execute della classe SQLServerCallableStatement per eseguire la stored procedure. in quanto la stored procedure non ha restituito alcun set di risultati. In caso contrario, si userebbe il metodo [executeQuery](../../connect/jdbc/reference/executequery-method-sqlserverstatement.md).

Le stored procedure possono restituire conteggi aggiornamenti e più set di risultati. [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] è conforme alla specifica JDBC 3.0, che stabilisce che prima di recuperare i parametri OUT devono essere recuperati più set di risultati e conteggi di aggiornamento. Questo significa che l'applicazione deve recuperare tutti i conteggi di aggiornamento e gli oggetti ResultSet prima di recuperare i parametri OUT usando i metodi CallableStatement.getter. In caso contrario, gli oggetti ResultSet e i conteggi di aggiornamento non ancora recuperati andranno persi quando vengono recuperati i parametri OUT. Per altre informazioni sui conteggi di aggiornamento e l'uso di più set di risultati, vedere [Uso di una stored procedure con i conteggi di aggiornamento](../../connect/jdbc/using-a-stored-procedure-with-an-update-count.md) e [Uso di più set di risultati](../../connect/jdbc/using-multiple-result-sets.md).

## <a name="see-also"></a>Vedere anche

[Uso delle istruzioni con le stored procedure](../../connect/jdbc/using-statements-with-stored-procedures.md)
