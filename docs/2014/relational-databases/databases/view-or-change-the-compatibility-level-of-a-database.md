---
title: Visualizzare o modificare il livello di compatibilità di un database | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- compatibility levels [SQL Server], viewing
- compatibility [SQL Server], databases
- compatibility levels [SQL Server], changing
ms.assetid: 579867ec-57cb-4cb8-af35-9688c1e9e15d
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 320b2e33ed1f36ab2e67625047897a5e8710b2c4
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52783753"
---
# <a name="view-or-change-the-compatibility-level-of-a-database"></a>Visualizzare o modificare il livello di compatibilità di un database
  In questo argomento si illustra come visualizzare o modificare il livello di compatibilità di un database in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] utilizzando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)]. Prima di modificare il livello di compatibilità di un database, è importante comprendere quale impatto avrà la modifica sulle applicazioni. Per altre informazioni, vedere [Livello di compatibilità ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-compatibility-level).  
  
 **Contenuto dell'argomento**  
  
-   **Prima di iniziare:**  
  
     [Sicurezza](#Security)  
  
-   **Per visualizzare o modificare il livello di compatibilità di un database utilizzando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="Security"></a> Sicurezza  
  
####  <a name="Permissions"></a> Permissions  
 È richiesta l'autorizzazione ALTER per il database.  
  
##  <a name="SSMSProcedure"></a> Utilizzo di SQL Server Management Studio  
  
#### <a name="to-view-or-change-the-compatibility-level-of-a-database"></a>Per visualizzare o modificare il livello di compatibilità di un database  
  
1.  Dopo essersi connessi all'istanza appropriata del [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], in Esplora oggetti fare clic sul nome del server.  
  
2.  Espandere **Database**e, a seconda del database, selezionare un database utente o espandere **Database di sistema** e selezionare un database di sistema.  
  
3.  Fare clic con il pulsante destro del mouse sul database, quindi scegliere **Proprietà**.  
  
     Verrà visualizzata la finestra di dialogo **Proprietà database** .  
  
4.  Nel riquadro **Selezione pagina** fare clic su **Opzioni**.  
  
     Il livello di compatibilità corrente viene visualizzato nella casella di riepilogo **Livello di compatibilità** .  
  
5.  Per modificare il livello di compatibilità, selezionare un'opzione diversa dall'elenco. Scegliere tra **SQL Server 2008 (100)**, **SQL Server 2012 (110)** o **SQL Server 2014 (120)**.  
  
##  <a name="TsqlProcedure"></a> Utilizzo di Transact-SQL  
  
#### <a name="to-view-the-compatibility-level-of-a-database"></a>Per visualizzare il livello di compatibilità di un database  
  
1.  Connettersi al [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Dalla barra Standard fare clic su **Nuova query**.  
  
3.  Copiare e incollare l'esempio seguente nella finestra delle query e fare clic su **Esegui**. In questo esempio viene restituito il livello di compatibilità del database [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] .  
  
```tsql  
USE AdventureWorks2012;  
GO  
SELECT compatibility_level  
FROM sys.databases WHERE name = 'AdventureWorks2012';  
GO  
  
```  
  
#### <a name="to-change-the-compatibility-level-of-a-database"></a>Per modificare il livello di compatibilità di un database  
  
1.  Connettersi al [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Dalla barra Standard fare clic su **Nuova query**.  
  
3.  Copiare e incollare l'esempio seguente nella finestra delle query e fare clic su **Esegui**. Questo esempio viene modificato il livello di compatibilità di [!INCLUDE[ssSampleDBobject](../../includes/sssql14-md.md)].  
  
```tsql  
ALTER DATABASE AdventureWorks2012  
SET COMPATIBILITY_LEVEL = 120;  
GO  
```  
  
  
