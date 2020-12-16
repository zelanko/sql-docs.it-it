---
description: 'Lezione 2: Configurare le autorizzazioni per gli oggetti di database'
title: 'Esercitazione: Configurare le autorizzazioni per gli oggetti di database'
ms.custom: seo-lt-2019
ms.date: 07/31/2018
ms.prod: sql
ms.technology: t-sql
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- database permissions
ms.assetid: f964b66a-ec32-44c2-a185-6a0f173bfa22
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: e254a0f99ed717dbfde73f671d905ce8ecdf8264
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2020
ms.locfileid: "97466002"
---
# <a name="lesson-2-configure-permissions-on-database-objects"></a>Lezione 2: Configurare le autorizzazioni per gli oggetti di database
[!INCLUDE[tsql-appliesto-ss2008-all-md](../includes/tsql-appliesto-ss2008-all-md.md)]
La concessione di un accesso utente a un database consiste in tre passaggi. Viene innanzitutto creato un account di accesso, il quale consente all'utente di connettersi a [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]. L'account di accesso viene quindi configurato come utente nel database specificato. Viene infine concessa l'autorizzazione utente per gli oggetti di database. In questa lezione vengono illustrati tali passaggi e viene descritto come creare due oggetti, ovvero una vista e una stored procedure.  

  >[!NOTE]
  > Questa lezione si basa sugli oggetti creati nella [Lezione 1: Creare oggetti di database](lesson-1-creating-database-objects.md). Completare la lezione 1 prima di continuare con la lezione 2. 

## <a name="prerequisites"></a>Prerequisiti
Per completare questa esercitazione è necessario avere SQL Server Management Studio e l'accesso a un'istanza di SQL Server. 

- Installare [SQL Server Management Studio](../ssms/download-sql-server-management-studio-ssms.md).

Se non si dispone dell'accesso a un'istanza di SQL Server, selezionare la piattaforma in uso tra i collegamenti seguenti. Se si sceglie Autenticazione SQL, usare le credenziali di accesso di SQL Server.
- **Windows**: [scaricare SQL Server 2017 Developer Edition](https://www.microsoft.com/sql-server/sql-server-downloads).
- **macOS**: [scaricare SQL Server 2017 in Docker](../linux/quickstart-install-connect-docker.md).

[!INCLUDE[Freshness](../includes/paragraph-content/fresh-note-steps-feedback.md)]

## <a name="create-a-login"></a>Crea un accesso
Per accedere a [!INCLUDE[ssDE](../includes/ssde-md.md)]è necessario che gli utenti dispongano di un account di accesso. L'account di accesso può rappresentare l'identità dell'utente come un account di Windows o come membro di un gruppo di Windows oppure un account di accesso di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] esistente solo in [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Se possibile, è consigliabile utilizzare l'autenticazione di Windows.  
  
Per impostazione predefinita, gli amministratori del computer dispongono di accesso completo a [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Ai fini di questa lezione, è sufficiente un utente che dispone di minori privilegi e verrà pertanto creato un nuovo account dell'autenticazione di Windows locale nel computer in uso. A tale scopo, è necessario essere un amministratore del computer. Al nuovo utente verrà quindi concesso l'accesso a [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
### <a name="create-a-new-windows-account"></a>Creare un nuovo account di Windows  
  
1.  Fare clic sul pulsante **Start**, scegliere **Esegui**, nella casella **Apri** digitare **%SystemRoot%\system32\compmgmt.msc /s** e quindi fare clic su **OK** per aprire l'applicazione Gestione computer. 
2.  In **Utilità di sistema** espandere **Utenti e gruppi locali**, fare clic con il pulsante destro del mouse su **Utenti** e quindi scegliere **Nuovo utente**.    
3.  Nella casella **Nome utente** digitare **Mary**.    
4.  Nelle caselle **Password** e **Conferma password** digitare una password complessa e quindi fare clic su **Crea** per creare un nuovo utente locale di Windows.  
  
### <a name="create-a-sql-login"></a>Creare un account di accesso SQL  

Nella finestra dell'editor di query di [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]digitare ed eseguire il codice seguente sostituendo `computer_name` con il nome del computer. `FROM WINDOWS` indica che Windows autenticherà l'utente. L'argomento facoltativo `DEFAULT_DATABASE` connette l'utente `Mary` al database `TestData` a meno che la relativa stringa di connessione indichi un altro database. Questa istruzione introduce il punto e virgola come carattere di fine facoltativo per un'istruzione [!INCLUDE[tsql](../includes/tsql-md.md)] .
  
  ```sql  
  CREATE LOGIN [computer_name\Mary]  
      FROM WINDOWS  
      WITH DEFAULT_DATABASE = [TestData];  
  GO  
  ```  
  
  Ciò autorizza il nome utente `Mary`, autenticato dal computer in uso, ad accedere all'istanza di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Se sono presenti più istanze di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] nel computer, è necessario creare l'account di accesso in ogni istanza a cui l'utente `Mary` deve accedere.    
  > [!NOTE]  
  > Poiché `Mary` non è un account di dominio, il nome utente può essere autenticato solo nel computer in questione. 


## <a name="grant-access-to-a-database"></a>Concedere l'accesso a un database
L'utente Mary dispone ora dell'accesso all'istanza di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], ma non delle autorizzazioni necessarie per accedere ai database. L'utente non dispone inoltre dell'accesso al proprio database predefinito **TestData** a meno che non lo si autorizzi in qualità di utente del database.  
  
Per concedere l'accesso all'utente Mary, passare al database **TestData** e quindi utilizzare l'istruzione CREATE USER per eseguire il mapping dell'account utente a un utente denominato Mary.  
  
### <a name="to-create-a-user-in-a-database"></a>Per creare un utente in un database  
  
Digitare ed eseguire le istruzioni seguenti sostituendo `computer_name` con il nome del computer in uso per concedere all'utente `Mary` l'accesso al database `TestData` .
  
 ```sql  
 USE [TestData];  
 GO  
 
 CREATE USER [Mary] FOR LOGIN [computer_name\Mary];  
 GO    
 ```  
  
 L'utente Mary dispone ora dell'accesso a [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] e al database `TestData` .  


## <a name="create-views-and-stored-procedures"></a>Creare viste e stored procedure
In qualità di amministratore, l'utente è autorizzato a eseguire l'istruzione SELECT dalla tabella **Products** e dalla vista **vw_Names** , nonché a eseguire la procedura **pr_Names** . All'utente Mary non sono tuttavia concesse tali autorizzazioni. Per concedere a tale utente le autorizzazioni necessarie, utilizzare l'istruzione GRANT.  

### <a name="grant-permission-to-stored-procedure"></a>Concedere l'autorizzazione per una stored procedure  
Eseguire l'istruzione seguente per concedere a `Mary` l'autorizzazione `EXECUTE` per la stored procedure `pr_Names` .
  
  ```sql  
  GRANT EXECUTE ON pr_Names TO Mary;  
  GO  
  ```  
  
In questo scenario, all'utente Mary è consentito solo l'accesso alla tabella **Products** usando la stored procedure. Se si desidera autorizzare l'utente Mary a eseguire un'istruzione SELECT sulla vista, è inoltre necessario eseguire `GRANT SELECT ON vw_Names TO Mary`. Per rimuovere l'accesso agli oggetti di database, utilizzare l'istruzione REVOKE.  
  
> [!NOTE]  
> Se la tabella, la vista e la stored procedure non appartengono allo stesso schema, la procedura per la concessione delle autorizzazioni risulta più complessa.  
  
### <a name="about-grant"></a>Informazioni sull'istruzione GRANT  
È necessario disporre dell'autorizzazione EXECUTE per eseguire una stored procedure. Per accedere e modificare i dati, è necessario disporre delle autorizzazioni SELECT, INSERT, UPDATE e DELETE. L'istruzione GRANT è inoltre utilizzata per altre autorizzazioni , ad esempio quella per creare tabelle.  
  
## <a name="next-steps"></a>Passaggi successivi
L'articolo successivo illustra come rimuovere gli oggetti di database creati nelle altre lezioni. 

Per altre informazioni, vedere l'articolo successivo:
> [!div class="nextstepaction"]
>[Passaggi successivi](lesson-3-deleting-database-objects.md)
