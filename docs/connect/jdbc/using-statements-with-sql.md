---
title: Uso di istruzioni con SQL | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: fe28f48a-e1bc-48ff-a5e7-c24cd6e5ecc7
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 17e6253d0ff1f4fa9a26d97772fb9f7ff2890221
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/08/2020
ms.locfileid: "80923980"
---
# <a name="using-statements-with-sql"></a>Uso di istruzioni SQL

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Quando si gestiscono dati in un database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tramite [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] e istruzioni SQL inline, è possibile usare diverse classi. in base al tipo di istruzione SQL che si desidera eseguire.  
  
Se l'istruzione SQL non contiene parametri IN, usare la classe [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md); se, invece, contiene parametri IN, usare la classe [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md).  
  
> [!NOTE]  
> Se è necessario usare istruzioni SQL che contengono sia parametri IN che OUT, è necessario implementarle come stored procedure e chiamarle usando la classe [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md). Per altre informazioni sull'uso delle stored procedure, vedere [Uso delle istruzioni con le stored procedure](../../connect/jdbc/using-statements-with-stored-procedures.md).  
  
Nelle sezioni seguenti sono descritti i diversi scenari di utilizzo di dati in un database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mediante istruzioni SQL.  

## <a name="in-this-section"></a>Contenuto della sezione  

| Argomento                                                                                                                        | Descrizione                                                       |
| ---------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------- |
| [Uso di un'istruzione SQL senza parametri](../../connect/jdbc/using-an-sql-statement-with-no-parameters.md)                 | Descrive come utilizzare istruzioni SQL che non contengono parametri.   |
| [Uso di istruzioni SQL con parametri](../../connect/jdbc/using-an-sql-statement-with-parameters.md)                       | Descrive come utilizzare istruzioni SQL che contengono parametri.      |
| [Uso di un'istruzione SQL per modificare gli oggetti di database](../../connect/jdbc/using-an-sql-statement-to-modify-database-objects.md) | Descrive come utilizzare istruzioni SQL per modificare gli oggetti di database.   |
| [Uso di un'istruzione SQL per modificare i dati](../../connect/jdbc/using-an-sql-statement-to-modify-data.md)                         | Descrive come utilizzare istruzioni SQL per modificare i dati in un database. |
  
## <a name="see-also"></a>Vedere anche

[Uso delle istruzioni con il driver JDBC](../../connect/jdbc/using-statements-with-the-jdbc-driver.md)  
