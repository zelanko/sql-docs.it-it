---
title: Configurare gli avvisi di replica predefiniti (SSMS)
description: Informazioni su come configurare gli avvisi di replica predefiniti usando SQL Server Management Studio (SSMS).
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- alerts [SQL Server replication]
- predefined replication alerts [SQL Server replication]
ms.assetid: c0414147-7ffe-4f9a-908c-71c1b5201584
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: b3d02391f8a0423b46e18298b997e0de3623651b
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/30/2020
ms.locfileid: "76516512"
---
# <a name="configure-predefined-replication-alerts-sql-server-management-studio"></a>Configurazione degli avvisi di replica predefiniti (SQL Server Management Studio)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md.md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  La replica offre gli avvisi predefiniti seguenti, configurabili in risposta a eventi di replica:  
  
-   **Replica: operazione dell'agente riuscita**  
  
-   **Replica: errore dell'agente**  
  
-   **Replica: nuovo tentativo dell'agente**  
  
-   **Replica: eliminata sottoscrizione scaduta**  
  
-   **Replica: la sottoscrizione è stata reinizializzata dopo l'errore di convalida**  
  
-   **Replica: la convalida dei dati nel Sottoscrittore non è riuscita**  
  
-   **Replica: la convalida dei dati nel Sottoscrittore è riuscita**  
  
-   **Replica: arresto dell'agente personalizzato**  
  
 Configurare questi avvisi nella cartella **Avvisi** in [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] o nella scheda **Avvisi** in Monitoraggio replica. Per altre informazioni sull'accesso a questa scheda, vedere [Visualizzare le informazioni ed eseguire attività usando Monitoraggio replica](../../../relational-databases/replication/monitor/view-information-and-perform-tasks-replication-monitor.md).  
  
 In aggiunta a questi avvisi, in Monitoraggio replica è disponibile un set di avvisi relativi allo stato e alle prestazioni. Per altre informazioni, vedere [Set Thresholds and Warnings in Replication Monitor](../../../relational-databases/replication/monitor/set-thresholds-and-warnings-in-replication-monitor.md). È inoltre possibile definire avvisi per altri eventi di replica utilizzando l'infrastruttura degli avvisi di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Per altre informazioni, vedere [Creare un evento definito dall'utente](https://msdn.microsoft.com/library/03d71a35-97fa-4bba-aa9a-23ac9c9cf879).  
  
### <a name="to-configure-a-predefined-replication-alert-in-management-studio"></a>Per configurare un avviso di replica predefinito in Management Studio  
  
1.  Connettersi al database di distribuzione in [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)], quindi espandere il nodo del server.  
  
2.  Espandere la cartella **SQL Server Agent** e quindi la cartella **Avvisi** .  
  
3.  Fare clic con il pulsante destro del mouse su un avviso di replica e quindi scegliere **Proprietà**.  
  
4.  Impostare le opzioni nella finestra di dialogo **Proprietà dell'avviso \<NomeAvviso>** :  
  
    -   Nella pagina **Generale** fare clic su **Abilita**e specificare il database a cui si desidera applicare l'avviso.  
  
    -   Nella pagina **Risposta** specificare se si desidera inviare un messaggio di posta elettronica e/o eseguire un processo.  
  
         Se l'avviso è **Replica: la convalida dei dati nel Sottoscrittore non è riuscita**, è possibile specificare il processo di risposta della replica per questo avviso: Selezionare **Esegui processo** e quindi fare clic sul pulsante Sfoglia ( **...** ). Nella finestra di dialogo **Individua processo** fare clic su **Sfoglia**. Nella finestra di dialogo **Cerca oggetti** selezionare **Reinizializzazione delle sottoscrizioni con errori di convalida dei dati**. Fare clic su **OK** in entrambe le finestre di dialogo aperte. Durante l'esecuzione il processo utilizza una chiamata di procedura remota (RPC) a una stored procedure che reinizializza la sottoscrizione. Se il server di pubblicazione utilizza un server di distribuzione remoto, è necessario definire un account di accesso al server remoto sul server di pubblicazione in modo che sia possibile eseguire la chiamata di procedura remota (RPC) dal server di distribuzione al server di pubblicazione.  
  
    -   Nella pagina **Opzioni** personalizzare il testo della risposta.  
  
5.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  

### <a name="to-configure-an-alert-for-a-threshold-in-replication-monitor"></a>Per configurare un avviso per una soglia in Monitoraggio replica  
  
1.  Nella scheda **Avvisi** fare clic su **Configura avvisi**.  
  
2.  Nella finestra di dialogo **Configura avvisi di replica** selezionare un avviso e quindi fare clic su **Configura**.  
  
3.  Impostare le opzioni nella finestra di dialogo **Proprietà dell'avviso \<NomeAvviso>** :  
  
    -   Nella pagina **Generale** fare clic su **Abilita**e specificare il database a cui si desidera applicare l'avviso.  
  
    -   Nella pagina **Risposta** specificare se si desidera inviare un messaggio di posta elettronica e/o eseguire un processo.  
  
         Se l'avviso è **Replica: la convalida dei dati nel Sottoscrittore non è riuscita**, è possibile specificare il processo di risposta della replica per questo avviso: Selezionare **Esegui processo** e quindi fare clic sul pulsante Sfoglia ( **...** ). Nella finestra di dialogo **Individua processo** fare clic su **Sfoglia**. Nella finestra di dialogo **Cerca oggetti** selezionare **Reinizializzazione delle sottoscrizioni con errori di convalida dei dati**. Fare clic su **OK** in entrambe le finestre di dialogo aperte. Durante l'esecuzione il processo utilizza una chiamata di procedura remota (RPC) a una stored procedure che reinizializza la sottoscrizione. Se il server di pubblicazione utilizza un server di distribuzione remoto, è necessario definire un account di accesso al server remoto sul server di pubblicazione in modo che sia possibile eseguire la chiamata di procedura remota (RPC) dal server di distribuzione al server di pubblicazione.  
  
    -   Nella pagina **Opzioni** personalizzare il testo della risposta.  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
5.  Fare clic su **Close**.  
  
## <a name="see-also"></a>Vedere anche  
 [Usare gli avvisi per gli eventi degli agenti di replica](../../../relational-databases/replication/agents/use-alerts-for-replication-agent-events.md)  
  
  
