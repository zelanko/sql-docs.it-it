---
title: Creare vincoli univoci | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2020
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
f1_keywords:
- UNIQUE_TSQL
helpviewer_keywords:
- UNIQUE constraints [SQL Server], creating
- constraints [SQL Server], creating
- constraints [SQL Server], unique
ms.assetid: a86f9d6f-f242-43be-b65d-b3435b71b62a
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: d66d2e0f2ddacb06e5313c6f5a5ee11fefaf2640
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/30/2020
ms.locfileid: "79448192"
---
# <a name="create-unique-constraints"></a>Creare vincoli univoci
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  È possibile creare un vincolo univoco in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] utilizzando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)] per assicurare non vengano immessi valori duplicat nelle colonne specifiche che non partecipano in una chiave primaria. La creazione automatica di un vincolo univoco crea un indice univoco corrispondente.  
  
> [!NOTE]    
> Per informazioni sui vincoli univoci in Azure Synapse Analytics, vedere [Chiave primaria, chiave esterna e chiave univoca in Azure Synapse Analytics](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-table-constraints).
  
 **Contenuto dell'articolo**  
  
-   **Prima di iniziare:**  
  
     [Sicurezza](#Security)  
  
-   **Per creare un vincolo univoco:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="security"></a><a name="Security"></a> Sicurezza  
  
####  <a name="permissions"></a><a name="Permissions"></a> Autorizzazioni  
 È necessario disporre dell'autorizzazione ALTER per la tabella.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Utilizzo di SQL Server Management Studio  
  
#### <a name="to-create-a-unique-constraint"></a>Per creare un vincolo univoco  
  
1.  In **Esplora oggetti**fare clic con il pulsante destro del mouse sulla tabella nella quale aggiungere un vincolo univoco e scegliere **Progetta**.  
  
2.  Scegliere **Indici/chiavi** nel menu **Progettazione tabelle**.  
  
3.  Nella finestra di dialogo **Indici/chiavi** fare clic su **Aggiungi**.  
  
4.  Nella griglia in **Generale**fare clic su **Tipo** e selezionare **Chiave univoca** dall'elenco a discesa a destra della proprietà.  
  
5.  Scegliere **Salva**_nome tabella_ dal menu **File**.  

##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Uso di Transact-SQL  
  
#### <a name="to-create-a-unique-constraint"></a>Per creare un vincolo univoco  
  
1.  In **Esplora oggetti**connettersi a un'istanza del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Sulla barra Standard fare clic su **Nuova query**.  
  
3.  Copiare e incollare l'esempio seguente nella finestra Query, quindi fare clic su **Esegui**. Nell'esempio viene creata la tabella `TransactionHistoryArchive4` e un vincolo univoco sulla colonna `TransactionID`.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    CREATE TABLE Production.TransactionHistoryArchive4  
     (  
       TransactionID int NOT NULL,   
       CONSTRAINT AK_TransactionID UNIQUE(TransactionID)   
    );   
    GO  
  
    ```  
  
#### <a name="to-create-a-unique-constraint-on-an-existing-table"></a>Per creare un vincolo univoco in una tabella esistente  
  
1.  In **Esplora oggetti**connettersi a un'istanza del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Sulla barra Standard fare clic su **Nuova query**.  
  
3.  Copiare e incollare l'esempio seguente nella finestra Query, quindi fare clic su **Esegui**. Nell'esempio viene creato un vincolo univoco nelle colonne `PasswordHash` e `PasswordSalt` della tabella `Person.Password`.  
  
    ```  
    USE AdventureWorks2012;   
    GO  
    ALTER TABLE Person.Password   
    ADD CONSTRAINT AK_Password UNIQUE (PasswordHash, PasswordSalt);   
    GO  
  
    ```  
  
#### <a name="to-create-a-unique-constraint-in-an-new-table"></a>Per creare un vincolo univoco in una nuova tabella  
  
1.  In **Esplora oggetti**connettersi a un'istanza del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Sulla barra Standard fare clic su **Nuova query**.  
  
3.  Copiare e incollare l'esempio seguente nella finestra Query, quindi fare clic su **Esegui**. Nell'esempio viene creata una tabella e definito un vincolo univoco nelle colonne `TransactionID`.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    CREATE TABLE Production.TransactionHistoryArchive2  
    (  
       TransactionID int NOT NULL,  
       CONSTRAINT AK_TransactionID UNIQUE(TransactionID)  
    );  
    GO  
  
    ```  
  
     Per altre informazioni, vedere [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md), [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md) e [table_constraint &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-table-constraint-transact-sql.md).  
  
###  <a name="TsqlExample"></a>  
