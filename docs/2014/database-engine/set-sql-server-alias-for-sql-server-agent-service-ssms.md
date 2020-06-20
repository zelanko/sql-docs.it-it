---
title: Impostare un alias di SQL Server per il servizio di SQL Server Agent (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- aliases [SQL Server], creating
- SQL Server Agent, aliases
ms.assetid: 02d6295d-ab52-44f0-8f1b-f3910a507d8f
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: b9f91ec957665975fd956e36a5af3c4261fb47af
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84929192"
---
# <a name="set-a-sql-server-alias-for-the-sql-server-agent-service-sql-server-management-studio"></a>Set a SQL Server Alias for the SQL Server Agent Service (SQL Server Management Studio)
  In questo argomento viene descritto come impostare un [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] alias per [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Agent da utilizzare per la connessione a utilizzando [!INCLUDE[ssDE](../includes/ssde-md.md)] [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] . Per impostazione predefinita, il servizio [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Agent si connette a un'istanza di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] mediante named pipe utilizzando nomi di server dinamici che non richiedono alcuna configurazione client aggiuntiva. La configurazione di un alias di connessione del server è necessaria solo se non si utilizza il trasporto di rete predefinito o se ci si connette a un'istanza di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] che rimane in attesa su un'altra named pipe.  
  
 **Contenuto dell'articolo**  
  
-   **Prima di iniziare:**  
  
     [Limitazioni e restrizioni](#Restrictions)  
  
     [Sicurezza](#Security)  
  
-   [Per impostare un alias SQL Server per il servizio SQL Server Agent utilizzando SQL Server Management Studio](#SSMSProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> Limitazioni e restrizioni  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Agent non funzionerà correttamente se non si seleziona un alias che fa riferimento all'istanza locale di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
-   In Esplora oggetti viene visualizzato il nodo [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Agent solo se si dispone dell'autorizzazione per utilizzarlo.  
  
###  <a name="security"></a><a name="Security"></a> Sicurezza  
  
####  <a name="permissions"></a><a name="Permissions"></a> Autorizzazioni  
 Per la corretta esecuzione delle funzioni, è necessario che [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Agent sia configurato per utilizzare le credenziali di un account membro del ruolo predefinito del server **sysadmin** in [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. L'account deve disporre delle autorizzazioni di Windows seguenti:  
  
-   Accesso come servizio (SeServiceLogonRight)  
  
-   Sostituzione di token a livello di processo (SeAssignPrimaryTokenPrivilege)  
  
-   Ignorare controllo incrociato (SeChangeNotifyPrivilege)  
  
-   Regolazione quote di memoria per un processo (SeIncreaseQuotaPrivilege)  
  
 Per ulteriori informazioni sulle autorizzazioni di Windows necessarie per l' [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] account del servizio Agent, vedere [selezionare un account per il servizio SQL Server Agent](../ssms/agent/select-an-account-for-the-sql-server-agent-service.md) e [configurare account di servizio e autorizzazioni di Windows](configure-windows/configure-windows-service-accounts-and-permissions.md).  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Utilizzo di SQL Server Management Studio  
  
#### <a name="to-set-a-sql-server-alias-for-the-sql-server-agent-service"></a>Per impostare un alias SQL Server per il servizio SQL Server Agent  
  
1.  In **Esplora oggetti**connettersi a un'istanza di [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] e quindi espandere tale istanza.  
  
2.  Fare clic con il pulsante destro del mouse su **SQL Server Agent**, quindi scegliere **Proprietà**.  
  
3.  Nella finestra di dialogo **proprietà SQL Server Agent**_server_name_ fare clic su **connessione**in **Selezione pagina**e  
  
4.  Nella casella **Alias server host locale** , digitare l'alias del server a cui si deve connettere [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Agent.  
  
5.  Fare clic su **OK**.  
  
  
