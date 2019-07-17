---
title: Specificare le proprietà della replica di Merge | Microsoft Docs
ms.custom: ''
ms.date: 11/29/2018
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- merge replication [SQL Server replication], about merge replication
- merge replication [SQL Server replication]
ms.assetid: ff87c368-4c00-4e48-809d-ea752839551e
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 22460851ce3136301beaf5d94e7b0a3b39f8217c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "68199290"
---
# <a name="specify-merge-replication-properties"></a>Specificare le proprietà della replica di Merge
Questo argomento illustra come specificare varie proprietà per la replica di tipo merge. 


## <a name="download-only"></a>Solo download
  In questa sezione viene descritto come specificare che un articolo di tabella di merge è di solo download nella [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] usando [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../../includes/tsql-md.md)]. Gli articoli di solo download sono progettati per le applicazioni i cui dati non vengono aggiornati nei Sottoscrittori. Per altre informazioni, vedere [Ottimizzare le prestazioni della replica di tipo merge con gli articoli di solo download](../merge/optimize-merge-replication-performance-with-download-only-articles.md).  
 
  
###  <a name="limitations-and-restrictions"></a>Limitazioni e restrizioni  
  
-   Se si specifica che un articolo è di tipo solo download dopo l'inizializzazione delle sottoscrizioni, tutte le sottoscrizioni client a cui è stato inviato l'articolo devono essere reinizializzate. Non è necessario reinizializzare le sottoscrizioni server. Per altre informazioni sugli effetti delle modifiche delle proprietà, vedere [Modifica delle proprietà di pubblicazioni e articoli](change-publication-and-article-properties.md).  
  
### <a name="using-sql-server-management-studio"></a>Utilizzo di SQL Server Management Studio  
 Specificare che un articolo è di tipo solo download nella pagina **Articoli** della Creazione guidata nuova pubblicazione o nella scheda **Proprietà** della finestra di dialogo **Proprietà articolo - \<Articolo>** . Questa finestra di dialogo è disponibile nella Creazione guidata nuova pubblicazione e nella finestra di dialogo **Proprietà pubblicazione - \<Pubblicazione>** . Per altre informazioni sull'uso della creazione guidata e l'accesso alla finestra di dialogo, vedere [Creare una pubblicazione](../publish/create-a-publication.md) e [Visualizzare e modificare le proprietà della pubblicazione](../publish/view-and-modify-publication-properties.md).  
  
#### <a name="to-specify-that-an-article-is-download-only-on-the-articles-page"></a>Per specificare che un articolo è di tipo solo download nella pagina Articoli  
  
-   Selezionare una tabella nella pagina **Articoli** di Creazione guidata nuova pubblicazione e quindi selezionare la casella di controllo **La tabella evidenziata è di tipo solo download**. 
  
#### <a name="to-specify-that-an-article-is-download-only-on-the-properties-tab-of-the-article-properties---article-dialog-box"></a>Per specificare che un articolo è di tipo solo download nella scheda Proprietà della finestra di dialogo Proprietà articolo - \<Articolo>  
  
1.  Nella pagina **Articoli** della Creazione guidata nuova pubblicazione o nella finestra di dialogo **Proprietà pubblicazione - \<Pubblicazione>** selezionare una tabella e quindi fare clic su **Proprietà articolo**.    
2.  Fare clic su **Imposta proprietà dell'articolo di tabelle evidenziato** o su **Imposta proprietà di tutti gli articoli di tabelle**.    
3.  Nella sezione **Oggetto di destinazione** della scheda **Proprietà** della finestra di dialogo **Proprietà articolo - \<Articolo>** specificare uno dei valori seguenti in **Direzione sincronizzazione**:    
    -   **Solo download sul Sottoscrittore, non consentire modifiche del Sottoscrittore**    
    -   **Solo download sul Sottoscrittore, consenti modifiche del Sottoscrittore**  
  
4.  Se è visualizzata la finestra di dialogo **Proprietà pubblicazione - \<Pubblicazione>** fare clic su **OK** per salvare e chiudere la finestra di dialogo.    

###  <a name="using-transact-sql"></a>Utilizzo di Transact-SQL  
  
#### <a name="to-specify-that-a-new-merge-table-article-is-download-only"></a>Per specificare che un nuovo articolo di tabella di merge è di solo download    
1.  Eseguire [sp_addmergearticle](/sql/relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql), specificando il valore **1** o **2** per il parametro **@subscriber_upload_options** . I numeri corrispondono al comportamento seguente:  
  
    -   **0** : nessuna restrizione (valore predefinito). Le modifiche eseguite nel Sottoscrittore vengono caricate nel server di pubblicazione.    
    -   **1** : le modifiche sono consentite nel Sottoscrittore, ma non vengono caricate nel server di pubblicazione.    
    -   **2** : non è consentito apportare modifiche nel Sottoscrittore.  
  
        > [!NOTE]  
        >  Se la tabella di origine di un articolo è già inclusa in un'altra pubblicazione, il valore di **@subscriber_upload_options** deve coincidere per entrambi gli articoli.  
  
#### <a name="to-modify-an-existing-merge-table-article-to-be-download-only"></a>Per impostare il tipo di un articolo di tabella di merge esistente su solo download  
  
1.  Per determinare se un articolo è di tipo solo download, eseguire [sp_helpmergearticle](/sql/relational-databases/system-stored-procedures/sp-helpmergearticle-transact-sql). Si noti il valore di **upload_options** relativo all'articolo nel set di risultati.    
2.  Se il valore restituito al passaggio 1 è **0**, eseguire [sp_changemergearticle](/sql/relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql), specificando il valore **subscriber_upload_options** per **@property** , il valore **1** per **@force_invalidate_snapshot** e **@force_reinit_subscription** e il valore **1** o **2** per **@value** , che corrisponde al comportamento seguente:  
  
    -   **1** : le modifiche sono consentite nel Sottoscrittore, ma non vengono caricate nel server di pubblicazione.    
    -   **2** : non è consentito apportare modifiche nel Sottoscrittore.  
  
        > [!NOTE]  
        >  Se la tabella di origine di un articolo è già inclusa in un'altra pubblicazione, il comportamento del solo download deve coincidere per entrambi gli articoli.  
 
## <a name="interactive-conflict-resolution">Risoluzione interattiva dei conflitti</a>
La replica di[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] offre un sistema di risoluzione interattivo che consente di risolvere i conflitti in modo manuale durante la sincronizzazione su richiesta in Gestione sincronizzazione [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows. Dopo l'abilitazione della risoluzione interattiva, risolvere interattivamente i conflitti durante la sincronizzazione utilizzando il sistema di risoluzione interattivo. Il sistema di risoluzione interattivo è disponibile tramite Gestione sincronizzazione [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows. Per altre informazioni, vedere [Sincronizzare una sottoscrizione mediante Gestione sincronizzazione Microsoft Windows &#40;Gestione sincronizzazione Microsoft Windows&#41;](../synchronize-a-subscription-using-windows-synchronization-manager.md).  
  
    
###  <a name="Recommendations"></a> Indicazioni  
  
-   Se si esegue una sincronizzazione all'esterno di Gestione sincronizzazione Microsoft Windows, ad esempio una sincronizzazione pianificata o su richiesta in SQL Server Management Studio o Monitoraggio replica, i conflitti vengono risolti automaticamente senza l'intervento dell'utente, utilizzando la risoluzione dei conflitti predefinita specificata per l'articolo. Per altre informazioni, vedere [Interactive Conflict Resolution](../merge/advanced-merge-replication-conflict-interactive-resolution.md).  
  
###  <a name="using-sql-server-management-studio"></a>Utilizzo di SQL Server Management Studio  
  
#### <a name="enable-interactive-conflict-resolution-for-an-article"></a>Abilitare la risoluzione interattiva dei conflitti per un articolo  
  
1.  Selezionare una tabella nella pagina **Articoli** della Creazione guidata nuova pubblicazione o nella finestra di dialogo **Proprietà pubblicazione - \<Pubblicazione>** . Per altre informazioni sull'uso della creazione guidata e l'accesso alla finestra di dialogo, vedere [Creare una pubblicazione](create-a-publication.md) e [Visualizzare e modificare le proprietà della pubblicazione](view-and-modify-publication-properties.md).    
2.  Fare clic su **Proprietà articolo**, quindi su **Imposta proprietà dell'articolo di tabella evidenziato** o su **Imposta proprietà di tutti gli articoli di tabelle**.    
3.  Nella pagina **Proprietà articolo - \<Articolo>** o **Proprietà di tutti gli articoli - \<Tipo articolo>** fare clic sulla scheda **Sistema di risoluzione**.    
4.  Selezionare **Consenti la risoluzione interattiva dei conflitti nel Sottoscrittore durante la sincronizzazione su richiesta**.    
5.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]    
6.  Se è visualizzata la finestra di dialogo **Proprietà pubblicazione - \<Pubblicazione>** fare clic su **OK** per salvare e chiudere la finestra di dialogo.  
  
#### <a name="to-specify-that-a-subscription-should-use-interactive-conflict-resolution"></a>Per specificare che in una sottoscrizione dovrà essere utilizzata la risoluzione interattiva dei conflitti  
  
1.  Nella finestra di dialogo **Proprietà sottoscrizione - \<Sottoscrittore>: \<DatabaseSottoscrizione>** specificare un valore **True** per l'opzione **Risoluzione interattiva dei conflitti**. Per ulteriori informazioni sull'accesso a questa finestra di dialogo, vedere [View and Modify Push Subscription Properties](../view-and-modify-push-subscription-properties.md) e [View and Modify Pull Subscription Properties](../view-and-modify-pull-subscription-properties.md). 
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
### <a name="using-transact-sql"></a>Utilizzo di Transact-SQL  
 È possibile impostare a livello di programmazione un Sottoscrittore in modo che utilizzi questa interfaccia grafica per risolvere conflitti relativi agli articoli quando viene creata una sottoscrizione pull di una pubblicazione di tipo merge. Nel sistema di risoluzione interattivo verranno visualizzati solo i conflitti relativi ad articoli che supportano questa opzione.  
  
#### <a name="create-a-merge-pull-subscription-that-uses-the-interactive-resolver"></a>Creare una sottoscrizione pull di tipo merge che usa il sistema di risoluzione interattivo  
  
1.  Nel database di pubblicazione del server di pubblicazione eseguire [sp_helpmergearticle](/sql/relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql), specificando **@publication** . Notare il valore di **allow_interactive_resolver** relativo a ogni articolo nel set di risultati per il quale verrà utilizzato il sistema di risoluzione interattivo.    
    -   Se questo valore è **1**, il sistema di risoluzione interattivo verrà utilizzato.    
    -   Se questo valore è **0**, è prima necessario attivare il sistema di risoluzione interattivo per ogni articolo. A tale scopo, eseguire [sp_changemergearticle](/sql/relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql), specificando **@publication** , **@article** , il valore **allow_interactive_resolver** per **@property** e il valore **true** per **@value** .    
2.  Nel database di sottoscrizione del Sottoscrittore eseguire [sp_addmergepullsubscription](/sql/relational-databases/system-stored-procedures/sp-addmergepullsubscription-transact-sql). Per altre informazioni, vedere [Creazione di una sottoscrizione pull](../create-a-pull-subscription.md).    
3.  Nel database di sottoscrizione del Sottoscrittore eseguire [sp_addmergepullsubscription_agent](/sql/relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql)specificando i parametri seguenti:  
  
    -   **@publisher** , **@publisher_db** (database pubblicato) e **@publication** .    
    -   Il valore **true** per **@enabled_for_syncmgr** .    
    -   Il valore **true** per **@use_interactive_resolver** .    
    -   Le informazioni sull'account di sicurezza richieste dall'agente di merge. Per altre informazioni, vedere [Create a Pull Subscription](../create-a-pull-subscription.md).    
4.  Nel database di pubblicazione del server di pubblicazione eseguire [sp_addmergesubscription](/sql/relational-databases/system-stored-procedures/sp-addmergesubscription-transact-sql).  
  
#### <a name="define-an-article-that-supports-the-interactive-resolver"></a>Definire un articolo che supporta il sistema di risoluzione interattivo  
  
Nel database di pubblicazione del server di pubblicazione eseguire [sp_addmergearticle](/sql/relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql). Specificare il nome della pubblicazione cui appartiene l'articolo per **@publication** , il nome dell'articolo per **@article** , l'oggetto di database da pubblicare per **@source_object** e il valore **true** per **@allow_interactive_resolver** . Per altre informazioni, vedere [definire un articolo](define-an-article.md).  

## <a name="specify-the-conflict-tracking-and-resolution-level"></a>Specificare il livello di risoluzione e rilevamento dei conflitti 
Quando si sincronizza una sottoscrizione di una pubblicazione di tipo merge, la replica verifica la presenza di conflitti causati dalle modifiche apportate agli stessi dati nel server di pubblicazione e nel Sottoscrittore. È possibile specificare se rilevare i conflitti a livello di riga, ovvero considerare un conflitto qualsiasi modifica apportata alla riga, o a livello di colonna, ovvero considerare un conflitto solo le modifiche apportate alla stessa riga e colonna. La risoluzione dei conflitti relativi agli articoli viene eseguita a livello di riga. Per ulteriori informazioni sul rilevamento e sulla risoluzione dei conflitti in caso di utilizzo dei record logici, vedere [Detecting and Resolving Conflicts in Logical Records](../merge/advanced-merge-replication-conflict-resolving-in-logical-record.md).  
  

  
###  <a name="Restrictions"></a> Limitazioni e restrizioni  
  
-   Se si modifica il livello di rilevamento in seguito all'inizializzazione delle sottoscrizioni, sarà necessario reinizializzarle. Per altre informazioni sugli effetti delle modifiche delle proprietà, vedere [Modificare le proprietà di pubblicazioni e articoli](../publish/change-publication-and-article-properties.md).    
-   Con il rilevamento a livello di riga e di colonna, la risoluzione dei conflitti viene sempre eseguita a livello di riga, ovvero la riga che prevale sovrascrive quella perdente. La replica di tipo merge consente inoltre di specificare che i conflitti vengano rilevati e risolti a livello di record logico. Queste opzioni tuttavia non sono disponibili in [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]. Per informazioni sulla relativa impostazione dalle stored procedure di replica, vedere [Definizione di una relazione tra record logici degli articoli di tabelle di merge](../publish/define-a-logical-record-relationship-between-merge-table-articles.md).  
  
###  <a name="SSMSProcedure"></a> Utilizzo di SQL Server Management Studio  
 Specificare il rilevamento a livello di riga o colonna per gli articoli di merge nella scheda **Proprietà** della finestra di dialogo **Proprietà articolo**, disponibile nella Creazione guidata nuova pubblicazione e nella finestra di dialogo **Proprietà pubblicazione - \<Pubblicazione>** . Per altre informazioni sull'uso della creazione guidata e l'accesso alla finestra di dialogo, vedere [Creare una pubblicazione](create-a-publication.md) e [Visualizzare e modificare le proprietà della pubblicazione](../publish/view-and-modify-publication-properties.md).  
  
#### <a name="specify-row--or-column-level-tracking"></a>Specificare il rilevamento a livello di riga o di colonna  
  
1.  Selezionare una tabella nella pagina **Articoli** della Creazione guidata nuova pubblicazione o nella finestra di dialogo **Proprietà pubblicazione - \<Pubblicazione>** .    
2.  Fare clic su **Proprietà articolo**, quindi su **Imposta proprietà dell'articolo di tabella evidenziato** o su **Imposta proprietà di tutti gli articoli di tabelle**.   
3.  Nella scheda **Proprietà** della finestra di dialogo **Proprietà articolo \<Articolo>** selezionare uno dei valori seguenti per la proprietà **Livello rilevamento**: **Rilevamento a livello di riga** o **Rilevamento a livello di colonna**.    
4.  Se è visualizzata la finestra di dialogo **Proprietà pubblicazione - \<Pubblicazione>** fare clic su **OK** per salvare e chiudere la finestra di dialogo.  
  
###  <a name="using-transact-sql"></a>Utilizzo di Transact-SQL  
  
#### <a name="specify-conflict-tracking-options-for-a-new-merge-article"></a>Specificare le opzioni per un nuovo articolo di merge di rilevamento dei conflitti  
  
1.  Nel database di pubblicazione del server di pubblicazione eseguire [sp_addmergearticle](/sql/relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql) e specificare uno dei valori seguenti per **@column_tracking** :  
  
    -   **true** : consente di utilizzare il rilevamento a livello di colonna per l'articolo.    
    -   **false** : consente di utilizzare il rilevamento a livello di riga, che corrisponde all'impostazione predefinita.  
  
#### <a name="change-conflict-tracking-options-for-a-merge-article"></a>Modificare le opzioni di rilevamento dei conflitti per un articolo di merge  
  
1.  Per determinare le opzioni di rilevamento dei conflitti per un articolo di merge, eseguire [sp_helpmergearticle](/sql/relational-databases/system-stored-procedures/sp-helpmergearticle-transact-sql). Notare il valore dell'opzione **column_tracking** nel set di risultati relativo l'articolo. Il valore **1** indica che viene utilizzato il rilevamento a livello di colonna, mentre il valore **0** indica che viene utilizzato il rilevamento a livello di riga.    
2.  Nel database di pubblicazione del server di pubblicazione eseguire [sp_changemergearticle](/sql/relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql). Specificare il valore **column_tracking** per **@property** e uno dei valori seguenti per **@value** :
    -   **true** : consente di utilizzare il rilevamento a livello di colonna per l'articolo.
    -   **false** : consente di utilizzare il rilevamento a livello di riga, che corrisponde all'impostazione predefinita.  
  
     Specificare il valore **1** sia per **@force_invalidate_snapshot** e **@force_reinit_subscription** .  

## <a name="tracking-deletes"></a>Rilevamento delle eliminazioni

> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../../includes/ssnotedepfutureavoid-md.md)]  
  
 Per impostazione predefinita, la replica di tipo merge consente di sincronizzare i comandi DELETE tra server di pubblicazione e Sottoscrittore. Con la replica di tipo merge le righe vengono mantenute nel database di sottoscrizione anche se sono state eliminate dalla pubblicazione e viceversa. È possibile specificare a livello di programmazione che i comandi DELETE vengano ignorati durante la creazione di un nuovo articolo oppure attivare questa funzionalità in un secondo momento utilizzando le stored procedure di replica.  
  
> [!IMPORTANT]  
>  L'attivazione di questa funzionalità causa la non convergenza pertanto i dati presenti nel Sottoscrittore non rifletteranno accuratamente i dati presenti nel server di pubblicazione. È necessario implementare un meccanismo personalizzato per la rimozione manuale delle righe eliminate.  
  
### <a name="specify-that-deletes-be-ignored-for-a-new-merge-article"></a>Specificare di ignorare le eliminazioni per un nuovo articolo di merge  
  
1.  Nel database di pubblicazione del server di pubblicazione eseguire [sp_addmergearticle &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql). Specificare il valore `false` per **@delete_tracking** . Per altre informazioni, vedere [definire un articolo](../publish/define-an-article.md).  
  
    > [!NOTE]  
    >  Se la tabella di origine di un articolo è già pubblicata in un'altra pubblicazione, il valore di **delete_tracking** deve essere uguale per entrambi gli articoli.  
  
### <a name="specify-that-deletes-be-ignored-for-an-existing-merge-article"></a>Specificare di ignorare le eliminazioni per un articolo di merge esistente  
  
1.  Per determinare se la compensazione errori è abilitata per un articolo, eseguire [sp_helpmergearticle &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-helpmergearticle-transact-sql) e prendere nota del valore di **delete_tracking** nel set di risultati. Se questo valore è **0**, le eliminazioni vengono già ignorate.    
2.  Se il valore ottenuto al passaggio 1 è **1**, eseguire [sp_changemergearticle &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql) nel database di pubblicazione del server di pubblicazione. Specificare il valore **delete_tracking** per **@property** e il valore `false` per **@value** .  
  
    > [!NOTE]  
    >  Se la tabella di origine di un articolo è già pubblicata in un'altra pubblicazione, il valore di **delete_tracking** deve essere uguale per entrambi gli articoli.  
  
## <a name="processing-order"></a>Ordine di elaborazione
  La replica di tipo merge consente di specificare l'ordine in cui gli articoli vengono elaborati dall'agente di merge durante il processo di sincronizzazione. È possibile assegnare a livello di programmazione un ordine a ogni articolo creato utilizzando le stored procedure di replica. Gli articoli vengono elaborati in ordine crescente in base al valore. Se due articoli hanno lo stesso valore, essi vengono elaborati simultaneamente. Per altre informazioni, vedere [Specificare le proprietà della replica di tipo merge](../publish/specify-merge-replication-properties.md).  

  A partire da [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], è possibile eseguire l'override dell'ordine predefinito dell'elaborazione degli articoli per le pubblicazioni di tipo merge. Ciò risulta utile, ad esempio, se si definisce l'integrità referenziale tramite trigger e tali trigger devono essere attivati in un determinato ordine. 

### <a name="how-processing-order-is-determined"></a>Modalità di determinazione dell'ordine di elaborazione  
 Durante la sincronizzazione di tipo merge, gli articoli vengono elaborati per impostazione predefinita nell'ordine richiesto dalle dipendenze tra gli oggetti, inclusi i vincoli di integrità referenziale dichiarativa definiti nelle tabelle di base. L'elaborazione prevede l'enumerazione delle modifiche apportate a una tabella e quindi l'applicazione di tali modifiche. Se non è presente l'integrità referenziale dichiarativa ma esistono filtri join o record logici tra gli articoli di tabella, gli articoli vengono elaborati nell'ordine richiesto dai filtri e dai record logici. Gli articoli non correlati ad altri articoli tramite integrità referenziale dichiarativa, filtri join, record logici o altre dipendenze vengono elaborati in base al nome alternativo dell'articolo nella tabella di sistema [sysmergearticles &#40;Transact-SQL&#41;](/sql/relational-databases/system-tables/sysmergearticles-transact-sql).  
  
 Si consideri una pubblicazione in cui sono incluse le tabelle **SalesOrderHeader** e **SalesOrderDetail** con una colonna chiave primaria **SalesOrderID** nella tabella **SalesOrderHeader** e una colonna chiave esterna **SalesOrderID** corrispondente nella tabella **SalesOrderDetail** . Durante la sincronizzazione, la replica di tipo merge impedisce le violazioni della chiave esterna inserendo nuove righe in **SalesOrderHeader** prima dell'inserimento delle righe associate in **SalesOrderDetail**. Analogamente, le righe vengono eliminate da **SalesOrderDetail** prima dell'eliminazione delle righe associate da **SalesOrderHeader**.  
  
 In alcune applicazioni, tuttavia, l'integrità referenziale viene applicata tramite trigger di database o a livello di applicazione, anziché tramite integrità referenziale dichiarativa. Nel caso della pubblicazione sopra descritta, anziché utilizzare l'integrità referenziale dichiarativa, la tabella **SalesOrderDetail** potrebbe disporre di un trigger di inserimento in grado di verificare l'esistenza della riga associata nella tabella **SalesOrderHeader** prima di consentire un inserimento. **SalesOrderHeader** potrebbe disporre di un trigger di eliminazione in grado di verificare l'assenza di righe associate in **SalesOrderDetail** prima di consentire un'eliminazione. I trigger non vengono presi in considerazione nella replica di tipo merge per determinare l'ordine di elaborazione degli articoli, poiché non è possibile determinare il risultato del trigger finché non viene attivato. Analogamente, nella replica non possono essere considerati i vincoli definiti a livello di applicazione.  
  
 In caso di mantenimento dell'integrità referenziale tramite trigger o a livello di applicazione, è consigliabile specificare l'ordine in cui gli articoli devono essere elaborati. Nell'esempio con i trigger, verrà specificato che la tabella **SalesOrderHeader** deve essere elaborata prima di **SalesOrderDetail**, poiché l'ordine degli articoli è basato sull'ordine di inserimento. Nella replica di tipo merge verrà automaticamente invertito l'ordine per le eliminazioni. La replica di tipo merge non avrà esito negativo se gli articoli non vengono ordinati, poiché l'agente di merge continua a elaborare gli articoli in caso di violazione di un vincolo e quindi ripete le operazioni non riuscite dopo l'elaborazione degli altri articoli. Specificando l'ordine degli articoli è semplicemente possibile evitare i successivi tentativi e l'elaborazione aggiuntiva associata. Se si specifica un ordine non corretto, ad esempio un ordine che determina l'elaborazione dei record di dettagli prima dei record di intestazione, la replica di tipo merge ripeterà l'elaborazione finché non avrà esito positivo.  

### <a name="new-article"></a>Nuovo articolo
  
1.  Nel database di pubblicazione del server di pubblicazione eseguire [sp_addmergearticle &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql). Specificare un valore integer che rappresenta l'ordine di elaborazione per l'articolo per **@processing_order** . Per altre informazioni, vedere [definire un articolo](define-an-article.md).  
  
    > [!NOTE]  
    >  Quando si creano articoli ordinati, è necessario lasciare gap tra i valori relativi all'ordine degli articoli. In questo modo risulta più agevole impostare nuovi valori in futuro. Se ad esempio si dispone di tre articoli per cui è necessario specificare un ordine di elaborazione fisso, impostare il valore di **@processing_order** su 10, 20 e 30 anziché rispettivamente su 1, 2 e 3.  
  
### <a name="existing-article"></a>Articolo esistente
  
1.  Per determinare l'ordine di elaborazione di un articolo, eseguire [sp_helpmergearticle &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-helpmergearticle-transact-sql) e prendere nota del valore di **processing_order** nel set di risultati.  
  
2.  Nel database di pubblicazione del server di pubblicazione eseguire [sp_changemergearticle &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql). Specificare il valore **processing_order** per **@property** e un valore integer che rappresenta l'ordine di elaborazione per **@value** .  



## <a name="see-also"></a>Vedere anche  
 [Ottimizzare le prestazioni della replica di tipo merge con il rilevamento condizionale delle eliminazioni](../merge/optimize-merge-replication-performance-with-conditional-delete-tracking.md)  
 [Detecting and Resolving Conflicts in Logical Records](../merge/advanced-merge-replication-conflict-resolving-in-logical-record.md)   
 [Define a Logical Record Relationship Between Merge Table Articles](define-a-logical-record-relationship-between-merge-table-articles.md)   
 [Rilevare e risolvere i conflitti tra repliche di tipo Merge](../merge/advanced-merge-replication-conflict-detection-and-resolution.md)   
 [Ottimizzare le prestazioni della replica di tipo merge con gli articoli di solo download](../merge/optimize-merge-replication-performance-with-download-only-articles.md)   
 [Define an Article](define-an-article.md)   
 [Visualizzare e modificare le proprietà degli articoli](view-and-modify-article-properties.md)  