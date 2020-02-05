---
title: Inizializzare una sottoscrizione senza uno snapshot (transazionale)
description: Informazioni su come inizializzare una replica transazionale senza usare uno snapshot per SQL Server.
ms.custom: seo-lt-2019
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- transactional replication, initializing
- replication [SQL Server], initializing
- initializing subscriptions [SQL Server replication], without snapshots
ms.assetid: 75c8c1f8-60bc-44a8-944b-d18d1f6bda11
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: df4463bf1ebfcc981c2828966c58e7fd0193f19f
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/01/2020
ms.locfileid: "76287968"
---
# <a name="initialize-a-transactional-subscription-without-a-snapshot"></a>Inizializzazione di una sottoscrizione transazionale senza uno snapshot
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  Per impostazione predefinita, una sottoscrizione di una pubblicazione transazionale viene inizializzata con uno snapshot generato dall'agente snapshot e applicato dall'agente di distribuzione. In alcuni scenari, ad esempio quelli che comportano l'utilizzo di set di dati iniziali di grandi dimensioni, è preferibile inizializzare una sottoscrizione utilizzando un altro metodo. Altri metodi di inizializzazione di un Sottoscrittore includono:  
  
-   Specifica di un backup. Ripristinare il backup sul Sottoscrittore in modo che l'agente di distribuzione possa quindi copiare le procedure di sistema e i metadati di replica richiesti. L'inizializzazione con un backup rappresenta la procedura più rapida per il recapito dei dati al Sottoscrittore ed è conveniente in quanto è possibile utilizzare qualsiasi backup recente purché sia stato eseguito in seguito all'abilitazione della pubblicazione per l'inizializzazione con un backup.  
  
-   Copia di un set di dati iniziali nel Sottoscrittore mediante un altro meccanismo, quale l'associazione di un database. È necessario accertarsi che nel Sottoscrittore siano presenti lo schema e i dati corretti. Successivamente, l'agente di distribuzione copierà le procedure di sistema e i metadati richiesti.  
  
## <a name="initializing-a-subscription-with-a-backup"></a>Inizializzazione di una sottoscrizione con un backup  
 Un backup contiene un intero database. Ogni database di sottoscrizione conterrà pertanto una copia completa del database di pubblicazione dopo l'inizializzazione:  
  
-   Il backup include tabelle non specificate come articoli per la pubblicazione.  
  
-   Il backup include tutti i dati, anche se in una tabella sono specificati filtri di riga o di colonna.  
  
 L'operazione di rimozione degli oggetti o dei dati non desiderati in seguito al ripristino del backup è a carico dell'amministratore o dell'applicazione. Nelle sincronizzazioni successive le modifiche ai dati vengono replicate solo se si riferiscono a tabelle specificate come articoli e se le modifiche soddisfano i criteri di filtro specificati.  
  
> [!NOTE]  
>  Durante il ripristino di un backup, è necessario accertarsi che il backup provenga dal server di pubblicazione se si desidera sincronizzare automaticamente il Sottoscrittore. Nel backup i valori dei numeri di sequenza del file di log (LSN), utilizzati per impostare il punto in cui avviare la sincronizzazione, sono specifici del server di pubblicazione.  
  
 **Per inizializzare una sottoscrizione con un backup**  
  
 Per inizializzare una sottoscrizione con un backup, è innanzitutto necessario abilitare l'opzione al momento della creazione di una pubblicazione, quindi specificare i valori per diverse opzioni al momento della creazione di una sottoscrizione. Le pubblicazioni possono essere abilitate mediante la Creazione guidata nuova pubblicazione o a livello di programmazione. I valori richiesti per le opzioni di sottoscrizione, tuttavia, possono essere specificati solo a livello di programmazione.  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]: [Abilitare l'inizializzazione con un backup per le pubblicazioni transazionali &#40;SQL Server Management Studio&#41;](../../relational-databases/replication/enable-initialization-with-backup-for-transactional-publications.md)  
  
-   Programmazione Transact-SQL della replica: [Inizializzare una sottoscrizione transazionale da un backup &#40;programmazione Transact-SQL della replica&#41;](../../relational-databases/replication/initialize-a-transactional-subscription-from-a-backup.md)  
  
> [!NOTE]  
>  Se una sottoscrizione viene inizializzata senza utilizzare uno snapshot, l'account con il quale viene eseguito il servizio SQL Server nel server di pubblicazione dovrà disporre delle autorizzazioni di scrittura sulla cartella snapshot del server di distribuzione. Per ulteriori informazioni sulle autorizzazioni, vedere [Replication Agent Security Model](../../relational-databases/replication/security/replication-agent-security-model.md).  
  
### <a name="ensuring-the-suitability-of-a-backup"></a>Verifica dell'idoneità di un backup  
 Un backup è idoneo per l'inizializzazione di un Sottoscrittore se tutte le transazioni che hanno luogo dopo la relativa esecuzione vengono archiviate nel server di distribuzione. Se il backup non è idoneo, durante la replica verrà visualizzato un messaggio di errore.  
  
 Per accertarsi che un backup sia idoneo per l'utilizzo, attenersi alle seguenti indicazioni:  
  
-   Utilizzare l'ultimo backup disponibile e, se è precedente al periodo massimo di memorizzazione della distribuzione, creare un nuovo backup prima di tentare di inizializzare una sottoscrizione con un backup. Per ulteriori informazioni sul periodo di memorizzazione, vedere [Subscription Expiration and Deactivation](../../relational-databases/replication/subscription-expiration-and-deactivation.md).  
  
-   Per impostazione predefinita, il processo di pulizia della distribuzione cancella dal database di distribuzione le transazioni che risalgono a più di 72 ore. La pulizia si basa sul periodo di memorizzazione impostato per la pubblicazione. Durante la sincronizzazione con backup precedenti, provare a disabilitare temporaneamente il processo prima del backup che si desidera ripristinare e a riabilitarlo in seguito alla creazione della sottoscrizione. In questo modo si impedisce la rimozione dal database di distribuzione delle transazioni che potrebbero essere necessarie per la corretta sincronizzazione dal backup. Per informazioni sull'esecuzione di processi di pulizia, vedere [Eseguire processi di manutenzione della replica &#40;SQL Server Management Studio&#41;](../../relational-databases/replication/administration/run-replication-maintenance-jobs-sql-server-management-studio.md).  
  
 In alcuni casi è necessario eseguire manualmente le personalizzazioni nel database del Sottoscrittore ripristinato dopo aver impostato le sottoscrizioni inizializzate con un backup. In genere, le modifiche manuali nel database del Sottoscrittore ripristinato sono necessarie se il server di pubblicazione è definito in modo che il contenuto del database del Sottoscrittore sia diverso da quello del database del server di pubblicazione, in base alle previsioni.  
  
-   Le viste indicizzate nel database ripristinato devono essere convertite in tabelle se vengono pubblicate come articoli di viste indicizzate di tabelle basati su log  
  
-   Le colonne di tipo timestamp sottoscritte nel database ripristinato devono essere convertite in colonne **binary(8)** . A tale scopo, copiare il contenuto delle tabelle contenenti colonne di tipo timestamp nelle nuove tabelle con schemi corrispondenti, ad eccezione delle colonne **binary(8)** che sostituiscono le colonne di tipo timestamp, eliminare le tabelle originali e rinominare le nuove tabelle con gli stessi nomi delle tabelle originali.  
  
## <a name="initializing-a-subscription-with-an-alternative-method"></a>Inizializzazione di una sottoscrizione con un metodo alternativo  
 È possibile inizializzare una sottoscrizione utilizzando qualsiasi metodo che consenta di copiare nel Sottoscrittore i dati e lo schema del database di pubblicazione, come [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. Quando si utilizza un metodo alternativo per inizializzare il Sottoscrittore, gli oggetti di supporto della replica vengono copiati nel Sottoscrittore.  
  
 Diversamente dall'inizializzazione con un backup, è necessario assicurarsi personalmente o mediante l'applicazione che i dati e lo schema vengano sincronizzati correttamente al momento dell'aggiunta della sottoscrizione. Ad esempio, in presenza di attività nel server di pubblicazione tra il momento in cui i dati e lo schema vengono copiati nel Sottoscrittore e il momento in cui viene aggiunta la sottoscrizione, le modifiche risultanti da questa attività potrebbero non essere replicate nel Sottoscrittore.  
  
 Per inizializzare una sottoscrizione con un metodo alternativo, vedere [Initialize a Subscription Manually](../../relational-databases/replication/initialize-a-subscription-manually.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Inizializzare una sottoscrizione](../../relational-databases/replication/initialize-a-subscription.md)  
  
  
