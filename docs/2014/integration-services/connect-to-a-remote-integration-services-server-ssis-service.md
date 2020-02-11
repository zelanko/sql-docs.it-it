---
title: Connettersi a un server di Integration Services remoto (servizio SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- service [Integration Services], remote instance
- Integration Services service, connecting
- Integration Services service, remote instance
- service [Integration Services], connecting
ms.assetid: 9487aff1-44d8-42c1-8176-bb9891d4632d
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: e0e7e62510338b9dd47d59ce50626ecffebfcf85
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66060417"
---
# <a name="connect-to-a-remote-integration-services-server-ssis-service"></a>Eseguire una connessione a un server Integration Services remoto (servizio SSIS)
    
> [!IMPORTANT] 
> In questo argomento viene illustrato il servizio [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] , un servizio Windows per la gestione dei pacchetti di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] . [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]supporta il servizio per la compatibilità con le versioni precedenti [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]di. A partire da [!INCLUDE[ssSQL11](../includes/sssql11-md.md)], è possibile gestire oggetti come i pacchetti del server Integration Services.  
  
 Per la connessione a un'istanza di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] in un server remoto da [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] o da un'altra applicazione di gestione, è necessario un set specifico di diritti nel server per gli utenti dell'applicazione.  
  
> [!IMPORTANT] 
> Per gestire i pacchetti archiviati in un server remoto, non è necessario connettersi all'istanza del servizio [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] sul server remoto in questione. Modificare, invece, il file di configurazione per il servizio [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] in modo che in [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] vengano visualizzati i pacchetti archiviati nel server remoto. Per altre informazioni, vedere [Configurazione del servizio Integration Services &#40;servizio SSIS&#41;](service/integration-services-service-ssis-service.md).  
  
## <a name="connecting-to-integration-services-on-a-remote-server"></a>Connessione a Integration Services in un server remoto  
  
#### <a name="to-connect-to-integration-services-on-a-remote-server"></a>Per connettersi a Integration Services in un server remoto  
  
1.  Aprire [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)].  
  
2.  Scegliere **Connetti Esplora oggetti**dal menu **File** per visualizzare la finestra di dialogo **Connetti al server** .  
  
3.  Nell'elenco **Tipo server** selezionare **Integration Services** .  
  
4.  Nella casella di testo [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] digitare il nome di un server di **** .  
  
    > [!NOTE]  
    >  Il servizio [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] non è specifico dell'istanza. Connettersi al servizio utilizzando il nome del computer sul quale è in esecuzione Integration Services.  
  
5.  Fare clic su **Connetti**.  
  
> [!NOTE]  
>  Nella finestra di dialogo **Cerca server** non vengono visualizzate le istanze remote di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]. Le opzioni disponibili nella scheda **Opzioni di connessione** della finestra di dialogo **Connetti al server** , visualizzata facendo clic sul pulsante **Opzioni** , non sono inoltre applicabili alle connessioni a [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] .  
  
## <a name="eliminating-the-access-is-denied-error"></a>Eliminazione dell'errore "Accesso negato"  
 Quando un utente che non dispone di diritti sufficienti tenta di connettersi a un'istanza di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] in un server remoto, viene visualizzato un errore di accesso negato. È possibile evitare la visualizzazione di questo messaggio di errore verificando che gli utenti dispongano delle autorizzazioni DCOM necessarie.  
  
#### <a name="to-configure-rights-for-remote-users-on-windows-server-2003-or-windows-xp"></a>Per configurare i diritti per gli utenti remoti in Windows Server 2003 o Windows XP  
  
1.  Se l'utente non è membro del gruppo Administrators locale, aggiungerlo al gruppo di utenti DCOM. A questo scopo, è possibile usare lo snap-in MMC Gestione computer, a cui è possibile accedere dal menu **Strumenti di amministrazione** .  
  
2.  Aprire il Pannello di controllo, fare clic su **Strumenti di amministrazione** e quindi fare doppio clic su **Servizi componenti** per avviare lo snap-in MMC Servizi componenti.  
  
3.  Espandere il nodo **Servizi componenti** nel riquadro a sinistra della console. Espandere il nodo **Computer** , espandere il nodo **Risorse del computer**, quindi fare clic sul nodo **Config DCOM** .  
  
4.  Selezionare il nodo **Config DCOM** , quindi selezionare SQL Server Integration Services 11.0 nell'elenco di applicazioni che è possibile configurare.  
  
5.  Fare clic con il pulsante destro del mouse su SQL Server Integration Services 11.0 e scegliere **Proprietà**.  
  
6.  Nella finestra di dialogo **Proprietà - SQL Server Integration Services 11.0** selezionare la scheda **Sicurezza** .  
  
7.  In **Autorizzazioni di esecuzione e attivazione**selezionare **Personalizza**, quindi fare clic su **Modifica** per aprire la finestra di dialogo **Autorizzazione di avvio** .  
  
8.  Nella finestra di dialogo **Autorizzazione di avvio** aggiungere o eliminare utenti e assegnare le autorizzazioni appropriate agli utenti e ai gruppi desiderati. Le autorizzazioni disponibili sono Avvio locale, Avvio remoto, Attivazione locale e Attivazione remota. I diritti di avvio consentono di concedere o negare l'autorizzazione per l'avvio e l'arresto del servizio, mentre quelli di attivazione consentono di concedere o negare l'autorizzazione per la connessione al servizio.  
  
9. Fare clic su OK per chiudere la finestra di dialogo.  
  
10. In **Autorizzazioni di accesso**, ripetere i passaggi 7 e 8 per assegnare le autorizzazioni appropriate a utenti e gruppi.  
  
11. Chiudere lo snap-in MMC.  
  
12. Riavviare il servizio [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] .  
  
#### <a name="to-configure-rights-for-remote-users-on-windows-2000-with-the-latest-service-packs"></a>Per configurare i diritti per gli utenti remoti in Windows 2000 con il Service Pack più recente  
  
1.  Eseguire **dcomcnfg.exe** al prompt dei comandi.  
  
2.  Nella pagina **Applicazioni** della finestra di dialogo **Proprietà - Configurazione Distributed COM** selezionare SQL Server Integration Services 11.0, quindi fare clic su **Proprietà**.  
  
3.  Selezionare la pagina **Sicurezza** .  
  
4.  Utilizzare le due finestre di dialogo separate per la configurazione delle **Autorizzazioni di accesso** e delle **Autorizzazioni di avvio**. Non è possibile fare distinzione tra l'accesso remoto e quello locale. Le autorizzazioni di accesso includono l'accesso remoto e locale e quelle di avvio includono l'avvio remoto e locale.  
  
5.  Chiudere le finestre di dialogo e **dcomcnfg.exe**.  
  
6.  Riavviare il servizio [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] .  
  
## <a name="connecting-by-using-a-local-account"></a>Connessione tramite un account locale  
 Se si utilizza un account di Windows locale in un computer client, è possibile connettersi al servizio [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] in un computer remoto solo se nel computer remoto è presente un account locale con lo stesso nome, la stessa password e i diritti appropriati.  
  
## <a name="by-default-the-ssis-service-does-not-support-delegation"></a>Per impostazione predefinita, il servizio SSIS non supporta la delega  
Per impostazione predefinita [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] , il servizio non supporta la delega delle credenziali o ciò che viene talvolta definito come doppio hop. In questo scenario si usa un computer client, il servizio [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] è in esecuzione in un secondo computer e [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] è in esecuzione in un terzo computer. Prima di tutto, [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] passa le credenziali dal computer client al secondo computer in cui è in esecuzione il servizio [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] . Dopo, tuttavia, il servizio [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] non può delegare le credenziali dal secondo computer al terzo computer in cui è in esecuzione [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .

È possibile abilitare la delega delle credenziali concedendo il diritto **Utente attendibile per la delega a qualsiasi servizio (solo Kerberos)** all'account del servizio SQL Server, che consente di avviare il servizio Integration Services (ISServerExec.exe) come processo figlio. Prima di concedere questo diritto, valutare se soddisfa i requisiti di sicurezza dell'organizzazione.

Per altre informazioni, vedere [Getting Cross Domain Kerberos and Delegation working with SSIS Package](https://blogs.msdn.microsoft.com/psssql/2014/06/26/getting-cross-domain-kerberos-and-delegation-working-with-ssis-package/)(Supporto di Kerberos e della delega tra domini con il pacchetto SSIS).
  
## <a name="see-also"></a>Vedere anche  
 [Configurare un Windows Firewall per l'accesso al servizio SSIS](../../2014/integration-services/configure-a-windows-firewall-for-access-to-the-ssis-service.md)  
  
  
