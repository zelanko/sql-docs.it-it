---
title: Rinominare un database | Microsoft Docs
ms.custom: ''
ms.date: 10/02/2018
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- databases [SQL Server], renaming
- renaming databases
ms.assetid: 44c69d35-abcb-4da3-9370-5e0bc9a28496
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 1be87a50ad6e8815a9446ca22c2734a6e82b4745
ms.sourcegitcommit: cff8dd63959d7a45c5446cadf1f5d15ae08406d8
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/05/2019
ms.locfileid: "67583540"
---
# <a name="rename-a-database"></a>Rinominare un database

[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Questo argomento illustra come rinominare un database definito dall'utente in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] o Azure SQL Database usando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)]. Nel nome del database è possibile utilizzare qualsiasi carattere conforme alle regole per gli identificatori.  
  
## <a name="in-this-topic"></a>Contenuto dell'argomento
  
- Prima di iniziare:  
  
     [Limitazioni e restrizioni](#limitations-and-restrictions)  
  
     [Security](#security)  
  
- Per rinominare un database utilizzando:  
  
     [SQL Server Management Studio](#rename-a-database-using-sql-server-management-studio)  
  
     [Transact-SQL](#rename-a-database-using-transact-sql)  
  
- **Completamento:**  [Dopo la ridenominazione di un database](#backup-after-renaming-a-database)  

> [!NOTE]
> Per rinominare un database in Azure SQL Data Warehouse o Parallel Data Warehouse, usare l'istruzione [RENAME (Transact-SQL)](../../t-sql/statements/rename-transact-sql.md).
  
## <a name="before-you-begin"></a>Prima di iniziare
  
### <a name="limitations-and-restrictions"></a>Limitazioni e restrizioni  
  
- I database di sistema non possono essere rinominati.
- Non è possibile modificare il nome del database mentre altri utenti accedono al database. 
  - In SQL Server è possibile impostare un database in modalità utente singolo per chiudere le connessioni aperte. Per altre informazioni, vedere [Impostare un database in modalità utente singolo](../../relational-databases/databases/set-a-database-to-single-user-mode.md).
  - Nel database SQL di Azure è necessario assicurarsi che nessun altro utente abbia una connessione aperta al database da rinominare.
  
### <a name="security"></a>Security  
  
#### <a name="permissions"></a>Autorizzazioni

È richiesta l'autorizzazione ALTER per il database.  
  
## <a name="rename-a-database-using-sql-server-management-studio"></a>Rinominare un database con SQL Server Management Studio

Usare la procedura seguente per rinominare un database SQL Server o SQL di Azure usando SQL Server Management Studio.
  
1. In **Esplora oggetti** connettersi all'istanza del database SQL.  
  
2. Assicurarsi che non siano presenti connessioni aperte al database. Se si usa SQL Server, è possibile [impostare il database in modalità utente singolo](../../relational-databases/databases/set-a-database-to-single-user-mode.md) per chiudere le connessioni aperte e impedire ad altri utenti di connettersi mentre si modifica il nome del database.  
  
3. In Esplora oggetti espandere **Database** e fare clic con il pulsante destro del mouse sul database che si vuole rinominare, quindi scegliere **Rinomina**.  
  
4. Immettere il nuovo nome del database, quindi fare clic su **OK**.  

[!INCLUDE[freshInclude](../../includes/paragraph-content/fresh-note-steps-feedback.md)]

## <a name="rename-a-database-using-transact-sql"></a>Rinominare un database con Transact-SQL  
  
### <a name="to-rename-a-sql-server-database-by-placing-it-in-single-user-mode"></a>Per rinominare un database di SQL Server impostando la modalità utente singolo

Usare la procedura seguente per rinominare un database di SQL Server mediante T-SQL in SQL Server Management Studio, inclusi i passaggi per impostare la modalità utente singolo per il database e per tornare a impostare la modalità multiutente dopo la modifica del nome.
  
1. Connettersi al database `master` per l'istanza in uso.  
2. Aprire una finestra di query.  
3. Copiare e incollare l'esempio seguente nella finestra Query, quindi fare clic su **Esegui**. In questo esempio il nome del database `MyTestDatabase` viene modificato in `MyTestDatabaseCopy`.
  
   ```sql
   USE master;  
   GO  
   ALTER DATABASE MyTestDatabase SET SINGLE_USER WITH ROLLBACK IMMEDIATE
   GO
   ALTER DATABASE MyTestDatabase MODIFY NAME = MyTestDatabaseCopy ;
   GO  
   ALTER DATABASE MyTestDatabaseCopy SET MULTI_USER
   GO
   ```  

### <a name="to-rename-an-azure-sql-database-database"></a>Per rinominare un database SQL di Azure

Usare la procedura seguente per rinominare un database SQL di Azure usando T-SQL in SQL Server Management Studio.
  
1. Connettersi al database `master` per l'istanza in uso.  
2. Aprire una finestra di query.
3. Assicurarsi che nessuno stia usando il database.
4. Copiare e incollare l'esempio seguente nella finestra Query, quindi fare clic su **Esegui**. In questo esempio il nome del database `MyTestDatabase` viene modificato in `MyTestDatabaseCopy`.
  
   ```sql
   ALTER DATABASE MyTestDatabase MODIFY NAME = MyTestDatabaseCopy ;
   ```  

## <a name="backup-after-renaming-a-database"></a>Backup dopo la modifica del nome di un database  

Dopo la ridenominazione di un database in SQL Server, eseguire il backup del database `master`. Nel database SQL di Azure questo non è necessario, perché i backup vengono eseguiti automaticamente.  
  
## <a name="see-also"></a>Vedere anche

- [ALTER DATABASE (Transact-SQL)](../../t-sql/statements/alter-database-transact-sql.md)
- [Identificatori del database](../../relational-databases/databases/database-identifiers.md)  
