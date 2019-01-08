---
title: Impostare un Alias SQL Server per il servizio SQL Server Agent (SQL Server Management Studio) | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 752796caafa86ece1b471beb25a77ea381497409
ms.sourcegitcommit: 37310da0565c2792aae43b3855bd3948fd13e044
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/18/2018
ms.locfileid: "53588600"
---
# <a name="set-a-sql-server-alias-for-the-sql-server-agent-service-sql-server-management-studio"></a>Set a SQL Server Alias for the SQL Server Agent Service (SQL Server Management Studio)
  In questo argomento viene descritto come impostare un alias [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] per [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Agent, da utilizzare per la connessione al [!INCLUDE[ssDE](../includes/ssde-md.md)] utilizzando [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]. Per impostazione predefinita, il servizio [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Agent si connette a un'istanza di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] mediante named pipe utilizzando nomi di server dinamici che non richiedono alcuna configurazione client aggiuntiva. La configurazione di un alias di connessione del server è necessaria solo se non si utilizza il trasporto di rete predefinito o se ci si connette a un'istanza di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] che rimane in attesa su un'altra named pipe.  
  
 **Contenuto dell'argomento**  
  
-   **Prima di iniziare:**  
  
     [Limitazioni e restrizioni](#Restrictions)  
  
     [Sicurezza](#Security)  
  
-   [Per impostare un alias SQL Server per il servizio SQL Server Agent utilizzando SQL Server Management Studio](#SSMSProcedure)  
  
##  <a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="Restrictions"></a> Limitazioni e restrizioni  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Agent non funzionerà correttamente se non si seleziona un alias che fa riferimento all'istanza locale di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
-   In Esplora oggetti viene visualizzato il nodo [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Agent solo se si dispone dell'autorizzazione per utilizzarlo.  
  
###  <a name="Security"></a> Sicurezza  
  
####  <a name="Permissions"></a> Permissions  
 Per la corretta esecuzione delle funzioni, è necessario che [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Agent sia configurato per utilizzare le credenziali di un account membro del ruolo predefinito del server **sysadmin** in [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. L'account deve disporre delle autorizzazioni di Windows seguenti:  
  
-   Accesso come servizio (SeServiceLogonRight)  
  
-   Sostituzione di token a livello di processo (SeAssignPrimaryTokenPrivilege)  
  
-   Ignorare controllo incrociato (SeChangeNotifyPrivilege)  
  
-   Regolazione quote di memoria per un processo (SeIncreaseQuotaPrivilege)  
  
 Per altre informazioni sulle autorizzazioni di Windows necessarie per la [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] account del servizio dell'agente, vedere [selezionare un Account per il servizio SQL Server Agent](../ssms/agent/select-an-account-for-the-sql-server-agent-service.md) e [configurare gli account del servizio Windows e Le autorizzazioni](configure-windows/configure-windows-service-accounts-and-permissions.md).  
  
##  <a name="SSMSProcedure"></a> Utilizzo di SQL Server Management Studio  
  
#### <a name="to-set-a-sql-server-alias-for-the-sql-server-agent-service"></a>Per impostare un alias SQL Server per il servizio SQL Server Agent  
  
1.  In **Esplora oggetti**connettersi a un'istanza di [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] e quindi espandere tale istanza.  
  
2.  Fare clic con il pulsante destro del mouse su **SQL Server Agent**, quindi scegliere **Proprietà**.  
  
3.  Nella finestra di dialogo **Proprietà SQL Server Agent**_nome_server_ fare clic su **Connessione**in **Seleziona una pagina**e  
  
4.  Nella casella **Alias server host locale** , digitare l'alias del server a cui si deve connettere [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Agent.  
  
5.  Fare clic su **OK**.  
  
  
