---
title: Impostare l'Account di avvio del servizio per SQL Server Agent (Gestione configurazione SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent, service accounts
- startup accounts [SQL Server]
- service startup accounts [SQL Server Agent]
ms.assetid: 46ffe818-ebb5-43a0-840b-923f219a2472
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 30c50d1f6efc44c17eac76e0e03432c2461da296
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63033666"
---
# <a name="set-the-service-startup-account-for-sql-server-agent-sql-server-configuration-manager"></a>Set the Service Startup Account for SQL Server Agent (SQL Server Configuration Manager)
  L'account di avvio del servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent definisce l'account di Windows con cui viene eseguito [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent e le relative autorizzazioni di rete. In questo argomento viene descritto come impostare l'account del servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent con Gestione configurazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] tramite [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
 **Contenuto dell'argomento**  
  
-   **Prima di iniziare:**  
  
     [Limitazioni e restrizioni](#Restrictions)  
  
     [Sicurezza](#Security)  
  
-   [Per impostare l'account di avvio del servizio per SQL Server Agent tramite SQL Server Management Studio](#SSMSProcedure)  
  
##  <a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="Restrictions"></a> Limitazioni e restrizioni  
  
-   A partire da [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], non è più necessario che l'account di avvio del servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent sia un membro del gruppo Administrators di [!INCLUDE[msCoName](../../includes/msconame-md.md)] . L'account di avvio del servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent deve tuttavia essere membro del ruolo predefinito del server [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]sysadmin. Per usare l'elaborazione dei processi multiserver, l'account deve essere un membro del ruolo TargetServersRole del database msdb nel server master.  
  
-   In Esplora oggetti viene visualizzato il nodo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent solo se si dispone dell'autorizzazione per utilizzarlo.  
  
###  <a name="Security"></a> Sicurezza  
  
####  <a name="Permissions"></a> Autorizzazioni  
 Per eseguire le funzioni [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent deve essere configurato per utilizzare le credenziali di un account che è un membro del `sysadmin` ruolo predefinito del server in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. L'account deve disporre delle autorizzazioni di Windows seguenti:  
  
-   Accesso come servizio (SeServiceLogonRight)  
  
-   Sostituzione di token a livello di processo (SeAssignPrimaryTokenPrivilege)  
  
-   Ignorare controllo incrociato (SeChangeNotifyPrivilege)  
  
-   Regolazione quote di memoria per un processo (SeIncreaseQuotaPrivilege)  
  
 Per altre informazioni sulle autorizzazioni di Windows necessarie per la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] account del servizio dell'agente, vedere [selezionare un Account per il servizio SQL Server Agent](select-an-account-for-the-sql-server-agent-service.md) e [configurare gli account del servizio Windows e Le autorizzazioni](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md).  
  
##  <a name="SSMSProcedure"></a> Utilizzo di SQL Server Management Studio  
  
#### <a name="to-set-the-service-startup-account-for-sql-server-agent"></a>Per impostare l'account di avvio del servizio SQL Server Agent  
  
1.  In **Server registrati**, fare clic sul segno più per espandere **Motore di database**.  
  
2.  Fare clic sul segno più per espandere la cartella **Gruppi di server locali** .  
  
3.  Fare clic con il pulsante destro del mouse sull'istanza del server dove si intende impostare l'account di avvio del servizio e selezionare **Gestione configurazione SQL Server...**.  
  
4.  Nella finestra di dialogo **Controllo account utente** fare clic su **Sì**.  
  
5.  Nel riquadro della console di Gestione configurazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , selezionare **Servizi di SQL Server**.  
  
6.  Nel riquadro dei dettagli fare clic con il pulsante destro del mouse su **SQL Server Agent**_(nome_server)_, dove *nome_server* è il nome dell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent per cui si vuole modificare l'account di avvio del servizio e scegliere **Proprietà**.  
  
7.  Nella finestra di dialogo **Proprietà**_di_ **Proprietà** , fare clic sulla scheda **Accesso** e selezionare una delle seguenti opzioni in **Accedi come**:  
  
    -   **Account predefinito**: selezionare questa opzione se i processi usano solo risorse del server locale. Per informazioni sulla selezione di un account predefinito di Windows, vedere [Selezionare un account per il servizio SQL Server Agent](https://msdn.microsoft.com/library/ms191543.aspx).  
  
        > [!IMPORTANT]  
        >  Il servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent non supporta l'account **Servizio locale** in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
    -   **Account seguente**: selezionare questa opzione se i processi richiedono risorse dalla rete, incluse le risorse dell'applicazione, per inoltrare eventi ad altri registri applicazioni di Windows oppure se per inviare una notifica agli operatori tramite messaggi di posta elettronica o cercapersone.  
  
         Se si seleziona questa opzione:  
  
        1.  Nella casella **Nome account** , immettere l'account che sarà utilizzato per eseguire SQL Server Agent. In alternativa, fare clic su **Sfoglia** per aprire la finestra di dialogo **Seleziona utente o gruppo** e selezionare l'account da utilizzare.  
  
        2.  Immettere nella casella **Password** la password per l'account. Immettere nuovamente la password nella casella **Conferma password** .  
  
8.  Fare clic su **OK**.  
  
9. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Fare clic sul pulsante **Chiudi** in Gestione configurazione.  
  
  
