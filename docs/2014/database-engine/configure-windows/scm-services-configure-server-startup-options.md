---
title: Configurazione delle opzioni di avvio del server (Gestione configurazione SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 01/07/2016
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- parameters [SQL Server], startup options
- SQL Server, startup options
- single-user mode [SQL Server], starting in
- startup options [SQL Server]
- SQL Server services, setting startup options
ms.assetid: 7a94643c-6460-4baf-bb31-0cb99eaf970d
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 91a48d4acd771c19617bac26c1393f30334768e8
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "62810369"
---
# <a name="configure-server-startup-options-sql-server-configuration-manager"></a>Configurazione delle opzioni di avvio del server (Gestione configurazione SQL Server)
  Questo argomento illustra come configurare le opzioni di avvio da usare ogni volta che il [!INCLUDE[ssDE](../../includes/ssde-md.md)] viene avviato in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] tramite [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager. Per un elenco delle opzioni di avvio, vedere [Opzioni di avvio del servizio del motore di database](database-engine-service-startup-options.md).  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Prima di iniziare  
  
### <a name="limitations-and-restrictions"></a>Limitazioni e restrizioni  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , i parametri di avvio vengono scritti nel Registro di sistema e vengono applicati al successivo avvio del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
 In un cluster le modifiche devono essere eseguite sul server attivo quando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è online e verranno applicate al riavvio di [!INCLUDE[ssDE](../../includes/ssde-md.md)] . L'aggiornamento delle opzioni di avvio nel Registro di sistema per l'altro nodo verrà eseguito al successivo failover.  
  
###  <a name="security"></a><a name="Security"></a> Sicurezza  
  
####  <a name="permissions"></a><a name="Permissions"></a> Autorizzazioni  
 La configurazione delle opzioni di avvio del server è limitata a utenti che possono modificare le voci correlate nel Registro di sistema. Sono inclusi gli utenti indicati di seguito.  
  
-   Membri del gruppo Administrators locale.  
  
-   Account di dominio utilizzato da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], se il [!INCLUDE[ssDE](../../includes/ssde-md.md)] è configurato per essere in esecuzione in un account di dominio.  
  
##  <a name="using-sql-server-configuration-manager"></a><a name="SSMSProcedure"></a> Utilizzo di Gestione configurazione SQL Server  
  
#### <a name="to-configure-startup-options"></a>Per configurare le opzioni di avvio  
  
1.  In Gestione configurazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fare clic su **Servizi di SQL Server**.  
  
    > [!NOTE]  
    >  Poiché Gestione configurazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è uno snap-in per il programma [!INCLUDE[msCoName](../../includes/msconame-md.md)] Management Console e non un programma autonomo, Gestione configurazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non viene visualizzato come applicazione nelle versioni più recenti di Windows.  
    >   
    >  -   **Windows 10**:  
    >          Per aprire [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager, nella **pagina iniziale**digitare SQLServerManager12. msc (per [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]). Per le versioni precedenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , sostituire 12 con un numero inferiore. Se si fa clic su SQLServerManager12.msc, viene aperto Gestione configurazione. Per aggiungere la Configuration Manager alla pagina iniziale o alla barra delle applicazioni, fare clic con il pulsante destro del mouse su SQLServerManager12. msc, quindi scegliere **Apri percorso file**. In Esplora file di Windows fare clic con il pulsante destro del mouse su SQLServerManager12. msc, quindi scegliere **Aggiungi a Start** o **Aggiungi alla barra delle applicazioni**.  
    > -   **Windows 8**:  
    >          Per aprire [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager, nell'accesso alla **ricerca** in **app**digitare **SQLServerManager\<Version>. msc** , ad esempio `SQLServerManager12.msc`, quindi premere **invio**.  
  
2.  Nel riquadro destro fare clic con il pulsante destro del mouse su **SQL Server(***<nome_istanza>***)** e quindi scegliere **Proprietà**.  
  
3.  Nella scheda **Parametri di avvio** della casella **Specificare un parametro di avvio** digitare il parametro e quindi fare clic su **Aggiungi**.  
  
     Ad esempio, per avviare in modalità utente singolo, digitare `-m` nella casella **specificare un parametro di avvio** e quindi fare clic su **Aggiungi**. Al riavvio di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in modalità utente singolo, arrestare [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. In caso contrario, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent potrebbe eseguire per primo la connessione impedendo la connessione come secondo utente.  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
5.  Riavviare il [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
    > [!WARNING]  
    >  Al termine dell'utilizzo della modalità utente singolo, nella casella parametri di avvio selezionare il `-m` parametro nella casella **parametri esistenti** , quindi fare clic su **Rimuovi**. Riavviare [!INCLUDE[ssDE](../../includes/ssde-md.md)] per ripristinare [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nella modalità tipica multiutente.  
  
## <a name="see-also"></a>Vedi anche  
 [Avviare SQL Server in modalità utente singolo](start-sql-server-in-single-user-mode.md)   
 [Connetti a SQL Server quando gli amministratori di sistema sono bloccati](connect-to-sql-server-when-system-administrators-are-locked-out.md)   
 [Start, Stop, or Pause the SQL Server Agent Service](../../ssms/agent/start-stop-or-pause-the-sql-server-agent-service.md)  
  
  
