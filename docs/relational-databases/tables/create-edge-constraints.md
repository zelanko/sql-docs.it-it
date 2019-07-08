---
title: Creare vincoli di arco | Microsoft Docs
ms.custom: ''
ms.date: 09/11/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- edge constraints [SQL Server]
- CONNECTION constraints
- edge constraints [Azure SQL Database]
- graph edge constraints
- SQL Graph
ms.assetid: ''
author: shkale-msft
ms.author: shkale
manager: craigg
monikerRange: '>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 97ad249695c4fbe0fd79a23a5493d998fbaf5191
ms.sourcegitcommit: cff8dd63959d7a45c5446cadf1f5d15ae08406d8
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/05/2019
ms.locfileid: "67582324"
---
# <a name="create-edge-constraints"></a>Creare vincoli di arco
[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx.md](../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

   È possibile definire un vincolo di arco in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tramite [!INCLUDE[tsql](../../includes/tsql-md.md)]. 
  
##  <a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="Restrictions"></a> Limitazioni e restrizioni  
  
-   È possibile definire un vincolo di arco solo in una tabella archi del grafo. 
  
##  <a name="TsqlProcedure"></a> Uso di Transact-SQL  

### <a name="to-create-an-edge-constraint-on-a-new-edge-table"></a>Per creare un vincolo di arco in una nuova tabella archi
  
1.  In **Esplora oggetti**connettersi a un'istanza del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Sulla barra Standard fare clic su **Nuova query**.  
  
3.  Copiare e incollare l'esempio seguente nella finestra Query, quindi fare clic su **Esegui**. L'esempio crea un vincolo di arco nella tabella archi **bought**.  

[!INCLUDE[freshInclude](../../includes/paragraph-content/fresh-note-steps-feedback.md)]

 ```sql
 USE TEMPDB
 GO
 -- CREATE node and edge tables
 CREATE TABLE Customer
    (
        ID INTEGER PRIMARY KEY, 
        CustomerName VARCHAR(100)
    )
 AS NODE
 GO

 CREATE TABLE Product 
  (
        ID INTEGER PRIMARY KEY, 
        ProductName VARCHAR(100)
  ) AS NODE
 GO

 CREATE TABLE bought
    (
        PurchaseCount INT,
        CONSTRAINT EC_BOUGHT CONNECTION (Customer TO Product)
    )
 AS EDGE
 GO
 ```  

### <a name="to-add-edge-constraint-to-an-existing-edge-table"></a>Per aggiungere un vincolo di arco a una tabella archi esistente. 
  
1.  In **Esplora oggetti**connettersi a un'istanza del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Sulla barra Standard fare clic su **Nuova query**.  
  
3.  Copiare e incollare l'esempio seguente nella finestra Query, quindi fare clic su **Esegui**. L'esempio usa ALTER TABLE per aggiungere un vincolo di arco nella tabella archi **bought**.
  
 ```sql
 USE TEMPDB
 GO
 -- CREATE node and edge tables
 CREATE TABLE Customer
    (
        ID INTEGER PRIMARY KEY, 
        CustomerName VARCHAR(100)
    )
 AS NODE
 GO

 CREATE TABLE Product 
  (
        ID INTEGER PRIMARY KEY, 
        ProductName VARCHAR(100)
  ) AS NODE
 GO

 CREATE TABLE bought
    (
        PurchaseCount INT
    )
 AS EDGE
 GO

 ALTER TABLE bought ADD CONSTRAINT EC_BOUGHT1 CONNECTION (Customer TO Product)
 GO
 ```  

### <a name="creating-a-new-edge-constraint-on-existing-edge-table-with-additional-edge-constraint-clauses"></a>Creazione di un nuovo vincolo di arco in una tabella archi esistente, con clausole aggiuntive per il vincolo di arco.
1.  In **Esplora oggetti**connettersi a un'istanza del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Sulla barra Standard fare clic su **Nuova query**.  
  
3.  Copiare e incollare l'esempio seguente nella finestra Query, quindi fare clic su **Esegui**. L'esempio usa ALTER TABLE per aggiungere un vincolo di arco con clausole aggiuntive per il vincolo di arco nella tabella archi **bought**.
  
 ```sql
 USE TEMPDB
 GO
 -- CREATE node and edge tables
 CREATE TABLE Customer
    (
        ID INTEGER PRIMARY KEY, 
        CustomerName VARCHAR(100)
    )
 AS NODE
 GO

 CREATE TABLE Supplier
    (
        ID INTEGER PRIMARY KEY, 
        SupplierName VARCHAR(100)
    )
 AS NODE
 GO

 CREATE TABLE Product 
  (
        ID INTEGER PRIMARY KEY, 
        ProductName VARCHAR(100)
  ) AS NODE
 GO

 CREATE TABLE bought
    (
        PurchaseCount INT,
        CONSTRAINT EC_BOUGHT CONNECTION (Customer TO Product)
    )
 AS EDGE
 GO

 -- Drop the existing edge constraint first and then create a new one.
 ALTER TABLE bought DROP CONSTRAINT EC_BOUGHT
 GO

 -- User ALTER TABLE to create a new edge constraint.
 ALTER TABLE bought ADD CONSTRAINT EC_BOUGHT1 CONNECTION (Customer TO Product, Supplier TO Product)
 GO
 ```  
 Si noti che sono presenti due clausole per il vincolo di arco nel vincolo *EC_BOUGHT1*, una che connette **Customer** a **Product** e l'altra che connette **Supplier**  a **Product**. Entrambe queste clausole vengono applicate in disgiunzione. Vale a dire, un determinato arco deve soddisfare una delle due clausole per essere consentito nella tabella archi. 



### <a name="creating-a-new-edge-constraint-on-existing-edge-table-with-new-edge-constraint-clause"></a>Creazione di un nuovo vincolo di arco in una tabella archi esistente, con una nuova clausola per il vincolo di arco.
1.  In **Esplora oggetti**connettersi a un'istanza del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Sulla barra Standard fare clic su **Nuova query**.  
  
3.  Copiare e incollare l'esempio seguente nella finestra Query, quindi fare clic su **Esegui**. L'esempio usa ALTER TABLE per aggiungere un vincolo di arco con una nuova clausola per il vincolo di arco nella tabella archi **bought**.
  
 ```sql
 USE TEMPDB
 GO
 -- CREATE node and edge tables
 CREATE TABLE Customer
    (
        ID INTEGER PRIMARY KEY, 
        CustomerName VARCHAR(100)
    )
 AS NODE
 GO

 CREATE TABLE Supplier
    (
        ID INTEGER PRIMARY KEY, 
        SupplierName VARCHAR(100)
    )
 AS NODE
 GO

 CREATE TABLE Product 
  (
        ID INTEGER PRIMARY KEY, 
        ProductName VARCHAR(100)
  ) AS NODE
 GO

 CREATE TABLE bought
    (
        PurchaseCount INT,
        CONSTRAINT EC_BOUGHT CONNECTION (Customer TO Product)
    )
 AS EDGE
 GO

 ALTER TABLE bought ADD CONSTRAINT EC_BOUGHT1 CONNECTION (Supplier TO Product)
 GO
 ```  

 In questo esempio sono stati creati due vincoli di arco separati sulla tabella archi **bought**: *EC_BOUGHT* e *EC_BOUGHT1*. Entrambi questi vincoli di arco hanno clausole diverse per il vincolo di arco. Se una tabella archi ha più di un vincolo di arco, un determinato arco deve soddisfare **TUTTI** i vincoli di arco per essere consentito nella tabella archi. Dato che nessun arco potrà soddisfare entrambi i vincoli *EC_BOUGHT* e *EC_BOUGHT1* in questo esempio, la tabella archi **bought** deve rimanere vuota. 

 Affinché gli inserimenti abbiano esito positivo in questa tabella archi, è necessario eliminare uno dei vincoli di arco oppure devono essere eliminati entrambi e occorre creare un nuovo vincolo di arco che include entrambe le clausole. 

 ```sql
 USE TEMPDB
 GO
 -- Drop the existing edge constraint first and then create a new one.
 ALTER TABLE bought DROP CONSTRAINT EC_BOUGHT
 GO
 
 ALTER TABLE bought DROP CONSTRAINT EC_BOUGHT1
 GO
 
 ALTER TABLE bought ADD CONSTRAINT EC_BOUGHT_NEW CONNECTION (Customer TO Product, Supplier TO Product)
 GO
 ```  

 Per essere consentito nella tabella archi **bought**, un determinato arco deve soddisfare una delle clausole nel vincolo *EC_BOUGHT_NEW*. Sarà quindi consentito qualsiasi arco che tenta di connettere un nodo **Customer** valido al nodo **Product** o un nodo **Supplier** al nodo **Product**. 
