---
title: Creazione di un account di accesso | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- creating a login
ms.assetid: a2512310-bdb6-41dc-858a-e866b2b58afc
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 7ceed5f82af858f6a2dc3a88df7276d5ba2fda3f
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "68211200"
---
# <a name="creating-a-login"></a>Creazione di un account di accesso
  Per accedere a [!INCLUDE[ssDE](../includes/ssde-md.md)]è necessario che gli utenti dispongano di un account di accesso. L'account di accesso può rappresentare l'identità dell'utente come un account di Windows o come membro di un gruppo di Windows oppure un account di accesso di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] esistente solo in [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Se possibile, è consigliabile utilizzare l'autenticazione di Windows.  
  
 Per impostazione predefinita, gli amministratori del computer dispongono di accesso completo a [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Ai fini di questa lezione, è sufficiente un utente che dispone di minori privilegi e verrà pertanto creato un nuovo account dell'autenticazione di Windows locale nel computer in uso. A tale scopo, è necessario essere un amministratore del computer. Al nuovo utente verrà quindi concesso l'accesso a [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
### <a name="to-create-a-new-windows-account"></a>Per creare un nuovo account di Windows  
  
1.  Fare clic sul pulsante **Start**, scegliere **Esegui**, digitare `%SystemRoot%\system32\compmgmt.msc /s`nella casella **Apri** e quindi fare clic su **OK** per aprire il programma di gestione computer.  
  
2.  In **Utilità di sistema**espandere **Utenti e gruppi locali**, fare clic con il pulsante destro del mouse su **Utenti**e quindi scegliere **Nuovo utente**.  
  
3.  Nella casella **Nome utente** digitare **Mary**.  
  
4.  Nelle caselle **Password** e **Conferma password** digitare una password complessa e quindi fare clic su **Crea** per creare un nuovo utente locale di Windows.  
  
### <a name="to-create-a-login"></a>Per creare un account di accesso  
  
1.  Nella finestra dell'editor di query di [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]digitare ed eseguire il codice seguente sostituendo `computer_name` con il nome del computer. `FROM WINDOWS` indica che Windows autenticherà l'utente. L'argomento facoltativo `DEFAULT_DATABASE` connette l'utente `Mary` al database `TestData` a meno che la relativa stringa di connessione indichi un altro database. Questa istruzione introduce il punto e virgola come carattere di fine facoltativo per un'istruzione [!INCLUDE[tsql](../includes/tsql-md.md)] .  
  
    ```  
    CREATE LOGIN [computer_name\Mary]  
        FROM WINDOWS  
        WITH DEFAULT_DATABASE = [TestData];  
    GO  
    ```  
  
     Ciò autorizza il nome utente `Mary`, autenticato dal computer in uso, ad accedere all'istanza di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Se sono presenti più istanze di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] nel computer, è necessario creare l'account di accesso in ogni istanza a cui l'utente `Mary` deve accedere.  
  
    > [!NOTE]  
    >  Poiché `Mary` non è un account di dominio, il nome utente può essere autenticato solo nel computer in questione.  
  
## <a name="next-task-in-lesson"></a>Attività successiva della lezione  
 [Concessione dell'accesso a un database](lesson-2-2-granting-access-to-a-database.md)  
  
## <a name="see-also"></a>Vedi anche  
 [Crea account di accesso &#40;&#41;Transact-SQL](/sql/t-sql/statements/create-login-transact-sql)   
 [Scegliere una modalità di autenticazione](../relational-databases/security/choose-an-authentication-mode.md)  
  
  
