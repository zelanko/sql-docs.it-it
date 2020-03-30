---
title: Sottoscrivere le pubblicazioni | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.conc.subtopubs.f1
helpviewer_keywords:
- subscriptions [SQL Server replication], about subscriptions
- pull subscriptions [SQL Server replication]
- subscriptions [SQL Server replication]
- push subscriptions [SQL Server replication], about push subscriptions
- merge replication subscribing [SQL Server replication]
- merge replication subscribing [SQL Server replication], about subscribing
- publications [SQL Server replication], subscribing
- push subscriptions [SQL Server replication]
- pull subscriptions [SQL Server replication], about pull subscriptions
- snapshot replication [SQL Server], subscribing
- transactional replication, subscribing
ms.assetid: 088ee30a-05ab-47c4-92ed-316b93e12445
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-current||>=sql-server-2014||=sqlallproducts-allversions
ms.openlocfilehash: e08891eb7cb9fb897b48e37d6d8caa0e12620d06
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/30/2020
ms.locfileid: "68768364"
---
# <a name="subscribe-to-publications"></a>Subscribe to Publications
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md.md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Una sottoscrizione è la richiesta di una copia di dati o di oggetti di database in una pubblicazione. Una sottoscrizione definisce quale pubblicazione verrà ricevuta, insieme alla posizione e al momento in cui verrà ricevuta. Quando si pianificano le sottoscrizioni, è necessario decidere dove si desidera eseguire l'elaborazione dell'agente. La posizione di esecuzione dell'agente varia in base al tipo di sottoscrizione selezionato. In una sottoscrizione push, l'agente di merge o l'agente di distribuzione viene eseguito nel server di distribuzione, mentre in una sottoscrizione pull gli agenti vengono eseguiti nei Sottoscrittori. Dopo la creazione di una sottoscrizione non è più possibile modificarne il tipo.  

[!INCLUDE[azure-sql-db-replication-supportability-note](../../includes/azure-sql-db-replication-supportability-note.md)]
  
|Subscription|Caratteristiche|Situazioni in cui utilizzarla|  
|------------------|---------------------|--------------|  
|Sottoscrizione push|Nelle sottoscrizioni push il server di pubblicazione propaga le modifiche a un Sottoscrittore senza che il Sottoscrittore ne faccia richiesta. È possibile inviare le modifiche ai Sottoscrittori su richiesta, in modo continuato o in base a una pianificazione definita. L'agente di distribuzione o l'agente di merge viene eseguito nel server di distribuzione.|I dati vengono sincronizzati in modo continuato o in modo ricorrente in base a una pianificazione specifica.<br /><br /> Le pubblicazioni richiedono lo spostamento dei dati quasi in tempo reale.<br /><br /> In un server di distribuzione l'aumento dell'overhead del processore non compromette le prestazioni.<br /><br /> Generalmente utilizzato con la replica snapshot e transazionale.|  
|Sottoscrizione pull|Tramite le sottoscrizioni pull il Sottoscrittore richiede le modifiche eseguite nel server di pubblicazione. Le sottoscrizioni pull consentono al Sottoscrittore di stabilire quando sincronizzare le modifiche apportate ai dati. L'agente di distribuzione o l'agente di merge viene eseguito nel Sottoscrittore.|I dati vengono sincronizzati su richiesta o in base a una pianificazione anziché in modo continuo.<br /><br /> Alla pubblicazione è associato un numero elevato di Sottoscrittori e/o l'esecuzione di tutti gli agenti nel server di distribuzione richiederebbe un numero di risorse eccessivo.<br /><br /> I Sottoscrittori sono autonomi, scollegati e/o mobili. I Sottoscrittori determinano quando eseguire la connessione e quando sincronizzare le modifiche.<br /><br /> Generalmente utilizzato con la replica di tipo merge.|  
  
## <a name="merge-replication-subscription-types"></a>Tipi di sottoscrizione della replica di tipo merge  
 Tutti i tipi di replica consentono le sottoscrizioni push e pull. Per la replica di tipo merge vengono usati due termini aggiuntivi per distinguere le sottoscrizioni: sottoscrizioni client e sottoscrizioni server. Le sottoscrizioni client e server possono essere entrambe utilizzate con le sottoscrizioni push e pull. Le sottoscrizioni client sono appropriate per la maggior parte dei Sottoscrittori, mentre le sottoscrizioni server sono generalmente utilizzate per i Sottoscrittori che ripubblicano i dati in altri Sottoscrittori. La scelta del tipo di sottoscrizione influisce anche sulla risoluzione dei conflitti.  
  
## <a name="non-sql-server-subscribers"></a>Sottoscrittori non SQL Server  
 Nei sistemi Oracle e IBM DB2 è possibile sottoscrivere pubblicazioni snapshot e transazionali mediante le sottoscrizioni push. Per altre informazioni, vedere [Non-SQL Server Subscribers](../../relational-databases/replication/non-sql/non-sql-server-subscribers.md).  
  
## <a name="creating-subscriptions"></a>Creazione di sottoscrizioni  
 Per creare una sottoscrizione, è necessario specificare le seguenti informazioni:  
  
-   Nome della pubblicazione.  
  
-   Nome del Sottoscrittore e database di sottoscrizione.  
  
-   Se l'agente di distribuzione o l'agente di merge viene eseguito nel server di distribuzione o nel Sottoscrittore.  
  
-   Se l'agente di distribuzione o di merge viene eseguito in modo continuato, in base a una pianificazione specifica oppure solo su richiesta.  
  
-   Se l'agente di snapshot deve creare uno snapshot iniziale per la sottoscrizione e l'agente di distribuzione o di merge deve applicare lo snapshot al Sottoscrittore.  
  
-   Account utilizzati per eseguire l'agente di distribuzione o di merge.  
  
-   Per la replica di tipo merge, il tipo di sottoscrizione: server o client.  
  
 **Per creare una sottoscrizione push**  
  
 [Creare una sottoscrizione push](../../relational-databases/replication/create-a-push-subscription.md)  
  
 **Per visualizzare o modificare le proprietà di sottoscrizione push**  
  
 [Visualizzare e modificare le proprietà delle sottoscrizioni push](../../relational-databases/replication/view-and-modify-push-subscription-properties.md)  
  
 **Per eliminare una sottoscrizione push**  
  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]: [Eliminare una sottoscrizione push](../../relational-databases/replication/delete-a-push-subscription.md)  
  
> [!NOTE]  
>  Se si elimina una sottoscrizione non si rimuovono gli oggetti pubblicati dal Sottoscrittore.  
  
 **Per creare una sottoscrizione pull**  
  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]: [Creare una sottoscrizione pull](../../relational-databases/replication/create-a-pull-subscription.md)  
  
 **Per visualizzare o modificare le proprietà di sottoscrizione pull**  
  
 [Visualizzare e modificare le proprietà delle sottoscrizioni pull](../../relational-databases/replication/view-and-modify-pull-subscription-properties.md)  
  
 **Per eliminare una sottoscrizione pull**  
  
 [Eliminare una sottoscrizione pull](../../relational-databases/replication/delete-a-pull-subscription.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Proteggere il Sottoscrittore](../../relational-databases/replication/security/secure-the-subscriber.md)   
 [Scadenza e disattivazione delle sottoscrizioni](../../relational-databases/replication/subscription-expiration-and-deactivation.md)  
  
  
