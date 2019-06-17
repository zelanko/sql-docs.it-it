---
title: Sottoscrizioni aggiornabili per la replica transazionale | Microsoft Docs
ms.custom: ''
ms.date: 03/31/2016
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- transactional replication, updatable subscriptions
- updatable subscriptions, about updatable subscriptions
- queued updating subscriptions [SQL Server replication]
- immediate updating subscriptions
- subscriptions [SQL Server replication], updatable
- updatable subscriptions
ms.assetid: 8eec95cb-3a11-436e-bcee-bdcd05aa5c5a
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 81235bf4bf4f1234be3d1ffdc341d3239b8d2b35
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62655493"
---
# <a name="updatable-subscriptions-for-transactional-replication"></a>Updatable Subscriptions for Transactional Replication
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

    
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../../includes/ssnotedepfutureavoid-md.md)]  
  
 La replica transazionale supporta gli aggiornamenti dei Sottoscrittori attraverso le sottoscrizioni aggiornabili e la replica peer-to-peer. Di seguito sono indicati i due tipi di sottoscrizioni aggiornabili:  
  
-   Aggiornamento immediato. Per l'aggiornamento dei dati nel Sottoscrittore è necessario che il server di pubblicazione e il Sottoscrittore siano connessi.  
  
-   Aggiornamento in coda. Per l'aggiornamento dei dati nel Sottoscrittore non è necessario che il server di pubblicazione e il Sottoscrittore siano connessi. È possibile eseguire gli aggiornamenti mentre il Sottoscrittore o il server di pubblicazione è offline.  
  
 Quando si aggiornano i dati in un Sottoscrittore, questi vengono innanzitutto propagati al server di pubblicazione e quindi agli altri Sottoscrittori. Se si utilizza l'aggiornamento immediato, le modifiche vengono propagate immediatamente tramite il protocollo di commit in due fasi. Se si utilizza l'aggiornamento in coda, le modifiche vengono archiviate in una coda. Le transazioni in coda vengono quindi applicate in modo asincrono nel server di pubblicazione ogni volta che è disponibile la connettività di rete. Poiché gli aggiornamenti vengono propagati in modo asincrono al server di pubblicazione, gli stessi dati potrebbero essere stati aggiornati dal server di pubblicazione o da un altro Sottoscrittore e potrebbero verificarsi conflitti in fase di applicazione degli aggiornamenti. I conflitti vengono rilevati e risolti in base a criteri di risoluzione dei conflitti impostati durante la creazione della pubblicazione.  
  
 Se si crea una pubblicazione transazionale con sottoscrizioni aggiornabili tramite la Creazione guidata nuova pubblicazione, verranno abilitati sia l'aggiornamento immediato che l'aggiornamento in coda. Se si crea una pubblicazione con stored procedure, è possibile abilitare una o entrambe le opzioni. Quando si crea una sottoscrizione della pubblicazione, è necessario specificare la modalità di aggiornamento da utilizzare. Se necessario, sarà quindi possibile passare da una modalità di aggiornamento all'altra. Per ulteriori informazioni, vedere la sezione seguente "Passaggio da una modalità di aggiornamento all'altra".  
  
 Per abilitare le sottoscrizioni aggiornabili per le pubblicazioni transazionali, [Enable Updating Subscriptions for Transactional Publications](../publish/enable-updating-subscriptions-for-transactional-publications.md)  
  
 Per creare sottoscrizioni aggiornabili per le pubblicazioni transazionali, vedere [Create an Updatable Subscription to a Transactional Publication](../publish/create-an-updatable-subscription-to-a-transactional-publication.md)  
  
## <a name="switching-between-update-modes"></a>Passaggio da una modalità di aggiornamento all'altra  
 Quando si utilizzano le sottoscrizioni aggiornabili, è possibile specificare che per una sottoscrizione venga utilizzata una modalità di aggiornamento e quindi si passi all'altra se l'applicazione lo richiede. È possibile, ad esempio, specificare che per una sottoscrizione venga utilizzato l'aggiornamento immediato, ma si passi all'aggiornamento in coda se un errore di sistema provoca la perdita della connettività di rete.  
  
> [!NOTE]  
>  La replica non passa automaticamente da una modalità di aggiornamento all'altra. Per passare da una modalità all'altra, è necessario impostare la modalità di aggiornamento tramite SQL Server Management Studio oppure l'applicazione deve chiamare [sp_setreplfailovermode &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-setreplfailovermode-transact-sql).  
  
 Se si passa dall'aggiornamento immediato all'aggiornamento in coda, non sarà possibile tornare all'aggiornamento immediato fino a quando il Sottoscrittore e il server di pubblicazione non sono connessi e tramite l'agente di lettura coda non sono stati applicati al server di pubblicazione tutti i messaggi in sospeso nella coda.  
  
 **Per passare da una modalità di aggiornamento all'altra**  
  
 Per passare da una modalità di aggiornamento all'altra, è necessario abilitare la pubblicazione e la sottoscrizione per entrambe le modalità e quindi passare da una all'altra, se necessario. Per ulteriori informazioni, vedere  
[Passare da una modalità di aggiornamento all'altra per una sottoscrizione transazionale aggiornabile](../administration/switch-between-update-modes-for-an-updatable-transactional-subscription.md)  
  
### <a name="considerations-for-using-updatable-subscriptions"></a>Considerazioni per l'utilizzo di sottoscrizioni aggiornabili  
  
-   Dopo avere abilitato una pubblicazione per le sottoscrizioni aggiornabili o per le sottoscrizioni ad aggiornamento in coda, non sarà possibile disabilitare l'opzione per la pubblicazione, anche nel caso in cui non sia necessaria per le sottoscrizioni. Per disabilitare l'opzione, è necessario eliminare la pubblicazione e crearne una nuova.  
  
-   La ripubblicazione dei dati non è supportata.  
  
-   La replica aggiunge la colonna **msrepl_tran_version** alle tabelle pubblicate per consentire il rilevamento. A causa di questa colonna aggiuntiva, tutte le istruzioni `INSERT` devono includere un elenco di colonne.  
  
-   Per apportare modifiche allo schema in una tabella di una pubblicazione che supporta le sottoscrizioni aggiornabili, è necessario arrestare tutte le attività nella tabella nel server di pubblicazione e nei Sottoscrittori e propagare a tutti i nodi le modifiche ai dati in sospeso prima di apportare modifiche allo schema. In questo modo le transazioni in sospeso non entrano in conflitto con le modifiche allo schema in sospeso. Dopo avere propagato a tutti i nodi le modifiche dello schema, è possibile riprendere le attività nelle tabelle pubblicate. Per altre informazioni, vedere [Come mettere una topologia di replica in stato di inattività &#40;programmazione Transact-SQL della replica&#41;](../administration/quiesce-a-replication-topology-replication-transact-sql-programming.md).  
  
-   Se si prevede di passare da una modalità di aggiornamento all'altra, è necessario eseguire l'agente di lettura coda almeno una volta dopo l'inizializzazione della sottoscrizione. Per impostazione predefinita, l'agente di lettura coda viene eseguito continuamente.  
  
-   Se il database del Sottoscrittore è partizionato orizzontalmente e nella partizione vi sono righe presenti nel Sottoscrittore ma non nel server di pubblicazione, il Sottoscrittore non potrà aggiornare tali righe. I tentativi di aggiornamento di queste righe generano un errore. In questi casi è necessario eliminare le righe dalla tabella e quindi aggiungerle nel server di pubblicazione.  
  
### <a name="updates-at-the-subscriber"></a>Aggiornamenti nel Sottoscrittore  
  
-   Gli aggiornamenti nel Sottoscrittore vengono propagati al server di pubblicazione, anche se una sottoscrizione è scaduta o inattiva. Verificare che tali sottoscrizioni vengano eliminate o reinizializzate.  
  
-   Se le colonne `TIMESTAMP` o `IDENTITY` vengono usate e replicate come tipi di dati di base, i valori contenuti non devono essere aggiornati nel sottoscrittore.  
  
-   I sottoscrittori non possono aggiornare o inserire valori `text`, `ntext` o `image` perché non è possibile leggere dalle tabelle inserite o eliminate all'interno dei trigger di rilevamento modifiche della replica. In modo analogo, i sottoscrittori non possono aggiornare o inserire valori `text` o `image` tramite `WRITETEXT` o `UPDATETEXT` perché i dati vengono sovrascritti dal server di pubblicazione. È invece possibile partizionare le colonne `text` e `image` in una tabella distinta e modificare le due tabelle all'interno di una transazione.  
  
     Per aggiornare gli oggetti di grandi dimensioni in un sottoscrittore, usare i tipi di dati `varchar(max)`, `nvarchar(max)`, `varbinary(max)` anziché, rispettivamente, `text`, `ntext`, e `image`.  
  
-   Gli aggiornamenti delle chiavi univoche, incluse le chiavi primarie, che generano duplicati, ad esempio, un aggiornamento del form `UPDATE <column> SET <column> =<column>+1` , non sono consentiti e vengono rifiutati in quanto violazioni dell'univocità. Questo avviene perché gli aggiornamenti dei set eseguiti nel sottoscrittore vengono propagati tramite replica come singole istruzioni `UPDATE` per tutte le righe interessate.  
  
-   Se il database del Sottoscrittore è partizionato orizzontalmente e nella partizione vi sono righe presenti nel Sottoscrittore ma non nel server di pubblicazione, il Sottoscrittore non potrà aggiornare tali righe. I tentativi di aggiornamento di queste righe generano un errore. In questi casi è necessario eliminare le righe dalla tabella e inserirle di nuovo.  
  
### <a name="user-defined-triggers"></a>Trigger definiti dall'utente  
  
-   Se per l'applicazione sono necessari trigger nel sottoscrittore, i trigger devono essere definiti con l'opzione `NOT FOR REPLICATION` nel server di pubblicazione e nel sottoscrittore. In questo modo, i trigger vengono attivati solo per modifiche ai dati originali, ma non quando le modifiche vengono replicate.  
  
     Verificare che il trigger definito dall'utente non venga attivato quando il trigger di replica aggiorna la tabella. A tale scopo, chiamare la procedura `sp_check_for_sync_trigger` nel corpo del trigger definito dall'utente. Per altre informazioni, vedere [sp_addlinkedserver &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-check-for-sync-trigger-transact-sql).  
  
### <a name="immediate-updating"></a>Aggiornamento immediato  
  
-   Per le sottoscrizioni ad aggiornamento immediato, le modifiche nel Sottoscrittore vengono propagate al server di pubblicazione e applicate tramite Microsoft Distributed Transaction Coordinator (MS DTC). Verificare che MS DTC sia installato e configurato nel server di pubblicazione e nel Sottoscrittore. Per ulteriori informazioni, vedere la documentazione di Windows.  
  
-   Per i trigger utilizzati dalle sottoscrizioni ad aggiornamento immediato, per replicare le modifiche è necessaria una connessione al server di pubblicazione.  
  
-   Se la pubblicazione consente le sottoscrizioni ad aggiornamento immediato e un articolo nella pubblicazione contiene un filtro colonne, non è possibile escludere tramite il filtro le colonne che non ammettono valori Null senza valori predefiniti.  
  
### <a name="queued-updating"></a>Aggiornamento in coda  
  
-   Le tabelle incluse in una pubblicazione di tipo merge non possono essere pubblicate anche come parte di una pubblicazione transazionale che consente le sottoscrizioni ad aggiornamento in coda.  
  
-   La chiave primaria viene utilizzata come indicatore di posizione dei record per tutte le query, pertanto non è consigliabile apportare aggiornamenti a colonne chiave primaria quando si utilizza l'aggiornamento in coda. Quando i criteri di risoluzione dei conflitti sono impostati su Prevale il Sottoscrittore, è necessario prestare attenzione durante l'aggiornamento delle chiavi primarie. Se gli aggiornamenti alla chiave primaria vengono eseguiti sia nel Sottoscrittore che nel server di pubblicazione, si ottengono due righe con chiavi primarie diverse.  
  
-   Per le colonne del tipo di dati `SQL_VARIANT`:, quando i dati vengono inseriti o aggiornati nel sottoscrittore, ne viene eseguito il mapping dall'agente di lettura coda quando vengono copiati dal sottoscrittore alla coda nel modo illustrato di seguito:  
  
    -   Viene eseguito il mapping di `BIGINT`, `DECIMAL`, `NUMERIC`, `MONEY` e `SMALLMONEY` a `NUMERIC`.  
  
    -   Viene eseguito il mapping di `BINARY` e `VARBINARY` ai dati `VARBINARY`.  
  
### <a name="conflict-detection-and-resolution"></a>Rilevamento e risoluzione di conflitti  
  
-   Per i criteri di risoluzione dei conflitti Prevale il Sottoscrittore: la risoluzione dei conflitti non è supportata per gli aggiornamenti alle colonne chiave primaria.  
  
-   I conflitti provocati dagli errori relativi ai vincoli di chiave esterna non vengono risolti dalla replica:  
  
    -   Se non si prevedono conflitti e i dati sono partizionati correttamente, ovvero se i Sottoscrittori non aggiornano le stesse righe, è possibile utilizzare vincoli di chiave esterna nel server di pubblicazione e nel Sottoscrittore.  
  
    -   Se si prevedono conflitti, quando si utilizza l'opzione di risoluzione dei conflitti "Prevale il Sottoscrittore", è consigliabile non utilizzare vincoli di chiave esterna nel server di pubblicazione e nel Sottoscrittore, mentre, quando si utilizza l'opzione di risoluzione dei conflitti "Prevale il server di pubblicazione", è consigliabile non utilizzare vincoli di chiave esterna nel Sottoscrittore.  
  
## <a name="see-also"></a>Vedere anche  
 [Peer-to-Peer Transactional Replication](peer-to-peer-transactional-replication.md)   
 [Replica transazionale](transactional-replication.md)   
 [Pubblicare dati e oggetti di database](../publish/publish-data-and-database-objects.md)   
 [Sottoscrizione delle pubblicazioni](../subscribe-to-publications.md)  
  
  
