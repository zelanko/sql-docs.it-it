---
title: Avvisi (Snapshot - Monitoraggio replica)
decription: Describes the 'Warnings' tab for a Snapshot Publication in the Replication Monitor found in SQL Server Management Studio (SSMS).
ms.custom: seo-lt-2019
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.monitor.publicationinfo.warningsandagents.snapshot.f1
ms.assetid: 7aa2eb52-b6b7-4dd3-8483-8ef00d9f0435
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: db9b32625cf31f5a632eef1234e7f01110c46727
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/01/2020
ms.locfileid: "76286610"
---
# <a name="publication-information-warnings-snapshot-publication-sql-server-2005-and-later"></a>Informazioni sulla pubblicazione, Avvisi (pubblicazione snapshot, SQL Server 2005 e versioni successive)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  La scheda **Avvisi** è disponibile per i server di distribuzione che eseguono [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e versioni successive. La scheda **Avvisi** consente di eseguire le attività seguenti per la pubblicazione selezionata:  
  
-   Abilitazione di avvisi.  
  
-   Specificare valori soglia associati agli avvisi.  
  
-   Definire messaggi di avviso associati ad avvisi.  
  
## <a name="warnings-thresholds-and-alerts"></a>Avvisi, soglie e messaggi di avviso  
 Per impostazione predefinita, Monitoraggio replica visualizza avvisi per le sottoscrizioni non inizializzate, includendo lo stato **Sottoscrizione non inizializzata** come avviso nella colonna **Stato** delle pagine contenenti informazioni sulla sottoscrizione. Per le pubblicazioni snapshot, è inoltre possibile specificare che l'imminente scadenza della sottoscrizione venga notificata tramite un avviso impostando l'opzione **Avvisa se una sottoscrizione scade entro il valore soglia**. Se il valore soglia specificato viene raggiunto o superato, lo stato della sottoscrizione viene visualizzato come **Scadenza imminente/Scaduta** , a meno che non sia necessario visualizzare un problema con una priorità più alta.  
  
 Oltre a visualizzare un avviso in Monitoraggio replica, il raggiungimento di un valore soglia può inoltre attivare un messaggio di avviso. Gli avvisi vengono definiti facendo clic su **Configura avvisi** e specificando le informazioni appropriate nella finestra di dialogo **Configura avvisi di replica** .  
  
## <a name="options"></a>Opzioni  
 **Enabled**  
 Selezionare questa opzione per abilitare un avviso e specificare un valore soglia.  
  
 **Warning**  
 Descrizione dell'avviso associato al valore soglia.  
  
 **Soglia**  
 Consente di specificare un valore per la soglia.  
  
 **Configura avvisi**  
 Selezionare una riga nella griglia **Avvisi** e fare clic su **Configura avvisi** per aprire la finestra di dialogo **Configura avvisi di replica** . Tramite questa finestra di dialogo è possibile definire un avviso associato al valore soglia e all'avviso selezionati.  
  
 **Ignora modifiche**  
 Fare clic su questo pulsante per ignorare le eventuali modifiche apportate agli avvisi e alle soglie.  
  
> [!NOTE]  
>  La scelta del pulsante **Ignora modifiche** non influisce sugli avvisi definiti nella finestra di dialogo **Configura avvisi di replica** .  
  
 **Salva modifiche**  
 Fare clic su questo pulsante per salvare le eventuali modifiche apportate agli avvisi e alle soglie.  
  
## <a name="see-also"></a>Vedere anche  
 [Avviare Monitoraggio replica](../../relational-databases/replication/monitor/start-the-replication-monitor.md)   
 [Visualizzare le informazioni ed eseguire attività usando Monitoraggio replica](../../relational-databases/replication/monitor/view-information-and-perform-tasks-replication-monitor.md)   
 [Monitoraggio della replica](../../relational-databases/replication/monitor/monitoring-replication.md)  
  
  
