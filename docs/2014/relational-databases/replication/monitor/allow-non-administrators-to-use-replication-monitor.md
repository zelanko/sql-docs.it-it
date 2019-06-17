---
title: Consentire a utenti non amministratori di usare Monitoraggio replica | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- Replication Monitor, non-administrators access
ms.assetid: 1cf21d9e-831d-41a1-a5a0-83ff6d22fa86
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 9e8f03d12d3ac1695d4f6d000c8eab89a42004fd
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62667389"
---
# <a name="allow-non-administrators-to-use-replication-monitor"></a>Autorizzazione di utenti non amministratori all'utilizzo di Monitoraggio replica
  In questo argomento viene descritto come consentire agli utenti non amministratore di utilizzare Monitoraggio replica in [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] tramite [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../../includes/tsql-md.md)]. Monitoraggio replica può essere utilizzato da membri che appartengono ai ruoli seguenti:  
  
-   Il ruolo predefinito del server **sysadmin** .  
  
     Questi utenti possono monitorare la replica e avere il controllo completo sulla modifica delle proprietà di replica, ad esempio le pianificazioni degli agenti, i profili agente e così via.  
  
-   Il `replmonitor` ruolo del database nel database di distribuzione.  
  
     Questi utenti possono monitorare la replica, ma non possono modificare le proprietà di replica.  
  
 **Contenuto dell'argomento**  
  
-   **Prima di iniziare:**  
  
     [Sicurezza](#Security)  
  
-   **Per consentire a utenti non amministratori di utilizzare Monitoraggio replica tramite:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="Security"></a> Sicurezza  
  
####  <a name="Permissions"></a> Autorizzazioni  
 Per consentire a utenti non amministratori di utilizzare Monitoraggio replica, un membro del **sysadmin** ruolo predefinito del server è necessario aggiungere l'utente al database di distribuzione e assegnare all'utente di `replmonitor` ruolo.  
  
##  <a name="SSMSProcedure"></a> Utilizzo di SQL Server Management Studio  
  
#### <a name="to-allow-non-administrators-to-use-replication-monitor"></a>Per consentire a utenti non amministratori di utilizzare Monitoraggio replica  
  
1.  Connettersi al database di distribuzione in [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]e quindi espandere il nodo del server.  
  
2.  Espandere **Database**, **Database di sistema**e quindi il database di distribuzione (denominato **distribuzione** per impostazione predefinita).  
  
3.  Espandere **Sicurezza**, fare clic con il pulsante destro del mouse su **Utenti**e quindi scegliere **Nuovo utente**.  
  
4.  Immettere un nome utente e un account di accesso per l'utente.  
  
5.  Selezionare uno schema predefinito di `replmonitor`.  
  
6.  Selezionare il `replmonitor` casella di controllo la **l'appartenenza al ruolo del Database** griglia.  
  
7.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
##  <a name="TsqlProcedure"></a> Utilizzo di Transact-SQL  
  
#### <a name="to-add-a-user-to-the-replmonitor-fixed-database-role"></a>Per aggiungere un utente al ruolo predefinito del database replmonitor  
  
1.  Nel database di distribuzione del server di distribuzione eseguire [sp_helpuser &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-helpuser-transact-sql). Se l'utente non è elencato `UserName` nel set di risultati, l'utente deve essere concesso l'accesso al database di distribuzione usando il [CREATE USER &#40;Transact-SQL&#41; ](/sql/t-sql/statements/create-user-transact-sql) istruzione.  
  
2.  Nel server di distribuzione nel database di distribuzione, eseguire [sp_helprolemember &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-helprolemember-transact-sql), specificando il valore `replmonitor` per il **@rolename** parametro. Se l'utente è elencato `MemberName` nel set di risultati, appartiene già a questo ruolo.  
  
3.  Se l'utente non appartiene al `replmonitor` ruolo, eseguire [sp_addrolemember &#40;Transact-SQL&#41; ](/sql/relational-databases/system-stored-procedures/sp-addrolemember-transact-sql) nel server di distribuzione nel database di distribuzione. Specificare il valore `replmonitor` per **@rolename** e il nome dell'utente del database o i [!INCLUDE[msCoName](../../../includes/msconame-md.md)] account di accesso di Windows da aggiungere per **@membername** .  
  
#### <a name="to-remove-a-user-from-the-replmonitor-fixed-database-role"></a>Per rimuovere un utente dal ruolo predefinito del database replmonitor  
  
1.  Per verificare che l'utente appartiene al `replmonitor` ruolo, eseguire [sp_helprolemember &#40;Transact-SQL&#41; ](/sql/relational-databases/system-stored-procedures/sp-helprolemember-transact-sql) nel database di distribuzione, il server di distribuzione e specificare il valore `replmonitor` per **@rolename** . Se l'utente non è elencato in `MemberName` nel set di risultati, attualmente non appartiene al ruolo.  
  
2.  Se l'utente appartiene al `replmonitor` ruolo, eseguire [sp_droprolemember &#40;Transact-SQL&#41; ](/sql/relational-databases/system-stored-procedures/sp-droprolemember-transact-sql) nel server di distribuzione nel database di distribuzione. Specificare il valore `replmonitor` per **@rolename** e il nome dell'utente del database o l'account di accesso di Windows rimosso per **@membername** .  
  
  
