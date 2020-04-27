---
title: Rinominare un database | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
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
ms.openlocfilehash: f014cb37c6c28a0c9a91bd811b9e94d734167e1e
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "62916771"
---
# <a name="rename-a-database"></a>Rinominare un database
  In questo argomento si illustra come rinominare un database definito dall'utente in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] utilizzando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)]. Nel nome del database è possibile utilizzare qualsiasi carattere conforme alle regole per gli identificatori.  
  
 **Contenuto dell'articolo**  
  
-   **Prima di iniziare:**  
  
     [Limitazioni e restrizioni](#Restrictions)  
  
     [Sicurezza](#Security)  
  
-   **Per rinominare un database utilizzando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   **Completamento:**  [Dopo la ridenominazione di un database](#FollowUp)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> Limitazioni e restrizioni  
  
-   I database di sistema non possono essere rinominati.  
  
###  <a name="security"></a><a name="Security"></a> Sicurezza  
  
####  <a name="permissions"></a><a name="Permissions"></a> Autorizzazioni  
 È richiesta l'autorizzazione ALTER per il database.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Utilizzo di SQL Server Management Studio  
  
#### <a name="to-rename-a-database"></a>Per rinominare un database  
  
1.  In **Esplora oggetti**connettersi a un'istanza del, quindi [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]espandere l'istanza.  
  
2.  Verificare che nessuno stia usando il database e quindi [impostare il database in modalità utente singolo](set-a-database-to-single-user-mode.md).  
  
3.  Espandere **Database**, fare clic con il pulsante destro del mouse sul database che si vuole rinominare, quindi scegliere **Rinomina**.  
  
4.  Immettere il nuovo nome del database, quindi fare clic su **OK**.  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Uso di Transact-SQL  
  
#### <a name="to-rename-a-database"></a>Per rinominare un database  
  
1.  Connettersi al [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Dalla barra Standard fare clic su **Nuova query**.  
  
3.  Copiare e incollare l'esempio seguente nella finestra Query, quindi fare clic su **Esegui**. In questo esempio il nome del database `AdventureWorks2012` viene modificato in `Northwind`.  
  
```sql  
USE master;  
GO  
ALTER DATABASE AdventureWorks2012  
Modify Name = Northwind ;  
GO  
```  
  
###  <a name="TsqlExample"></a>   
##  <a name="follow-up-after-renaming-a-database"></a><a name="FollowUp"></a> Completamento: Dopo la rinomina di un database  
 Dopo aver rinominato un database, eseguire il backup del database **master** .  
  
## <a name="see-also"></a>Vedi anche  
 [ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql)   
 [Identificatori del database](database-identifiers.md)  
  
  
