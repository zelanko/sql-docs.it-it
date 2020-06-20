---
title: Modificare l'account di avvio del servizio per SQL Server (Gestione configurazione SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 01/07/2016
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- SQL Server services, startup account changes
- startup accounts [SQL Server]
- changing startup accounts for services
ms.assetid: d721c796-0397-46a7-901b-1a9a3c3fb385
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 105592676413fb43c4cac5b572623096a517b147
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84935103"
---
# <a name="change-the-service-startup-account-for-sql-server-sql-server-configuration-manager"></a>Modifica dell'account di avvio del servizio di SQL Server (Gestione configurazione SQL Server)
  Questo argomento descrive come usare Gestione configurazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per modificare le opzioni di avvio dei servizi [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e gli account di servizio usati dal [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] e da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../includes/tsql-md.md)]o PowerShell. Per altre informazioni su come selezionare un account di servizio appropriato, vedere [Configurare account di servizio e autorizzazioni di Windows](configure-windows-service-accounts-and-permissions.md).  
  
> [!IMPORTANT]  
>  Per rendere effettiva la modifica dell'account di avvio del servizio per il [!INCLUDE[ssDE](../../includes/ssde-md.md)] e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent, è necessario riavviare il servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , ovvero il [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Tutti i database associati a tale istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non saranno disponibili finché il servizio non verrà riavviato correttamente. Se è necessario modificare l'account di avvio del servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent, eseguire questa operazione durante l'esecuzione di attività di manutenzione pianificate regolarmente o quando è possibile portare i database offline senza interrompere le operazioni quotidiane.  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> Limitazioni e restrizioni  
  
-   Server cluster  
  
     La modifica dell'account del servizio usato da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent deve essere eseguita dal nodo attivo del cluster di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
     Quando l'esecuzione avviene in Windows Server 2008 (in una configurazione non predefinita che prevede l'utilizzo di gruppi di dominio), per modificare l'account del servizio usato da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent è necessario arrestare [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mediante Gestione configurazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , portando i gruppi di risorse offline.  
  
-   Aggiornamento della SKU (da[!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] a una versione non Express)  
  
     Durante l'installazione di [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] , il servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent viene configurato per l'utilizzo dell'account Servizio di rete, ma risulta disabilitato. Gestione configurazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] consente di modificare l'account assegnato per il servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent, ma non di abilitare o avviare il servizio. Dopo aver eseguito l'aggiornamento della SKU da [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] a una versione non Express, il servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent non viene abilitato automaticamente, ma può esserlo quando necessario mediante Gestione configurazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e l'impostazione della modalità di avvio del servizio su Manuale o Automatico.  
  
##  <a name="using-sql-server-configuration-manager"></a><a name="SSMSProcedure"></a> Utilizzo di Gestione configurazione SQL Server  
  
#### <a name="to-change-the-sql-server-service-startup-account"></a>Per modificare l'account di avvio del servizio SQL Server  
  
1.  Fare clic sul menu **Start** , scegliere **Tutti i programmi**, [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)], **Strumenti di configurazione**e quindi **Gestione configurazione SQL Server**.  
  
    > [!NOTE]  
    >  Poiché Gestione configurazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è uno snap-in per il programma [!INCLUDE[msCoName](../../includes/msconame-md.md)] Management Console e non un programma autonomo, Gestione configurazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non viene visualizzato come applicazione nelle versioni più recenti di Windows.  
    >   
    >  -   **Windows 10**:  
    >          Per aprire [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager, nella **pagina iniziale**digitare SQLServerManager12. msc (per [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ). Per le versioni precedenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , sostituire 12 con un numero inferiore. Se si fa clic su SQLServerManager12.msc, viene aperto Gestione configurazione. Per aggiungere la Configuration Manager alla pagina iniziale o alla barra delle applicazioni, fare clic con il pulsante destro del mouse su SQLServerManager12. msc, quindi scegliere **Apri percorso file**. In Esplora file di Windows fare clic con il pulsante destro del mouse su SQLServerManager12. msc, quindi scegliere **Aggiungi a Start** o **Aggiungi alla barra delle applicazioni**.  
    > -   **Windows 8**:  
    >          Per aprire [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager, nell'accesso alla **ricerca** , in **app**digitare **SQLServerManager \<version> . msc** , ad esempio `SQLServerManager12.msc` , quindi premere **invio**.  
  
2.  In Gestione configurazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fare clic su **Servizi di SQL Server**.  
  
3.  Nel riquadro dei dettagli fare clic con il pulsante destro del mouse sull'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per la quale si desidera modificare l'account di avvio del servizio e quindi fare clic su **Proprietà**.  
  
4.  Nella finestra di dialogo ** \<***instancename***> Proprietà SQL Server** fare clic sulla scheda **accesso** e selezionare un tipo di account **Accedi come** .  
  
5.  Dopo aver selezionato il nuovo account di avvio del servizio, scegliere **OK**.  
  
     Verrà visualizzata una finestra di messaggio in cui viene richiesto se si desidera riavviare il servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
6.  Fare clic su **Sì**, quindi chiudere Gestione configurazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="see-also"></a>Vedere anche  
 [Avviare, arrestare, sospendere, riprendere, riavviare il motore di database, SQL Server Agent o SQL Server Browser](start-stop-pause-resume-restart-sql-server-services.md)   
 [Configurazione di WMI per mostrare lo stato del server in Strumenti SQL Server](../../ssms/configure-wmi-to-show-server-status-in-sql-server-tools.md)  
  
  
