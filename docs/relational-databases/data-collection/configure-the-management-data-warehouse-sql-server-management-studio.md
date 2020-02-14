---
title: Configurare il data warehouse di gestione (SSMS)
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
f1_keywords:
- sql13.swb.dc.datacollection.wizard_completecfg.f1
- sql13.swb.dc.datacollection.wizard_config.f1
- sql13.swb.dc.datacollection.wizard_finish.f1
- sql13.swb.dc.datacollection.wizard_maploginuser.f1
- sql13.swb.dc.datacollection.wizard_choosemdw.f1
- sql13.swb.dc.datacollection.wizard_welcome.f1
- sql13.swb.dc.datacollection.wizard_createmdw.f1
helpviewer_keywords:
- data warehouse [SQL Server], multiple instances
- data warehouse [SQL Server], configuring
- Configure Management Data Warehouse Wizard
- management data warehouse, configuring
ms.assetid: 23a584f3-c5e1-414c-9afe-73cd7efbda4b
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 54badd0404ee5360aef4a7bc095c236e5b31f79d
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/01/2020
ms.locfileid: "74056468"
---
# <a name="configure-the-management-data-warehouse-sql-server-management-studio"></a>Configurazione del data warehouse di gestione (SQL Server Management Studio)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  In questo argomento viene descritto come configurare il data warehouse di gestione per supportare l'archiviazione dei dati per una singola istanza o per più istanze di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] che utilizzano l'agente di raccolta dati. Queste istanze possono essere installate nello stesso server o in server diversi. In questo argomento vengono fornite anche le descrizioni dell'interfaccia utente per la finestra di dialogo [Configurazione guidata data warehouse di gestione](#Wizard) . Per ulteriori informazioni sulla configurazione di un agente di raccolta dati, vedere [Configure Properties of a Data Collector](../../relational-databases/data-collection/configure-properties-of-a-data-collector.md).  
  
> [!NOTE]  
>  Se [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent è configurato per essere eseguito utilizzando uno degli account di servizio del sistema (Sistema locale, Servizio di rete o Servizio locale) e il data warehouse di gestione viene creato in un'istanza diversa da quella dell'agente di raccolta dati, è necessario configurare i set di raccolta in modo che venga utilizzato un proxy per il caricamento di dati nel data warehouse di gestione.  
  
### <a name="configure-the-management-data-warehouse-on-a-single-instance-or-multiple-instances-of-includessnoversionincludesssnoversion-mdmd"></a>Configurare il data warehouse di gestione su una o più istanze di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
1.  Verificare che [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent sia in esecuzione.  
  
2.  In Esplora oggetti espandere il nodo **Gestione** .  
  
3.  Fare clic con il pulsante destro del mouse **Raccolta dati**, espandere **Attività**e fare clic su **Configura data warehouse di gestione**.  
  
4.  Utilizzare la [Configurazione guidata data warehouse di gestione](#Wizard) per creare un data warehouse di gestione, configurare gli account di accesso, abilitare la raccolta dati e avviare i **Set di raccolta dati di sistema**.  
  
     Per configurare più istanze, continuare con il passaggio 5.  
  
    > [!NOTE]  
    >  Una procedura consigliata consiste nell'utilizzo di proxy in distribuzioni in cui l'agente di raccolta dati è installato su più istanze di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] che si servono dello stesso data warehouse di gestione.  
  
5.  Aprire [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] in un'altra istanza ed effettuare una delle operazioni seguenti:  
  
    -   Utilizzare la Configurazione guidata data warehouse di gestione per configurare la raccolta dati per il data warehouse di gestione esistente.  
  
    -   Fare clic con il pulsante destro del mouse su **Raccolta dati**e scegliere **Proprietà**. Nella scheda **Generale** specificare il data warehouse di gestione esistente e il server in cui è installato.  
  
6.  Ripetere il passaggio 5 fino a quando tutte le istanze del database che utilizzano l'agente di raccolta dati sono configurate per caricare dati sul data warehouse di gestione condiviso.  

####  <a name="Wizard"></a> Configurazione guidata data warehouse di gestione  
 **Pagina introduttiva**  
  
 La pagina iniziale corrisponde alla pagina di avvio di Configurazione guidata raccolta dati e la sua visualizzazione è facoltativa.  
  
 **Non visualizzare più questa pagina iniziale.**  
 Selezionare questa opzione per evitare la visualizzazione di questa pagina al prossimo avvio di Configurazione guidata raccolta dati.  
  
 **Configurazione archiviazione del data warehouse di gestione**  
  
 Utilizzare questa pagina per selezionare un server di database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e un data warehouse di gestione. Il data warehouse di gestione è un database relazionale in cui vengono archiviati i dati raccolti.  
  
> [!NOTE]  
>  Per creare il data warehouse di gestione nel server è necessario disporre del livello adeguato di autorizzazioni. Per alte informazioni, vedere [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md). È inoltre necessario disporre del livello adeguato di autorizzazioni per la creazione degli account di accesso per i ruoli del data warehouse di gestione.  
  
 **Nome server**  
 Consente di specificare il nome del server in cui risiederà il data warehouse di gestione.  
  
 In caso di configurazione di un data warehouse di gestione, **Nome server** è sempre il nome del server locale e non può essere modificato.  
  
 **Nome database**  
 Consente di specificare il database relazionale in cui saranno archiviati i dati raccolti. Utilizzare l'elenco per selezionare un database esistente o fare clic su **Nuovo** per creare un database nuovo mediante la finestra di dialogo **Nuovo database** .  
  
 L'opzione **Nuovo** è disponibile solo in caso di configurazione di un set di raccolta dati.  
  
 **Pagina Mapping account di accesso e utenti**  
  
 Utilizzare questa pagina per eseguire il mapping degli account di accesso ai ruoli utente del database per il data warehouse di gestione.  
  
 **Utenti di cui è stato eseguito il mapping all'account di accesso seguente**  
 Visualizza gli account di accesso esistenti nel server che ospiterà il data warehouse di gestione. Ciascuna riga contiene una casella di controllo **Mapping** modificabile, un nome di **Account di accesso** e un **Tipo** di account di accesso.  
  
 Specificare un account di accesso selezionando la casella di controllo **Mapping** .  
  
 **Appartenenza a ruoli del database per:** *\<nome data warehouse>*  
 Selezionare il ruolo del data warehouse di gestione cui viene eseguito il mapping dell'account di accesso facendo clic nella casella di controllo di una o più delle opzioni seguenti:  
  
-   **mdw_admin**  
  
-   **mdw_reader**  
  
-   **mdw_writer**  
  
 **Nuovo account di accesso**  
 Aprire la finestra di dialogo **Account di accesso - Nuovo** e creare un nuovo account di accesso per il data warehouse di gestione.  
  
 **Pagina Completamento procedura guidata**  
  
 Utilizzare questa pagina per verificare e completare la configurazione della raccolta di dati. L'albero nella finestra di visualizzazione mostra le configurazioni applicate e le azioni eseguite dopo la selezione di **Fine**.  
  
 **Pagina Stato Configurazione guidata raccolta dati**  
  
 Utilizzare questa pagina per visualizzare i risultati di ciascun passaggio di configurazione.  
  
 **Dettagli**  
 Consente di visualizzare ogni passaggio di configurazione in una riga nella griglia **Dettagli** . Ogni riga contiene una colonna **Azione** con la descrizione del passaggio e una colonna **Stato** con l'indicazione dell'esito positivo o negativo dello stesso. In presenza di errori, nella colonna **Messaggio** è visualizzato un messaggio.  
  
 **Stop**  
 Consente di arrestare l'elaborazione della procedura guidata.  
  
 **Report**  
 Consente di visualizzare un report della configurazione di raccolta dati. Sono disponibili le opzioni seguenti:  
  
-   Visualizza report  
  
-   Salva report su file  
  
-   Copia report negli Appunti  
  
-   Invia report per posta elettronica  
  
 **Close**  
 Consente di chiudere la procedura guidata.  
  
## <a name="see-also"></a>Vedere anche  
 [sp_syscollector_enable_collector &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-enable-collector-transact-sql.md)   
 [sp_syscollector_disable_collector &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-disable-collector-transact-sql.md)   
 [Raccolta dati](../../relational-databases/data-collection/data-collection.md)   
 [Gestire raccolta dati](../../relational-databases/data-collection/manage-data-collection.md)  
  
  
