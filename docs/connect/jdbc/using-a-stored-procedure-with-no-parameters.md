---
title: Uso di una stored procedure senza parametri | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: e9470a6d-a758-4c56-96ec-7b37139e36a7
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 01f59f44d42af1d0880df48b043080525d9821ee
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 08/14/2019
ms.locfileid: "69027026"
---
# <a name="using-a-stored-procedure-with-no-parameters"></a>Uso di una stored procedure senza parametri

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Il tipo più semplice di stored procedure di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] che è possibile chiamare è quello che non contiene parametri e restituisce un solo set di risultati. In [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] è disponibile la classe [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) che è possibile usare per chiamare questo tipo di stored procedure ed elaborare i dati restituiti.

Quando si usa il driver JDBC per chiamare una stored procedure senza parametri, è necessario usare la sequenza di escape SQL `call`. La sintassi della sequenza di escape `call` senza parametri è la seguente:

`{call procedure-name}`

> [!NOTE]  
> Per ulteriori informazioni sulle sequenze di escape SQL, vedere [utilizzo di sequenze di escape SQL](../../connect/jdbc/using-sql-escape-sequences.md).

Come esempio, viene creata la seguente stored procedure nel database di esempio [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)]:

```sql
CREATE PROCEDURE GetContactFormalNames
AS  
BEGIN  
   SELECT TOP 10 Title + ' ' + FirstName + ' ' + LastName AS FormalName
   FROM Person.Contact  
END  
```

Questa stored procedure restituisce un solo set di risultati contenente una colonna di dati che corrispondono a una combinazione di titolo, nome e cognome dei primi 10 contatti presenti nella tabella Person.Contact.

Nell'esempio seguente viene passata alla funzione una connessione aperta al database di esempio [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] e viene usato il metodo [executeQuery](../../connect/jdbc/reference/executequery-method-sqlserverstatement.md) per chiamare la stored procedure GetContactFormalNames.

```java
public static void executeSprocNoParams(Connection con) throws SQLException {  
    try(Statement stmt = con.createStatement();) {  

        ResultSet rs = stmt.executeQuery("{call dbo.GetContactFormalNames}");  
        while (rs.next()) {  
            System.out.println(rs.getString("FormalName"));  
        }  
    }  
}
```

## <a name="see-also"></a>Vedere anche

[Uso delle istruzioni con le stored procedure](../../connect/jdbc/using-statements-with-stored-procedures.md)
