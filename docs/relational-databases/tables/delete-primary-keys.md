---
title: Eliminare chiavi primarie | Microsoft Docs
ms.custom: ''
ms.date: 07/25/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- removing primary keys
- deleting primary keys
- primary keys [SQL Server], deleting
ms.assetid: c472e465-7bdd-4d74-8fc9-e47fca007ccb
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 87c1456360542797ed5fe80029236663f11c1aa1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62515895"
---
# <a name="delete-primary-keys"></a>Eliminazione di chiavi primarie
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  È possibile eliminare una chiave primaria in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] tramite [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)]. Quando viene eliminata la chiave primaria, viene eliminato l'indice corrispondente.  
  
 **Contenuto dell'articolo**  
  
-   **Prima di iniziare:**  
  
     [Security](#Security)  
  
-   **Per eliminare una chiave primaria:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="Security"></a> Sicurezza  
  
####  <a name="Permissions"></a> Autorizzazioni  
 È necessario disporre dell'autorizzazione ALTER per la tabella.  
  
##  <a name="SSMSProcedure"></a> Utilizzo di SQL Server Management Studio  
  
#### <a name="to-delete-a-primary-key-constraint-using-object-explorer"></a>Per eliminare un vincolo chiave primaria utilizzando Esplora oggetti  
  
1.  In Esplora oggetti, espandere la tabella contenente la chiave primaria, quindi espandere la cartella **Chiavi**.  
  
2.  Fare clic con il pulsante destro del mouse sulla chiave e scegliere **Elimina**.  
  
3.  Nella finestra di dialogo **Elimina oggetto** verificare che venga specificata la chiave corretta e fare clic su **OK**.  
  
#### <a name="to-delete-a-primary-key-constraint-using-table-designer"></a>Per eliminare un vincolo chiave primaria utilizzando Progettazione tabelle  
  
1.  In Esplora oggetti fare clic con il pulsante destro del mouse sulla tabella con la chiave primaria e scegliere **Progetta**.  
  
2.  Nella griglia della tabella fare clic con il pulsante destro del mouse sulla riga con la chiave primaria, quindi scegliere **Rimuovi chiave primaria** per attivare o disattivare l'impostazione.  
  
    > [!NOTE]  
    >  Per annullare questa operazione, chiudere la tabella senza salvare le modifiche. L'eliminazione di una chiave primaria non può essere annullata senza perdere tutte le altre modifiche apportate alla tabella.  
  
3.  Nel menu **File** scegliere **Salva**_table name_.  
  
##  <a name="TsqlProcedure"></a> Uso di Transact-SQL  
  
#### <a name="to-delete-a-primary-key-constraint"></a>Per eliminare un vincolo di chiave primaria  
  
1.  In **Esplora oggetti**connettersi a un'istanza del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Sulla barra Standard fare clic su **Nuova query**.  
  
3.  Copiare e incollare l'esempio seguente nella finestra Query, quindi fare clic su **Esegui**. Nell'esempio viene prima identificato il nome del vincolo di chiave primaria, quindi questo viene eliminato.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    -- Return the name of primary key.  
    SELECT name  
    FROM sys.key_constraints  
    WHERE type = 'PK' AND OBJECT_NAME(parent_object_id) = N'TransactionHistoryArchive';  
    GO  
    -- Delete the primary key constraint.  
    ALTER TABLE Production.TransactionHistoryArchive  
    DROP CONSTRAINT PK_TransactionHistoryArchive_TransactionID;   
    GO  
    ```  
  
 Per altre informazioni, vedere [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md) e [sys.key_constraints &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-key-constraints-transact-sql.md)  
  
###  <a name="TsqlExample"></a>  
