---
description: Proprietà pubblicazione, Opzioni sottoscrizione
title: Proprietà pubblicazione, Opzioni sottoscrizione | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.newpubwizard.pubproperties.subscriptionoptions.f1
ms.assetid: 31abd605-b273-419d-86df-d0ecf539a507
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016
ms.openlocfilehash: b30077fae17f88495c660cf5c7881270342b01cd
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2020
ms.locfileid: "97483042"
---
# <a name="publication-properties-subscription-options"></a>Proprietà pubblicazione, Opzioni sottoscrizione
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]
  La pagina **Opzioni sottoscrizione** della finestra di dialogo **Proprietà pubblicazione** consente di visualizzare e impostare le proprietà a livello di pubblicazione associate alle sottoscrizioni. Le proprietà sono raggruppate nelle categorie seguenti:  
  
-   Proprietà che si applicano a tutte le pubblicazioni.  
  
-   Proprietà che si applicano alle pubblicazioni snapshot e transazionali, incluse le pubblicazioni che consentono le sottoscrizioni aggiornabili.  
  
-   Proprietà che si applicano alle pubblicazioni di tipo merge.  
  
> [!NOTE]  
>  Alcune proprietà sono di sola lettura, per i motivi spiegati nelle descrizioni delle proprietà all'interno di questo argomento. Per alcune modifiche alle proprietà è necessario un nuovo snapshot per la pubblicazione, mentre per altre è necessaria inoltre la reinizializzazione di tutte le sottoscrizioni. Per altre informazioni, vedere [Modificare le proprietà di pubblicazioni e articoli](../../relational-databases/replication/publish/change-publication-and-article-properties.md).  
  
## <a name="options-for-all-publications"></a>Opzioni per tutte le pubblicazioni  
  
### <a name="creation-and-synchronization"></a>Creazione e sincronizzazione  
 **Consenti sottoscrizioni anonime**  
 Determina se consentire le sottoscrizioni pull anonime. Le sottoscrizioni anonime sono supportate per [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssEWEd2005](../../includes/ssewed2005-md.md)], [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssMobileEd2005](../../includes/ssmobileed2005-md.md)] e [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per Windows CE. Per utilizzare questa opzione per le pubblicazioni snapshot e transazionali, l'opzione **Snapshot sempre disponibile** deve essere impostata su **True**.  
  
 **Database di sottoscrizione collegabile**  
 Determina se è possibile creare le sottoscrizioni collegando una copia del database di sottoscrizione. Per le pubblicazioni snapshot e transazionali, è necessario che l'opzione **Snapshot sempre disponibile** sia impostata su **True** .  
  
> [!IMPORTANT]  
>  Le sottoscrizioni collegabili non saranno disponibili nelle versioni future. Questa funzionalità è deprecata.  
  
 **Consenti sottoscrizioni pull**  
 Determina se consentire ai Sottoscrittori di creare sottoscrizioni pull sulla pubblicazione corrente. Per altre informazioni, vedere [Sottoscrivere le pubblicazioni](../../relational-databases/replication/subscribe-to-publications.md).  
  
### <a name="schema-replication"></a>Replica dello schema  
 **Replicare le modifiche dello schema**  
 Solo [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e versioni successive. Determina se replicare le modifiche dello schema, ad esempio l'aggiunta di una colonna a una tabella o la modifica del tipo di dati di una colonna, agli oggetti pubblicati. Per altre informazioni, vedere [Apportare modifiche allo schema nei database di pubblicazione](../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md).  
  
## <a name="options-for-snapshot-and-transactional-publications"></a>Opzioni per le pubblicazioni snapshot e transazionali  
  
### <a name="creation-and-synchronization"></a>Creazione e sincronizzazione  
 **Agente di distribuzione indipendente**  
 Determina se utilizzare un agente che sia indipendente da altre pubblicazioni del database. Questa opzione è di sola lettura, è impostata su **True** per impostazione predefinita per le pubblicazioni create con la Creazione guidata nuova pubblicazione e non può essere modificata dopo la creazione della pubblicazione. Per altre informazioni, vedere [Amministrazione dell'agente di replica](../../relational-databases/replication/agents/replication-agent-administration.md).  
  
 **Snapshot sempre disponibile**  
 Determina se vengono creati file di snapshot a ogni esecuzione dell'agente snapshot. È necessaria l'opzione **Agente di distribuzione indipendente**. Questa opzione è di sola lettura ed è impostata su **True** se è stata selezionata l'opzione **Crea uno snapshot immediatamente e mantieni lo snapshot disponibile per l'inizializzazione delle sottoscrizioni** nella pagina **Agente snapshot** della Creazione guidata nuova pubblicazione (opzione predefinita). Per altre informazioni, vedere [Creare e applicare lo snapshot](../../relational-databases/replication/create-and-apply-the-initial-snapshot.md).  
  
 **Consenti inizializzazione dai file di backup**  
 Solo[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e versioni successive. Determina se consentire l'utilizzo dei file di backup per inizializzare le sottoscrizioni. Per altre informazioni, vedere [Inizializzazione di una sottoscrizione transazionale senza uno snapshot](../../relational-databases/replication/initialize-a-transactional-subscription-without-a-snapshot.md).  
  
 **Consenti Sottoscrittori non SQL Server**  
 Solo[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e versioni successive. Determina se la pubblicazione supporta Sottoscrittori non [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se si imposta questa opzione su **True** alcune proprietà della pubblicazione vengono modificate per supportare i sottoscrittori non [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se esistono sottoscrizioni questa opzione è di sola lettura. L'opzione non può essere impostata su **True** se **Consenti sottoscrizioni ad aggiornamento immediato**, **Consenti sottoscrizioni ad aggiornamento in coda** o **Consenti sottoscrizioni peer-to-peer** è impostata su **True**. Per altre informazioni, vedere [Non-SQL Server Subscribers](../../relational-databases/replication/non-sql/non-sql-server-subscribers.md).  
  
### <a name="data-transformation"></a>Trasformazioni dei dati  
 **Consenti trasformazioni dei dati**  
 Determina se utilizzare Data Transformation Services (DTS) per trasformare i dati prima di distribuirli a un Sottoscrittore. Questa opzione è di sola lettura. Le trasformazioni dei dati possono essere abilitate solo se una pubblicazione viene creata utilizzando le stored procedure.  
  
> [!IMPORTANT]  
>  Le sottoscrizioni trasformabili non saranno disponibili nelle versioni future. Questa funzionalità è deprecata.  
  
### <a name="peer-to-peer-replication"></a>Replica peer-to-peer  
 **Consenti sottoscrizioni peer-to-peer**  
 Si applica solo a [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e versioni successive. Determina se la pubblicazione supporta la replica peer-to-peer. Se si imposta questa opzione su **True** , alcune proprietà della pubblicazione verranno modificate per supportare la replica peer-to-peer. Se esistono sottoscrizioni questa opzione è di sola lettura. Questa opzione non può essere impostata su **True** se l'opzione **Consenti sottoscrizioni ad aggiornamento immediato** , **Consenti sottoscrizioni ad aggiornamento in coda** o **Consenti Sottoscrittori non SQL Server** è impostata su **True**. Per altre informazioni, vedere [Peer-to-Peer Transactional Replication](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md).  
  
 **Consenti rilevamento conflitti peer-to-peer**  
 Si applica solo a [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e versioni successive. Specifica se il rilevamento dei conflitti è abilitato per la pubblicazione. Per usare il rilevamento dei conflitti, tutti i nodi devono eseguire [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] o versioni successive e il rilevamento deve essere abilitato per tutti i nodi. Per utilizzare rilevamento dei conflitti, è inoltre necessario specificare un valore per **ID origine peer**. Per altre informazioni, vedere [Conflict Detection in Peer-to-Peer Replication](../../relational-databases/replication/transactional/peer-to-peer-conflict-detection-in-peer-to-peer-replication.md).  
  
 **ID origine peer**  
 Si applica solo a [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e versioni successive. Specifica un ID per un nodo in una topologia peer-to-peer. Questo ID viene utilizzato per il rilevamento dei conflitti se l'opzione **Consenti rilevamento dei conflitti peer-to-peer** è impostata su **True**. Specificare un ID positivo diverso da zero che non sia mai stato utilizzato nella topologia. Per un elenco degli ID che sono già stati utilizzati, eseguire una query sulla tabella di sistema [Mspeer_originatorid_history](../../relational-databases/system-tables/mspeer-originatorid-history-transact-sql.md) .  
  
### <a name="updatable-subscriptions"></a>Sottoscrizioni aggiornabili  
 **Consenti sottoscrizioni ad aggiornamento immediato**  
 Determina se le modifiche apportate ai dati del Sottoscrittore possono essere replicate immediatamente nel server di pubblicazione. Questa opzione è di sola lettura. Le sottoscrizioni aggiornabili possono essere abilitate solo al momento della creazione di una pubblicazione. Per altre informazioni, vedere [Updatable Subscriptions for Transactional Replication](../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md).  
  
 **Consenti sottoscrizioni ad aggiornamento in coda**  
 Determina se le modifiche apportate ai dati del Sottoscrittore possono essere inserite in coda e replicate successivamente nel server di pubblicazione. Questa opzione è di sola lettura. Le sottoscrizioni aggiornabili possono essere abilitate solo al momento della creazione di una pubblicazione. Per altre informazioni, vedere [Updatable Subscriptions for Transactional Replication](../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md).  
  
 **Segnala conflitti a livello centrale**  
 Determina se segnalare i conflitti generati dalle modifiche apportate ai dati solo nel server di pubblicazione oppure sia nel server di pubblicazione che nel Sottoscrittore. È necessaria l'opzione **Consenti sottoscrizioni ad aggiornamento in coda**. Questa opzione è di sola lettura, è impostata su **True** per impostazione predefinita per le pubblicazioni create con la Creazione guidata nuova pubblicazione e non può essere modificata dopo la creazione della pubblicazione. Il valore **True** indica che i conflitti vengono segnalati solo sul server di pubblicazione. I conflitti possono essere visualizzati solo sul server in cui vengono segnalati.  
  
 **Criteri di risoluzione dei conflitti**  
 Consente di specifica l'azione da intraprendere quando una modifica apportata nel Sottoscrittore è in conflitto con una modifica apportata nel server di pubblicazione. È necessaria l'opzione **Consenti sottoscrizioni ad aggiornamento in coda**. Per altre informazioni, vedere [Queued Updating Conflict Detection and Resolution](../../relational-databases/replication/transactional/updatable-subscriptions-queued-updating-conflict-resolution.md).  
  
 **Tipo di coda**  
 Determina se utilizzare una coda [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o [!INCLUDE[msCoName](../../includes/msconame-md.md)] Message Queuing (MSMQ) per accodare le modifiche nel Sottoscrittore finché non possono essere applicate al server di pubblicazione. È necessaria l'opzione **Consenti sottoscrizioni ad aggiornamento in coda**. Questa opzione riguarda solo [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)], poiché nelle versioni successive per l'accodamento vengono sempre utilizzate tabelle [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="options-for-merge-publications"></a>Opzioni per le pubblicazioni di tipo merge  
  
### <a name="conflict-reporting"></a>Report sui conflitti  
 **Segnala conflitti a livello centrale**  
 Determina se segnalare i conflitti generati dalle modifiche apportate ai dati solo nel server di pubblicazione o sia nel server di pubblicazione che nel Sottoscrittore. Questa opzione è di sola lettura, è impostata su **True** per impostazione predefinita per le pubblicazioni create con la Creazione guidata nuova pubblicazione e non può essere modificata dopo la creazione della pubblicazione. Il valore **True** indica che i conflitti vengono segnalati solo sul server di pubblicazione. I conflitti possono essere visualizzati solo sul server in cui vengono segnalati. Per ulteriori informazioni, vedere la sezione relativa alla visualizzazione dei conflitti in [Advanced Merge Replication Conflict Detection and Resolution](../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md).  
  
### <a name="filtering"></a>Filtro  
 **Consenti filtri con parametri**  
 Viene impostata in base al fatto che una pubblicazione utilizzi i filtri con parametri. Questa opzione è sempre di sola lettura. Per altre informazioni sui filtri di riga con parametri, vedere [Filtri di riga con parametri](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md).  
  
 **Convalida Sottoscrittori**  
 Determina le funzioni da utilizzare per convalidare che un Sottoscrittore disponga della partizione dati corretta. È possibile immettere più valori separandoli con una virgola. Per altre informazioni, vedere [Convalidare le informazioni sulle partizioni per un Sottoscrittore di tipo merge](../../relational-databases/replication/validate-partition-information-for-a-merge-subscriber.md).  
  
 **Pre-calcola partizioni**  
 Solo[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e versioni successive. Determina se ottimizzare la sincronizzazione calcolando in anticipo quali righe di dati appartengono alle varie partizioni. L'impostazione predefinita di questa opzione è **True** se la pubblicazione soddisfa i criteri per le partizioni pre-calcolate. Per altre informazioni, vedere [Ottimizzare le prestazioni dei filtri con parametri con le partizioni pre-calcolate](../../relational-databases/replication/merge/parameterized-filters-optimize-for-precomputed-partitions.md).  
  
 **Ottimizza sincronizzazione**  
 Determina se ottimizzare l'elaborazione di processi merge archiviando metadati aggiuntivi in ogni Sottoscrittore. Tale ottimizzazione è stata sostituita dalle partizioni pre-calcolate. L'opzione **Ottimizza sincronizzazione** è rilevante solo se l'opzione **Pre-calcola partizioni** è impostata su **False**. Per altre informazioni sui filtri di riga con parametri, vedere [Filtri di riga con parametri](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md).  
  
### <a name="merge-processes"></a>Processi di merge  
 **Limita processi simultanei**  
 Determina se limitare il numero di agenti di merge che possono essere eseguiti contemporaneamente. Questa opzione viene in genere utilizzata se una pubblicazione include un elevato numero di sottoscrizioni push che potrebbero sincronizzarsi contemporaneamente.  
  
 **Numero massimo processi simultanei**  
 Numero massimo di agenti di merge che possono essere eseguiti contemporaneamente. È necessaria l'opzione **Limita processi simultanei**. Se il numero di agenti in sincronizzazione supera il numero massimo, gli agenti vengono inseriti in una coda fino a quando il loro numero non scende al di sotto di tale soglia.  
  
## <a name="see-also"></a>Vedere anche  
 [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)   
 [Visualizzare e modificare le proprietà della pubblicazione](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)   
 [Pubblicare dati e oggetti di database](../../relational-databases/replication/publish/publish-data-and-database-objects.md)  
  
  
