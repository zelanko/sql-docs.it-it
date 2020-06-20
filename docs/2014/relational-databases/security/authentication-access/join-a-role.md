---
title: Aggiungere un ruolo | Microsoft Docs
ms.custom: ''
ms.date: 07/14/2016
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
f1_keywords:
- SQL12.SWB.DATABASEUSER.MEMBERSHIP.F1
helpviewer_keywords:
- adding a member to a role
- join a role
ms.assetid: 05c8d10d-5823-46c6-8b1a-81722da6a42b
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 58e8c071672c8c3afba8d6c424488899dcf76be7
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85016378"
---
# <a name="join-a-role"></a>aggiungere un ruolo
  In questo argomento si descrive come assegnare ruoli agli account di accesso e agli utenti di database in [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] tramite [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../../includes/tsql-md.md)]. Utilizzare i ruoli disponibili in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] per gestire in modo efficace le autorizzazioni. Assegnare autorizzazioni ai ruoli, quindi aggiungere e rimuovere utenti e account di accesso ai ruoli. Utilizzando i ruoli, non è necessario gestire singolarmente le autorizzazioni per ciascun utente.  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] supporta quattro tipi di ruoli.  
  
-   Ruoli predefiniti del server  
  
-   Ruoli del server definiti dall'utente  
  
-   Ruoli predefiniti del database  
  
-   Ruoli del database definiti dall'utente  
  
 I ruoli predefiniti sono automaticamente disponibili in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. I ruoli predefiniti dispongono delle autorizzazioni necessarie per completare attività comuni. Per ulteriori informazioni sui ruoli predefiniti, vedere i collegamenti seguenti. I ruoli definiti dall'utente vengono creati dall'utente e possono essere personalizzati con le autorizzazioni desiderate. Per ulteriori informazioni sui ruoli definiti dall'utente, vedere i collegamenti seguenti.  
  
 **Contenuto dell'articolo**  
  
-   **Prima di iniziare:**  
  
     [Limitazioni e restrizioni](#Restrictions)  
  
     [Sicurezza](#Security)  
  
-   **Per assegnare ruoli ad account di accesso e utenti di database tramite:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> Limitazioni e restrizioni  
  
-   La modifica del nome di un ruolo del database non comporta la modifica del numero di ID, del proprietario o delle autorizzazioni del ruolo.  
  
-   I ruoli del database sono visibili nelle viste del catalogo sys.database_role_members e sys.database_principals.  
  
###  <a name="security"></a><a name="Security"></a> Sicurezza  
  
####  <a name="permissions"></a><a name="Permissions"></a> Autorizzazioni  
 È richiesta `ALTER ANY ROLE` l'autorizzazione per il database, l' `ALTER` autorizzazione per il ruolo o l'appartenenza a **db_securityadmin**.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Con SQL Server Management Studio  
  
#### <a name="to-add-a-member-to-a-fixed-server-role"></a>Per aggiungere un membro a un ruolo predefinito del server  
  
1.  In Esplora oggetti espandere il server in cui si desidera modificare un ruolo predefinito del server.  
  
2.  Espandere la cartella **Sicurezza** .  
  
3.  Espandere la cartella **Ruoli del server** .  
  
4.  Fare clic con il pulsante destro del mouse sul ruolo da modificare e selezionare **Proprietà**.  
  
5.  Nella finestra di dialogo **Proprietà ruolo server-**_server_role_name_ , nella pagina **membri** , fare clic su **Aggiungi**.  
  
6.  Nella finestra di dialogo **Seleziona account di accesso o ruolo del server** immettere l'account di accesso o il ruolo del server da aggiungere a questo ruolo del server in **Immettere i nomi degli oggetti da selezionare (esempi)** . In alternativa, fare clic su **Sfoglia...** e selezionare uno, alcuni o tutti gli oggetti disponibili nella finestra di dialogo **Cerca oggetti**. Fare clic su **OK** per tornare alla finestra di dialogo **Proprietà ruolo server-**_server_role_name_ .  
  
7.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
#### <a name="to-add-a-member-to-a-user-defined-database-role"></a>Per aggiungere un membro a un ruolo del database definito dall'utente  
  
1.  In Esplora oggetti espandere il server in cui si desidera modificare un ruolo del database definito dall'utente.  
  
2.  Espandere la cartella **Database** .  
  
3.  Espandere il database in cui si desidera modificare un ruolo del database definito dall'utente.  
  
4.  Espandere la cartella **Sicurezza** .  
  
5.  Espandere la cartella **Ruoli** .  
  
6.  Espandere la cartella **Ruoli del server** .  
  
7.  Fare clic con il pulsante destro del mouse sul ruolo da modificare e selezionare **Proprietà**.  
  
8.  Nella finestra di dialogo **Proprietà ruolo database-**_database_role_name_ , nella pagina **generale** , fare clic su **Aggiungi**.  
  
9. Nella finestra di dialogo **Seleziona utente o ruolo del database** immettere l'account di accesso o il ruolo del database da aggiungere a questo ruolo del database in **Immettere i nomi degli oggetti da selezionare (esempi)** . In alternativa, fare clic su **Sfoglia...** e selezionare uno, alcuni o tutti gli oggetti disponibili nella finestra di dialogo **Cerca oggetti**. Fare clic su **OK** per tornare alla finestra di dialogo **Proprietà ruolo database-**_database_role_name_ .  
  
10. [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Con Transact-SQL  
  
#### <a name="to-add-a-member-to-a-fixed-server-role"></a>Per aggiungere un membro a un ruolo predefinito del server  
  
1.  In **Esplora oggetti**connettersi a un'istanza del [!INCLUDE[ssDE](../../../includes/ssde-md.md)].  
  
2.  Sulla barra Standard fare clic su **Nuova query**.  
  
3.  Copiare e incollare l'esempio seguente nella finestra Query, quindi fare clic su **Esegui**.  
  
    ```  
    ALTER SERVER ROLE diskadmin ADD MEMBER [Domain\Juan] ;  
    GO  
    ```  
  
 Per altre informazioni, vedere [ALTER ROLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-role-transact-sql).  
  
#### <a name="to-add-a-member-to-a-user-defined-database-role"></a>Per aggiungere un membro a un ruolo del database definito dall'utente  
  
1.  In **Esplora oggetti**connettersi a un'istanza del [!INCLUDE[ssDE](../../../includes/ssde-md.md)].  
  
2.  Sulla barra Standard fare clic su **Nuova query**.  
  
3.  Copiare e incollare l'esempio seguente nella finestra Query, quindi fare clic su **Esegui**.  
  
    ```  
    ALTER ROLE Marketing ADD MEMBER [Domain\Juan] ;  
    GO  
    ```  
  
 Per altre informazioni, vedere [sp_addrolemember &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addrolemember-transact-sql).  
  
## <a name="see-also"></a>Vedere anche  
 [Ruoli a livello di server](server-level-roles.md)   
 [Ruoli a livello di database](../authentication-access/database-level-roles.md)   
 [Ruoli applicazione](../authentication-access/application-roles.md)  
  
  
