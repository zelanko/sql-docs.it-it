---
description: Aggiungi server di pubblicazione
title: Aggiungi server di pubblicazione | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.monitor.addpublisher.f1
helpviewer_keywords:
- Add Publisher dialog box
ms.assetid: 4b57e298-655f-42c2-82bc-25cdad94a194
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: 1ce82548d63c88565a48d3930c3a7b9a40884413
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88423625"
---
# <a name="add-publisher"></a>Aggiungi server di pubblicazione
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]
  La finestra di dialogo **Aggiungi server di pubblicazione** consente di aggiungere uno o più server di pubblicazione al riquadro sinistro di Monitoraggio replica. Dopo l'aggiunta di un server di pubblicazione, selezionare il server nel riquadro sinistro per visualizzare le informazioni relative nel riquadro destro.  
  
## <a name="options"></a>Opzioni  
 **Aggiungere**  
 Fare clic su questo pulsante per selezionare un tipo di server di pubblicazione da aggiungere. Verrà visualizzata la finestra di dialogo **Connetti al server** . Le opzioni disponibili sono le seguenti:  
  
-   **Aggiungi server di pubblicazione SQL Server**  
  
     Consente di connettersi al server di pubblicazione utilizzando la finestra di dialogo **Connetti al server** .  
  
-   **Aggiungi server di pubblicazione Oracle**  
  
     Consente di connettersi al server di distribuzione [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] associato al server di pubblicazione Oracle usando la finestra di dialogo **Connetti al server**.  
  
-   **Specificare un server di distribuzione e aggiungere i relativi server di pubblicazione**  
  
     Consente di connettersi al server di distribuzione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] associato a uno o più server di pubblicazione utilizzando la finestra di dialogo **Connetti al server** .  
  
 Dopo avere stabilito la connessione al server di pubblicazione o di distribuzione, il nome di ogni server di pubblicazione e il nome del relativo server di distribuzione vengono visualizzati nella griglia posta nella parte superiore della finestra di dialogo.  
  
> [!NOTE]  
>  Il server di distribuzione e il server di pubblicazione vengono spesso eseguiti sulla stessa istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], ma il server di distribuzione può essere eseguito su un'altra istanza. Tale configurazione viene definita server di distribuzione remoto.  
  
 **Rimuovi**  
 Selezionare un server di pubblicazione nella griglia posta nella parte superiore della finestra di dialogo e fare clic su **Rimuovi** per rimuovere il server di pubblicazione dall'elenco dei server di pubblicazione da aggiungere.  
  
> [!NOTE]  
>  Non è possibile utilizzare questo pulsante per rimuovere un server di pubblicazione già visualizzato in Monitoraggio replica. Per rimuovere un server di pubblicazione già visualizzato fare clic con il pulsante destro del mouse sul server di pubblicazione nel riquadro sinistro di Monitoraggio replica e scegliere **Rimuovi**.  
  
 **Connetti automaticamente all'avvio di Monitoraggio replica**  
 Selezionare questa casella di controllo per consentire a Monitoraggio replica di connettersi automaticamente al server di distribuzione e di recuperare informazioni sullo stato del server di pubblicazione selezionato nella griglia posta nella parte superiore della finestra di dialogo. Se questa casella di controllo è deselezionata è necessario connettersi manualmente dopo l'avvio di Monitoraggio replica. Fare clic con il pulsante destro del mouse sul server di pubblicazione visualizzato nel riquadro sinistro di Monitoraggio replica e scegliere **Connetti**.  
  
 **Aggiorna automaticamente lo stato del server di pubblicazione e delle sue pubblicazioni**  
 Selezionare questa opzione per consentire a Monitoraggio replica di aggiornare automaticamente lo stato del server di pubblicazione selezionato nella griglia posta nella parte superiore della finestra di dialogo. Se questa opzione è selezionata, Monitoraggio replica esegue il polling del server di distribuzione per ottenere informazioni sullo stato del server di pubblicazione e delle relative pubblicazioni. L'intervallo di polling viene impostato dall'opzione **Frequenza di aggiornamento** . Per altre informazioni sull'aggiornamento in Monitoraggio replica, vedere [Memorizzazione nella cache, aggiornamento e prestazioni di Monitoraggio replica](../../relational-databases/replication/monitor/caching-refresh-and-replication-monitor-performance.md).  
  
 **Frequenza di aggiornamento**  
 Immettere un valore, espresso in secondi, per specificare la frequenza di polling del server di distribuzione per ottenere informazioni sullo stato da parte di Monitoraggio replica. Valori inferiori indicano un polling più frequente, che influisce sulle prestazioni del server di distribuzione se il monitoraggio include un numero elevato di server di pubblicazione. È consigliabile eseguire prove sul sistema per determinare un valore appropriato. L'impostazione **Frequenza di aggiornamento** viene utilizzata anche se si seleziona **Aggiornamento automatico** in una delle finestre dei dettagli di Monitoraggio replica.  
  
 **Mostra server di pubblicazione nel gruppo seguente**  
 Selezionare un gruppo di server di pubblicazione nell'elenco. Il server di pubblicazione viene visualizzato in questo gruppo nel riquadro sinistro. I gruppi consentono di organizzare i server di pubblicazione e non influiscono sul funzionamento della replica. Se non sono definiti gruppi o si desidera creare un nuovo gruppo fare clic su **Nuovo gruppo**.  
  
 **Nuovo gruppo**  
 Fare clic su questa opzione per creare un nuovo gruppo di server di pubblicazione. Un gruppo di server di pubblicazione consente di organizzare facilmente i server di pubblicazione all'interno di Monitoraggio replica. I gruppi non influiscono sulla replica dei dati o sulla relazione tra i server in una topologia di replica.  
  
## <a name="see-also"></a>Vedere anche  
 [Avviare Monitoraggio replica](../../relational-databases/replication/monitor/start-the-replication-monitor.md)   
 [Monitoraggio della replica](../../relational-databases/replication/monitor/monitoring-replication.md)  
  
  
