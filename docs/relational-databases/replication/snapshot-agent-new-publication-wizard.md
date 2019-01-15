---
title: Agente snapshot (Creazione guidata nuova pubblicazione) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.newpubwizard.configuresnapshotagent.f1
ms.assetid: 0257d4ee-1f7b-49fd-b4ef-65bfc1ef6951
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 074b0932f97c168a8d2250c057ac246785bf2dd0
ms.sourcegitcommit: 7aa6beaaf64daf01b0e98e6c63cc22906a77ed04
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/09/2019
ms.locfileid: "54126151"
---
# <a name="snapshot-agent-new-publication-wizard"></a>Agente snapshot (Creazione guidata nuova pubblicazione)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  L'agente snapshot crea file contenenti lo schema della pubblicazione e i dati utilizzati per inizializzare nuove sottoscrizioni. Per impostazione predefinita, l'agente snapshot viene eseguito immediatamente dopo la creazione della pubblicazione mediante Creazione guidata nuova pubblicazione. L'agente verrà successivamente eseguito in base alla pianificazione impostata dall'utente. L'eventuale creazione di nuovi file di snapshot a ogni esecuzione dell'agente dipende dal tipo di replica e dalle opzioni scelte. Per altre informazioni, vedere [Creare e applicare lo snapshot](../../relational-databases/replication/create-and-apply-the-initial-snapshot.md).  
  
 Per le pubblicazioni di tipo merge che utilizzano filtri con parametri, è necessario creare uno snapshot per ogni partizione di dati dopo il completamento dello snapshot di pubblicazione. Per altre informazioni, vedere [Snapshots for Merge Publications with Parameterized Filters](../../relational-databases/replication/create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md).  
  
## <a name="options"></a>Opzioni  
 **Crea snapshot immediatamente** (replica di tipo merge) o **Crea uno snapshot immediatamente e mantieni lo snapshot disponibile per l'inizializzazione delle sottoscrizioni** (replica transazionale)  
 Selezionare questa casella di controllo per creare uno snapshot non appena viene completata la Creazione guidata nuova pubblicazione. Deselezionarla invece se si prevede di modificare le proprietà dello snapshot nella finestra di dialogo **Proprietà pubblicazione** prima di generare uno snapshot oppure se il Sottoscrittore verrà inizializzato senza alcuno snapshot. Per altre informazioni, vedere [Inizializzazione di una sottoscrizione transazionale senza uno snapshot](../../relational-databases/replication/initialize-a-transactional-subscription-without-a-snapshot.md).  
  
> [!NOTE]  
>  Durante la procedura guidata è possibile che venga richiesto di selezionare la connessione al server di distribuzione per consentire l'avvio del processo appropriato per l'agente di distribuzione o l'agente di merge.  
  
 **Usa la pianificazione seguente per l'esecuzione dell'agente snapshot**  
 Accettare la pianificazione predefinita per l'esecuzione dell'agente snapshot oppure fare clic su **Cambia** per specificare una pianificazione diversa.  
  
## <a name="see-also"></a>Vedere anche  
 [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)   
 [Creare e applicare lo snapshot iniziale](../../relational-databases/replication/create-and-apply-the-initial-snapshot.md)   
 [Visualizzare e modificare le proprietà della pubblicazione](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)   
 [Inizializzare una sottoscrizione con uno snapshot](../../relational-databases/replication/initialize-a-subscription-with-a-snapshot.md)   
 [Pubblicare dati e oggetti di database](../../relational-databases/replication/publish/publish-data-and-database-objects.md)   
 [Panoramica degli agenti di replica](../../relational-databases/replication/agents/replication-agents-overview.md)  
  
  
