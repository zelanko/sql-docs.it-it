---
title: Gestione configurazione SQL Server - Modificare l'account di avvio del servizio | Microsoft Docs
ms.custom: ''
ms.date: 01/06/2016
ms.prod: sql
ms.prod_service: high-availability
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
manager: jroth
ms.openlocfilehash: 5e5c6ff900079e0dec26d49919f51ebe7c1128f5
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/07/2019
ms.locfileid: "66772038"
---
# <a name="scm-services---change-the-service-startup-account"></a>Gestione configurazione SQL Server - Modificare l'account di avvio del servizio
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  In questo argomento viene descritto come usare Gestione configurazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per modificare le opzioni di avvio dei servizi [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e gli account del servizio usati dal [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent, da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser, da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]e da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../includes/tsql-md.md)]o PowerShell. Per altre informazioni su come selezionare un account di servizio appropriato, vedere [Configurare account di servizio e autorizzazioni di Windows](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md).  
  
> [!IMPORTANT]  
>  Per rendere effettiva la modifica dell'account di avvio del servizio per il [!INCLUDE[ssDE](../../includes/ssde-md.md)] e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent, è necessario riavviare il servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , ovvero il [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Tutti i database associati a tale istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non saranno disponibili finché il servizio non verrà riavviato correttamente. Se è necessario modificare l'account di avvio del servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent, eseguire questa operazione durante l'esecuzione di attività di manutenzione pianificate regolarmente o quando è possibile portare i database offline senza interrompere le operazioni quotidiane.  
  
##  <a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="Restrictions"></a> Limitazioni e restrizioni  
  
-   Server cluster  
  
     La modifica dell'account del servizio usato da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent deve essere eseguita dal nodo attivo del cluster di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
     Quando l'esecuzione avviene in Windows Server 2008 (in una configurazione non predefinita che prevede l'utilizzo di gruppi di dominio), per modificare l'account del servizio usato da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent è necessario arrestare [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mediante Gestione configurazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , portando i gruppi di risorse offline.  
  
-   Aggiornamento della SKU (da[!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] a una versione non Express)  
  
     Durante l'installazione di [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] , il servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent viene configurato per l'utilizzo dell'account Servizio di rete, ma risulta disabilitato. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Gestione configurazione consente di modificare l'account assegnato per il servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent, ma non di abilitare o avviare il servizio. Dopo aver eseguito l'aggiornamento della SKU da [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] a una versione non Express, il servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent non viene abilitato automaticamente, ma può esserlo quando necessario mediante Gestione configurazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e l'impostazione della modalità di avvio del servizio su Manuale o Automatico.  
  
##  <a name="SSMSProcedure"></a> Utilizzo di Gestione configurazione SQL Server  
  
#### <a name="to-change-the-sql-server-service-startup-account"></a>Per modificare l'account di avvio del servizio SQL Server  
  
1.  Fare clic sul menu **Start** , scegliere **Tutti i programmi**, [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)], **Strumenti di configurazione**e quindi **Gestione configurazione SQL Server**.  
  
    > [!NOTE]  
    >  Poiché Gestione configurazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è uno snap-in per il programma [!INCLUDE[msCoName](../../includes/msconame-md.md)] Management Console e non un programma autonomo, Gestione configurazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non viene visualizzato come applicazione nelle nuove versioni di Windows.  
    >   
    >  -   **Windows 10**:  
    >          per aprire Gestione configurazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , nella **pagina iniziale**digitare SQLServerManager13.msc (per [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]). Per le versioni precedenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , sostituire 13 con un numero inferiore. Se si fa clic su SQLServerManager13.msc, viene aperto Gestione configurazione. Per aggiungere Gestione configurazione alla pagina iniziale o alla barra delle applicazioni, fare clic con il pulsante destro del mouse su SQLServerManager13.msc e quindi scegliere **Apri percorso file**. In Esplora file di Windows fare clic con il pulsante destro del mouse su SQLServerManager13.msc e quindi scegliere **Aggiungi a Start** o **Aggiungi alla barra delle applicazioni**.  
    > -   **Windows 8**:  
    >          Per aprire Gestione configurazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], nell'accesso alla **ricerca** in **App** digitare **SQLServerManager\<versione>.msc**, ad esempio **SQLServerManager13.msc** e quindi premere **INVIO**.  
  
2.  In Gestione configurazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fare clic su **Servizi di SQL Server**.  
  
3.  Nel riquadro dei dettagli fare clic con il pulsante destro del mouse sull'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per la quale si desidera modificare l'account di avvio del servizio e quindi fare clic su **Proprietà**.  
  
4.  Nella finestra di dialogo **SQL Server \<***nomeistanza***> Proprietà** fare clic sulla scheda **Accesso** e selezionare un tipo di account in **Accedi come**.  
  
5.  Dopo aver selezionato il nuovo account di avvio del servizio, scegliere **OK**.  
  
     Verrà visualizzata una finestra di messaggio in cui viene richiesto se si desidera riavviare il servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
6.  Fare clic su **Sì**, quindi chiudere Gestione configurazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="see-also"></a>Vedere anche  
 [Avviare, arrestare, sospendere, riprendere, riavviare il motore di database, SQL Server Agent o SQL Server Browser](../../database-engine/configure-windows/start-stop-pause-resume-restart-sql-server-services.md)   
 [Configurazione di WMI per mostrare lo stato del server in Strumenti SQL Server](../../ssms/configure-wmi-to-show-server-status-in-sql-server-tools.md)  
  
  
