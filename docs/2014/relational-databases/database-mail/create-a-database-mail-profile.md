---
title: Creare un profilo di Posta elettronica database | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- Database Mail [SQL Server], public profiles
- profiles [SQL Server], Database Mail
- public profiles [Database Mail]
ms.assetid: 58ae749d-6ada-4f9c-bf00-de7c7a992a2d
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 55eab0bbfacdde17ff69dd36a0641561695bc14d
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "62872207"
---
# <a name="create-a-database-mail-profile"></a>Creare un profilo di Posta elettronica database
  Per creare profili pubblici e privati di Posta elettronica database, è possibile utilizzare **Configurazione guidata posta elettronica database** o [!INCLUDE[tsql](../../includes/tsql-md.md)] .  
  

  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="prerequisites"></a><a name="Prerequisites"></a> Prerequisiti  
 Creare uno o più account di Posta elettronica database per il profilo. Per altre informazioni sulla creazione di account di Posta elettronica database, vedere [Creare un account di Posta elettronica database](create-a-database-mail-account.md).  
  
###  <a name="security"></a><a name="Security"></a> Sicurezza  
 Gli utenti in grado di accedere al database **msdb** possono usare un profilo pubblico per inviare messaggi di posta elettronica. Un profilo privato può essere utilizzato da un utente o da un ruolo. Concedendo ai ruoli l'accesso ai profili viene creata un'architettura gestita in modo più semplice. Solo un membro del ruolo **DatabaseMailUserRole** del database **msdb** con accesso ad almeno un profilo di Posta elettronica database può inviare messaggi di posta elettronica.  
  
####  <a name="permissions"></a><a name="Permissions"></a> Autorizzazioni  
 Per creare gli account dei profili ed eseguire le stored procedure è necessario che l'utente sia un membro del ruolo predefinito del server sysadmin.  
  

  
##  <a name="using-database-mail-configuration-wizard"></a><a name="SSMSProcedure"></a> Utilizzo della Configurazione guidata Posta elettronica database  
 **Per creare un profilo di Posta elettronica database**  
  
-   In Esplora oggetti, connettersi all'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] su cui si desidera configurare Posta elettronica database ed espandere l'albero di server.  
  
-   Espandere il nodo **Gestione**  
  
-   Fare doppio clic su Posta elettronica database per aprire la Configurazione guidata posta elettronica database.  
  
-   Nella pagina **Selezione attività di configurazione** selezionare l'opzione **Gestisci account e profili posta elettronica database** e fare clic su **Avanti**.  
  
-   Nella pagina **Gestione profili e account** selezionare l'opzione **Crea un nuovo profilo** e fare clic su **Avanti**.  
  
-   Nella pagina **Nuovo profilo** specificare il nome e la descrizione del profilo e aggiungere gli account da includere nel profilo, quindi fare clic su **Avanti**.  
  
-   Per completare la creazione del nuovo profilo, rivedere le azioni da eseguire nella pagina **Completamento procedura guidata** quindi fare clic su **Fine** .  
  
-   **Per configurare un profilo privato di Posta elettronica database:**  
  
    -   Aprire la configurazione guidata posta elettronica database.  
  
    -   Nella pagina **Selezione attività di configurazione** selezionare l'opzione **Gestisci account e profili di Posta elettronica database** e fare clic su **Avanti**.  
  
    -   Nella pagina **Gestione profili e account** selezionare l'opzione **Gestione sicurezza profilo** e fare clic su **Avanti**.  
  
    -   Nella scheda **Profili privati** selezionare la casella di controllo per il profilo che si desidera configurare e fare clic su **Avanti**.  
  
    -   Per completare la configurazione del profilo, rivedere le azioni da eseguire nella pagina **Completamento procedura guidata** quindi fare clic su **Fine** .  
  
-   **Per configurare un profilo pubblico di Posta elettronica database:**  
  
    -   Aprire la configurazione guidata posta elettronica database.  
  
    -   Nella pagina **Selezione attività di configurazione** selezionare l'opzione **Gestisci account e profili di Posta elettronica database** e fare clic su **Avanti**.  
  
    -   Nella pagina **Gestione profili e account** selezionare l'opzione **Gestione sicurezza profilo** e fare clic su **Avanti**.  
  
    -   Nella scheda **Profili pubblici** selezionare la casella di controllo per il profilo che si desidera configurare e fare clic su **Avanti**.  
  
    -   Per completare la configurazione del profilo, rivedere le azioni da eseguire nella pagina **Completamento procedura guidata** quindi fare clic su **Fine** .  
  

  
## <a name="using-transact-sql"></a>Uso di Transact-SQL  
  
###  <a name="to-create-a-database-mail-private-profile"></a><a name="PrivateProfile"></a> Per creare un profilo privato di Posta elettronica database  
  
-   Connettersi all'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   Per creare un nuovo profilo, eseguire la stored procedure di sistema [sysmail_add_profile_sp &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sysmail-add-profile-sp-transact-sql) come illustrato di seguito:  
  
     **EXECUTEmsdb.dbo.sysmail_add_profile_sp**  
  
     *@profile_name*='*Nome profilo*'  
  
     *@description*='*Descrizione*'  
  
     dove *@profile_name* è il nome del profilo e *@description* è la descrizione del profilo. Questo parametro è facoltativo e,  
  
-   Per ogni account, eseguire la stored procedure [sysmail_add_profileaccount_sp &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sysmail-add-profileaccount-sp-transact-sql) come descritto di seguito:  
  
     **EXECUTEmsdb.dbo.sysmail_add_profileaccount_sp**  
  
     *@profile_name*='*Nome del profilo*'  
  
     *@account_name*='*Nome dell'account*'  
  
     *@sequence_number*='*numero di sequenza dell'account all'interno del profilo.* '  
  
     dove *@profile_name* è il nome del profilo e *@account_name* è il nome dell'account da aggiungere al profilo, *@sequence_number* determina l'ordine in cui gli account vengono usati nel profilo.  
  
-   Concedere l'accesso al profilo a ogni utente o ruolo del database che invierà posta elettronica tramite questo profilo. A tale scopo, eseguire la stored procedure [sysmail_add_principalprofile_sp &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sysmail-add-principalprofile-sp-transact-sql) come descritto di seguito:  
  
     **EXECUTEmsdb.sysmail_add_principalprofile_sp**  
  
     *@profile_name*='*Nome del profilo*'  
  
     *@ principal_name* = '*Nome dell'utente del database o ruolo*'  
  
     *@is_default*='*Stato del profilo predefinito* '  
  
     dove *@profile_name* è il nome del profilo e *@principal_name* è il nome dell'utente o del ruolo del database, *@is_default* determina se il profilo è quello predefinito per l'utente o il ruolo del database.  
  
 Nell'esempio seguente vengono creati un account e un profilo privato di Posta elettronica database, viene quindi aggiunto l'account al profilo e viene concesso al ruolo del database **DBMailUsers** nel database **msdb** l'accesso al profilo.  
  
```  
-- Create a Database Mail account  
EXECUTE msdb.dbo.sysmail_add_account_sp  
    @account_name = 'AdventureWorks Administrator',  
    @description = 'Mail account for administrative e-mail.',  
    @email_address = 'dba@Adventure-Works.com',  
    @replyto_address = 'danw@Adventure-Works.com',  
    @display_name = 'AdventureWorks Automated Mailer',  
    @mailserver_name = 'smtp.Adventure-Works.com' ;  
  
-- Create a Database Mail profile  
EXECUTE msdb.dbo.sysmail_add_profile_sp  
    @profile_name = 'AdventureWorks Administrator Profile',  
    @description = 'Profile used for administrative mail.' ;  
  
-- Add the account to the profile  
EXECUTE msdb.dbo.sysmail_add_profileaccount_sp  
    @profile_name = 'AdventureWorks Administrator Profile',  
    @account_name = 'AdventureWorks Administrator',  
    @sequence_number =1 ;  
  
-- Grant access to the profile to the DBMailUsers role  
EXECUTE msdb.dbo.sysmail_add_principalprofile_sp  
    @profile_name = 'AdventureWorks Administrator Profile',  
    @principal_name = 'ApplicationUser',  
    @is_default = 1 ;  
```  
  
 
  
###  <a name="to-create-a-database-mail-public-profile"></a><a name="PublicProfile"></a> Per creare un profilo pubblica di Posta elettronica database  
  
-   Connettersi all'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   Per creare un nuovo profilo, eseguire la stored procedure di sistema [sysmail_add_profile_sp &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sysmail-add-profile-sp-transact-sql) come illustrato di seguito:  
  
     **EXECUTEmsdb.dbo.sysmail_add_profile_sp**  
  
     *@profile_name*='*Nome profilo*'  
  
     *@description*='*Descrizione*'  
  
     dove *@profile_name* è il nome del profilo e *@description* è la descrizione del profilo. Questo parametro è facoltativo e,  
  
-   Per ogni account, eseguire la stored procedure [sysmail_add_profileaccount_sp &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sysmail-add-profileaccount-sp-transact-sql) come descritto di seguito:  
  
     **EXECUTEmsdb.dbo.sysmail_add_profileaccount_sp**  
  
     *@profile_name*='*Nome del profilo*'  
  
     *@account_name*='*Nome dell'account*'  
  
     *@sequence_number*='*numero di sequenza dell'account all'interno del profilo.* '  
  
     dove *@profile_name* è il nome del profilo e *@account_name* è il nome dell'account da aggiungere al profilo, *@sequence_number* determina l'ordine in cui gli account vengono usati nel profilo.  
  
-   Per dare accesso, eseguire la stored procedure [sysmail_add_principalprofile_sp &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sysmail-add-principalprofile-sp-transact-sql) come descritto di seguito:  
  
     **EXECUTEmsdb.sysmail_add_principalprofile_sp**  
  
     *@profile_name*='*Nome del profilo*'  
  
     *@ principal_name* = '**pubblico** o **0**'  
  
     *@is_default*='*Stato del profilo predefinito* '  
  
     dove *@profile_name* è il nome del profilo e *@principal_name* per indicare che si tratta di un profilo pubblico, *@is_default* determina se il profilo è l'impostazione predefinita per l'utente o il ruolo del database.  
  
 Nell'esempio seguente vengono creati un account e un profilo privato di Posta elettronica database, quindi viene aggiunto l'account al profilo e viene concesso l'accesso pubblico al profilo.  
  
```  
-- Create a Database Mail account  
  
EXECUTE msdb.dbo.sysmail_add_account_sp  
    @account_name = 'AdventureWorks Public Account',  
    @description = 'Mail account for use by all database users.',  
    @email_address = 'db_users@Adventure-Works.com',  
    @replyto_address = 'danw@Adventure-Works.com',  
    @display_name = 'AdventureWorks Automated Mailer',  
    @mailserver_name = 'smtp.Adventure-Works.com' ;  
  
-- Create a Database Mail profile  
  
EXECUTE msdb.dbo.sysmail_add_profile_sp  
    @profile_name = 'AdventureWorks Public Profile',  
    @description = 'Profile used for administrative mail.' ;  
  
-- Add the account to the profile  
  
EXECUTE msdb.dbo.sysmail_add_profileaccount_sp  
    @profile_name = 'AdventureWorks Public Profile',  
    @account_name = 'AdventureWorks Public Account',  
    @sequence_number =1 ;  
  
-- Grant access to the profile to all users in the msdb database  
  
EXECUTE msdb.dbo.sysmail_add_principalprofile_sp  
    @profile_name = 'AdventureWorks Public Profile',  
    @principal_name = 'public',  
    @is_default = 1 ;  
```  
  

  
  
