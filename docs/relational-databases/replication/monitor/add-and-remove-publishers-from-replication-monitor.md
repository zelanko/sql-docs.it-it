---
title: Aggiungere e rimuovere server di pubblicazione da Monitoraggio replica (SSMS)
description: Informazioni su come aggiungere e rimuovere server di pubblicazione da Monitoraggio replica in SQL Server Management Studio (SSMS).
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- Replication Monitor, adding and removing Publishers
ms.assetid: fa36c4b4-bfa5-494e-92e3-07a02d7332c3
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: 08857f964f652c5663cda32ce442cf34e201c80c
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/22/2020
ms.locfileid: "86907287"
---
# <a name="add-and-remove-publishers-from-replication-monitor"></a>Aggiunta e rimozione di server di pubblicazione da Monitoraggio replica
[!INCLUDE[sql-asdbmi](../../../includes/applies-to-version/sql-asdbmi.md)]
  Se il server dal quale viene avviato Monitoraggio replica è un server di pubblicazione, quest'ultimo verrà automaticamente aggiunto al monitoraggio. È possibile aggiungere ulteriori server di pubblicazione tramite la finestra di dialogo **Aggiungi server di pubblicazione** . Dopo l'aggiunta di un server di pubblicazione, questo viene visualizzato in un gruppo di server nel riquadro sinistro di Monitoraggio replica. Il gruppo **Server di pubblicazione personali** è incluso per impostazione predefinita. Tuttavia è possibile creare nuovi gruppi per gestire una o più topologie di replica. Per informazioni sull'avvio di Monitoraggio replica, vedere [Avviare Monitoraggio replica](../../../relational-databases/replication/monitor/start-the-replication-monitor.md).  
  
### <a name="to-add-a-sql-server-publisher"></a>Per aggiungere un server di pubblicazione SQL Server  
  
1.  Fare clic con il pulsante destro del mouse sul nodo **Monitoraggio replica** oppure sul nodo di un gruppo di server di pubblicazione nel riquadro sinistro e quindi scegliere **Aggiungi server di pubblicazione**.  
  
2.  Nella finestra di dialogo **Aggiungi server di pubblicazione** fare clic su **Aggiungi**e quindi su **Aggiungi server di pubblicazione SQL Server**.  
  
3.  Nella finestra di dialogo **Connetti al server** immettere il nome del server di pubblicazione e quindi selezionare il tipo di autenticazione. Se si seleziona **Autenticazione di SQL Server**, specificare un account di accesso e la relativa password. Le credenziali specificate vengono salvate da Monitoraggio replica per poterle utilizzare per le connessioni future a questo server. L'account di Windows o l'account di accesso di SQL Server specificato deve essere un membro del ruolo predefinito del server **sysadmin** o del ruolo predefinito del database **replmonitor** nel database di distribuzione.  
  
4.  Fare clic su **Connetti**. Se il server di pubblicazione utilizza un server di distribuzione remoto, verrà richiesto di connettersi al server di distribuzione nella finestra di dialogo **Connetti al server** . Le credenziali specificate vengono salvate da Monitoraggio replica per poterle utilizzare per le connessioni future a questo server. L'account di Windows o l'account di accesso di SQL Server specificato deve essere un membro del ruolo predefinito del server **sysadmin** o del ruolo predefinito del database **replmonitor** nel database di distribuzione.  
  
5.  Il nome del server di pubblicazione e il nome del server di distribuzione vengono visualizzati nella griglia **Avvia il monitoraggio dei server di pubblicazione seguenti** .  
  
6.  Per specificare le opzioni di aggiornamento e connessione del server di pubblicazione, selezionare il server nella griglia e modificare le opzioni in base alle necessità. Per ulteriori informazioni sulle opzioni di aggiornamento, vedere [Caching, Refresh, and Replication Monitor Performance](../../../relational-databases/replication/monitor/caching-refresh-and-replication-monitor-performance.md).  
  
7.  Selezionare il gruppo all'interno del quale deve essere visualizzato il server di pubblicazione in Monitoraggio replica. Per creare un nuovo gruppo, fare clic su **Nuovo gruppo**e quindi specificare un nome per il gruppo. Al termine, selezionare il gruppo dall'elenco **Mostra server di pubblicazione nel gruppo seguente** .  
  
8.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
### <a name="to-add-an-oracle-publisher"></a>Per aggiungere un server di pubblicazione Oracle  
  
1.  Fare clic con il pulsante destro del mouse sul nodo **Monitoraggio replica** oppure sul nodo di un gruppo di server di pubblicazione nel riquadro sinistro e quindi scegliere **Aggiungi server di pubblicazione**.  
  
2.  Nella finestra di dialogo **Aggiungi server di pubblicazione** fare clic su **Aggiungi**e quindi su **Aggiungi server di pubblicazione Oracle**.  
  
3.  Nella finestra di dialogo **Connetti al server** immettere il nome del server di distribuzione [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] associato al server di pubblicazione Oracle e quindi selezionare il tipo di autenticazione. Se si seleziona **Autenticazione di SQL Server**, specificare un account di accesso e la relativa password. Le credenziali specificate vengono salvate da Monitoraggio replica per poterle utilizzare per le connessioni future a questo server. L'account di Windows o l'account di accesso di SQL Server specificato deve essere un membro del ruolo predefinito del server **sysadmin** o del ruolo predefinito del database **replmonitor** nel database di distribuzione.  
  
4.  Fare clic su **Connetti**.  
  
5.  Il nome del server di pubblicazione e il nome del server di distribuzione vengono visualizzati nella griglia **Avvia il monitoraggio dei server di pubblicazione seguenti** .  
  
6.  Per specificare le opzioni di aggiornamento e connessione del server di pubblicazione, selezionare il server nella griglia e modificare le opzioni in base alle necessità. Per ulteriori informazioni sulle opzioni di aggiornamento, vedere [Caching, Refresh, and Replication Monitor Performance](../../../relational-databases/replication/monitor/caching-refresh-and-replication-monitor-performance.md).  
  
7.  Selezionare il gruppo all'interno del quale deve essere visualizzato il server di pubblicazione in Monitoraggio replica. Per creare un nuovo gruppo, fare clic su **Nuovo gruppo**e quindi specificare un nome per il gruppo. Al termine, selezionare il gruppo dall'elenco **Mostra server di pubblicazione nel gruppo seguente** .  
  
8.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
### <a name="to-add-one-or-more-publishers-that-use-the-same-distributor"></a>Per aggiungere uno o più server di pubblicazione che utilizzano lo stesso server di distribuzione  
  
1.  Fare clic con il pulsante destro del mouse sul nodo **Monitoraggio replica** oppure sul nodo di un gruppo di server di pubblicazione nel riquadro sinistro e quindi scegliere **Aggiungi server di pubblicazione**.  
  
2.  Nella finestra di dialogo **Aggiungi server di pubblicazione** fare clic su **Aggiungi**e quindi su **Specificare un server di distribuzione e aggiungere i relativi server di pubblicazione**.  
  
3.  Nella finestra di dialogo **Connetti al server** immettere il nome del server di distribuzione e quindi selezionare il tipo di autenticazione. Se si seleziona **Autenticazione di SQL Server**, specificare un account di accesso e la relativa password. Le credenziali specificate vengono salvate da Monitoraggio replica per poterle utilizzare per le connessioni future a questo server. L'account di Windows o l'account di accesso di SQL Server specificato deve essere un membro del ruolo predefinito del server **sysadmin** o del ruolo predefinito del database **replmonitor** nel database di distribuzione.  
  
4.  Fare clic su **Connetti**.  
  
5.  Il nome del server di distribuzione e di ogni server di pubblicazione vengono visualizzati nella griglia **Avvia il monitoraggio dei server di pubblicazione seguenti** . Se un server di pubblicazione è già stato aggiunto a Monitoraggio replica, non verrà visualizzato nella griglia.  
  
6.  Per specificare le opzioni di aggiornamento e connessione del server di pubblicazione, selezionare il server nella griglia e modificare le opzioni in base alle necessità. Per ulteriori informazioni sulle opzioni di aggiornamento, vedere [Caching, Refresh, and Replication Monitor Performance](../../../relational-databases/replication/monitor/caching-refresh-and-replication-monitor-performance.md).  
  
7.  Selezionare il gruppo all'interno del quale devono essere visualizzati i server di pubblicazione in Monitoraggio replica. Per creare un nuovo gruppo, fare clic su **Nuovo gruppo**e quindi specificare un nome per il gruppo. Al termine, selezionare il gruppo dall'elenco **Mostra server di pubblicazione nel gruppo seguente** .  
  
8.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
### <a name="to-modify-settings-for-the-publisher-and-publisher-groups"></a>Per modificare le impostazioni del server di pubblicazione e dei gruppi di server di pubblicazione  
  
1.  Fare clic con il pulsante destro del mouse su un server di pubblicazione nel riquadro sinistro e quindi scegliere **Impostazioni server di pubblicazione**.  
  
2.  Apportare le modifiche desiderate nella finestra di dialogo **Impostazioni server di pubblicazione** :  
  
    -   Per modificare le credenziali utilizzate da Monitoraggio replica per la connessione al server, fare clic su **Connessione server di pubblicazione** o su **Connessione server di distribuzione**e nella finestra di dialogo **Connetti al server** immettere le nuove credenziali.  
  
    -   Per spostare un server di pubblicazione da un gruppo a un altro, selezionare il server di pubblicazione nella griglia **Avvia il monitoraggio dei server di pubblicazione seguenti** e quindi selezionare il nuovo gruppo nell'elenco **Mostra server di pubblicazione nel gruppo seguente** .  
  
3.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
### <a name="to-remove-a-publisher-from-replication-monitor"></a>Per rimuovere un server di pubblicazione da Monitoraggio replica  
  
1.  Fare clic con il pulsante destro del mouse su un server di pubblicazione nel riquadro sinistro.  
  
2.  Scegliere **Rimuovi**.  
  
### <a name="to-add-a-publisher-group-to-replication-monitor"></a>Per aggiungere un gruppo di server di pubblicazione a Monitoraggio replica  
  
1.  È possibile creare gruppi di server di pubblicazione solo quando si aggiunge un server di pubblicazione o si modificano le impostazioni di un server di pubblicazione. Per ulteriori informazioni, vedere le procedure relative all'aggiunta di un server di pubblicazione.  
  
### <a name="to-remove-a-publisher-group-from-replication-monitor"></a>Per rimuovere un gruppo di server di pubblicazione da Monitoraggio replica  
  
1.  Spostare tutti i server di pubblicazione in un gruppo diverso oppure rimuoverli da Monitoraggio replica. Per ulteriori informazioni, vedere le procedure precedenti in questo argomento.  
  
2.  Fare clic con il pulsante destro del mouse sul gruppo di server di pubblicazione e quindi scegliere **Rimuovi**.  
  
## <a name="see-also"></a>Vedere anche  
 [Configura distribuzione](../../../relational-databases/replication/configure-distribution.md)   
 [Monitoraggio della replica](../../../relational-databases/replication/monitor/monitoring-replication.md)  
  
  
