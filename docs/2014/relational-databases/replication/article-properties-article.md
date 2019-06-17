---
title: Proprietà articolo - &lt;Articolo&gt; | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.newpubwizard.articleproperties.f1
helpviewer_keywords:
- Article Properties dialog box
ms.assetid: 6dd601a4-1233-43d9-a9f0-bc8d84e5d188
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 2903eef63152af9b2e9af1434ba12ea91b4058fc
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62721783"
---
# <a name="article-properties---ltarticlegt"></a>Proprietà articolo - &lt;Articolo&gt;
  È possibile accedere alla finestra **Proprietà articolo** dalla Creazione guidata nuova pubblicazione e dalla finestra di dialogo **Proprietà pubblicazione** . Questa finestra di dialogo consente di visualizzare e impostare le proprietà per tutti i tipi di articoli. Alcune proprietà possono essere impostate solo dopo aver creato la pubblicazione, mentre altre possono essere impostate solo se la pubblicazione non dispone di sottoscrizioni attive. Le proprietà non impostabili vengono visualizzate in sola lettura.  
  
> [!NOTE]  
>  Dopo la creazione di una pubblicazione, per alcune modifiche delle proprietà è necessario un nuovo snapshot. Se la pubblicazione dispone di sottoscrizioni, per alcune modifiche è inoltre necessario reinizializzare tutte le sottoscrizioni. Per altre informazioni, vedere [Modificare le proprietà di pubblicazioni e articoli](publish/change-publication-and-article-properties.md).  
  
 Ogni proprietà nella finestra di dialogo **Proprietà articolo** contiene una descrizione. Fare clic su una proprietà per visualizzarne la descrizione nella parte inferiore della finestra di dialogo. In questo argomento sono specificate informazioni aggiuntive su diverse proprietà. Le proprietà sono raggruppate nelle categorie seguenti:  
  
-   Proprietà che si applicano a tutte le pubblicazioni di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   Proprietà che si applicano alle pubblicazioni transazionali di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   Proprietà che si applicano alle pubblicazioni di tipo merge.  
  
-   Proprietà che si applicano alle pubblicazioni transazionali e snapshot di server di pubblicazione Oracle.  
  
## <a name="options-for-all-publications"></a>Opzioni per tutte le pubblicazioni  
 **Copia schemi di partizione delle tabelle** e **Copia schemi di partizione dell'indice**  
 In[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] sono state introdotte la partizione della tabella e la partizione dell'indice, caratteristiche non correlate alla replica di partizionamento ottenuta tramite filtri di riga e di colonna. Le opzioni **Copia schemi di partizione delle tabelle** e **Copia schemi di partizione dell'indice** consentono di specificare se gli schemi di partizione devono essere copiati nel Sottoscrittore. Per ulteriori informazioni sul partizionamento, vedere [Partitioned Tables and Indexes](../partitions/partitioned-tables-and-indexes.md).  
  
 **Converti tipi di dati**  
 Determina se convertire tipi di dati definiti dall'utente in tipi di dati di base durante la creazione di oggetti nel Sottoscrittore. I tipi di dati definiti dall'utente includono i tipi di dati CLR definiti dall'utente introdotti in [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]. Specificare il valore **True** se questi tipi di dati verranno replicati in versioni precedenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]per garantire che vengano gestiti correttamente nel Sottoscrittore.  
  
 **Crea schemi nel Sottoscrittore**  
 In[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] sono stati introdotti gli schemi, che vengono definiti utilizzando l'istruzione CREATE SCHEMA. Uno schema è il proprietario di un oggetto e viene utilizzato in un nome in più parti, ad esempio \<Database>.\<Schema>.\<Oggetto>. Se nel database esistono oggetti di proprietà di schemi diversi da DBO, la replica è in grado di creare tali schemi nel Sottoscrittore in modo che sia possibile creare gli oggetti pubblicati.  
  
 Se i dati verranno replicati in versioni [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] precedenti a [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]:  
  
-   Impostare questa opzione su **False**, poiché le versioni precedenti non supportano l'istruzione CREATE SCHEMA.  
  
-   Per ogni schema, aggiungere un utente al database di sottoscrizione utilizzando lo stesso nome dello schema.  
  
 **Converti tipi di dati XML in NTEXT**, **Converti tipi di dati MAX in NTEXT e IMAGE**, **Converti nuovi tipi datetime in NVARCHAR**, **Converti tipo FILESTREAM in tipi di dati MAX**, **Converti tipo CLR di grandi dimensioni in tipi di dati MAX**, **Converti tipo hierarchyId in tipi di dati MAX**e **Converti tipo spaziale in tipi di dati MAX**.  
 Determina se convertire i tipi di dati e gli attributi come descritto. Specificare il valore **True** se si intende replicare questi tipi di dati in versioni precedenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. In questo modo i tipi di dati verranno gestiti correttamente nel Sottoscrittore.  
  
 **Nome oggetto di destinazione**  
 Nome dell'oggetto creato nel database di sottoscrizione. Non è possibile modificare questa opzione per articoli contenuti in pubblicazioni abilitate per la replica transazionale peer-to-peer.  
  
 **Proprietario oggetto di destinazione**  
 Schema con cui è stato creato l'oggetto nel database di sottoscrizione. L'impostazione predefinita è rappresentata dallo schema al quale appartiene l'oggetto nel database di pubblicazione, con le eccezioni seguenti:  
  
-   Per articoli contenuti in pubblicazioni di tipo merge con un livello di compatibilità inferiore a 90: per impostazione predefinita, il proprietario viene lasciato vuoto e viene specificato come **dbo** durante la creazione dell'oggetto nel Sottoscrittore.  
  
-   Per articoli contenuti in pubblicazioni Oracle: per impostazione predefinita, viene specificato il proprietario **dbo**.  
  
-   Per articoli di pubblicazioni che usano snapshot in modalità carattere (usati per Sottoscrittori non[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e Sottoscrittori [!INCLUDE[ssEW](../../includes/ssew-md.md)] ): per impostazione predefinita, il proprietario rimane vuoto. Il proprietario viene impostato sul proprietario associato all'account utilizzato dall'agente di distribuzione o dall'agente di merge per la connessione al Sottoscrittore.  
  
 Non è possibile modificare questa opzione per articoli contenuti in pubblicazioni abilitate per la replica transazionale peer-to-peer.  
  
 **Gestisci automaticamente gli intervalli di valori Identity**  
 Per impostazione predefinita, la replica gestisce tutte le colonne Identity nel server di pubblicazione e in ogni Sottoscrittore. A ogni nodo di replica viene assegnato un intervallo di valori Identity, specificato con le opzioni **Dimensioni intervallo server di pubblicazione** e **Dimensioni intervallo Sottoscrittore** , per garantire che un determinato risultato venga utilizzato in un solo nodo. Per altre informazioni, vedere [Replicare colonne Identity](publish/replicate-identity-columns.md).  
  
## <a name="options-for-transactional-publications"></a>Opzioni per le pubblicazioni transazionali  
 **Copia stored procedure INSERT, UPDATE e DELETE**  
 Se nella sezione **Recapito istruzione** di questa finestra di dialogo si sceglie di utilizzare le stored procedure per propagare le modifiche ai Sottoscrittori (impostazione predefinita), specificare se copiare le procedure in ogni Sottoscrittore. Se si seleziona **False**, sarà necessario copiare le procedure in modo manuale, poiché diversamente il tentativo di recapito delle modifiche da parte dell'agente di distribuzione avrà esito negativo.  
  
 **Statement delivery**  
 Le opzioni contenute in questa sezione si applicano a tutte le tabelle, incluse le viste indicizzate che vengono replicate come tabelle. [!INCLUDE[msCoName](../../includes/msconame-md.md)] consiglia di utilizzare le opzioni predefinite, a meno che l'applicazione utilizzata non richieda caratteristiche diverse. Per impostazione predefinita, la replica transazionale propaga le modifiche ai Sottoscrittori utilizzando un set di stored procedure installate in ogni Sottoscrittore. Quando viene eseguito un inserimento, un aggiornamento o un'eliminazione in una tabella nel server di pubblicazione, l'operazione viene tradotta in una chiamata alla stored procedure nel Sottoscrittore.  
  
 Le opzioni relative al **recapito dell'istruzione** consentono di specificare se utilizzare una stored procedure e quale formato deve essere utilizzato per i parametri passati alla procedura. Le opzioni relative alla **stored procedure** consentono di utilizzare le procedure create automaticamente dalla replica o di sostituire le procedure personalizzate create dall'utente.  
  
 Per altre informazioni, vedere [Specificare la modalità di propagazione delle modifiche per gli articoli transazionali](transactional/transactional-articles-specify-how-changes-are-propagated.md).  
  
 **Replica**  
 Questa opzione si applica solo alle stored procedure e determina se replicare la definizione della stored procedure, ovvero l'istruzione CREATE PROCEDURE, oppure la relativa esecuzione. Se si replica l'esecuzione della procedura, la definizione della procedura viene replicata nel Sottoscrittore nel momento in cui la sottoscrizione viene inizializzata. Quando la procedura viene eseguita nel server di pubblicazione, il processo di replica esegue la procedura corrispondente nel Sottoscrittore. Ciò consente di ottenere un miglioramento significativo delle prestazioni nel caso in cui vengano eseguite operazioni su batch di grandi dimensioni. Per altre informazioni, vedere [Publishing Stored Procedure Execution in Transactional Replication](transactional/publishing-stored-procedure-execution-in-transactional-replication.md).  
  
## <a name="options-for-merge-publications"></a>Opzioni per le pubblicazioni di tipo merge  
 La finestra di dialogo **Proprietà articolo** per le pubblicazioni di tipo merge dispone di due schede: **Proprietà** e **Sistema di risoluzione**.  
  
### <a name="properties-tab"></a>Scheda Proprietà  
 **Direzione sincronizzazione**  
 Determina se le modifiche possono essere caricate dai Sottoscrittori che utilizzano il tipo di sottoscrizione client:  
  
-   **Bidirezionale** (valore predefinito): le modifiche possono essere scaricate nel Sottoscrittore e caricate nel server di pubblicazione.  
  
-   **Solo download sul Sottoscrittore, non consentire modifiche del Sottoscrittore**: le modifiche possono essere scaricate nel Sottoscrittore ma non possono essere caricate nel server di pubblicazione. I trigger impediscono che le modifiche vengano apportate al Sottoscrittore.  
  
-   **Solo download sul Sottoscrittore, consenti modifiche del Sottoscrittore**: le modifiche possono essere scaricate nel Sottoscrittore ma non possono essere caricate nel server di pubblicazione.  
  
 Per altre informazioni, vedere [Ottimizzare le prestazioni della replica di tipo merge con gli articoli di solo download](merge/optimize-merge-replication-performance-with-download-only-articles.md).  
  
 **Opzioni partizioni**  
 Specifica il tipo di partizioni create da un filtro con parametri. Per ulteriori informazioni, vedere la sezione Impostazione delle opzioni delle partizioni in [Parameterized Row Filters](merge/parameterized-filters-parameterized-row-filters.md).  
  
 **Livello rilevamento**  
 Determina se gestire come conflitto le modifiche apportate alla stessa riga o alla stessa colonna.  
  
 **Verifica autorizzazione INSERT**, **Verifica autorizzazione UPDATE**e **Verifica autorizzazione DELETE**  
 Determina se durante la sincronizzazione viene controllata la disponibilità delle autorizzazioni INSERT, UPDATE o DELETE da parte dell'account di accesso del Sottoscrittore per le tabelle pubblicate nel database di pubblicazione. Il valore predefinito è **False** poiché per la replica di tipo merge non è necessario disporre di tali autorizzazioni. L'accesso alle tabelle pubblicate viene controllato tramite l'elenco di accesso alla pubblicazione. Per altre informazioni sull'elenco di acceso alla pubblicazione, vedere [Proteggere il server di pubblicazione](security/secure-the-publisher.md).  
  
 È possibile richiedere che vengano verificate le autorizzazioni se si desidera consentire a uno o più Sottoscrittori di caricare solo determinate modifiche nei dati pubblicati. Ad esempio, è possibile aggiungere un Sottoscrittore all'elenco di accesso alla pubblicazione senza concedere al Sottoscrittore alcuna autorizzazione per le tabelle contenute nel database di pubblicazione. È quindi possibile impostare l'opzione Verifica autorizzazioni DELETE su **True**in modo che il Sottoscrittore sia in grado di caricare inserimenti e aggiornamenti, ma non eliminazioni.  
  
 **UPDATE multicolonna**  
 Quando la replica di tipo merge esegue un aggiornamento, vengono aggiornate tutte le colonne modificate in un'unica istruzione UPDATE e reimpostati i valori originali per le colonne non modificate. L'alternativa in questi casi consiste nell'inoltrare più istruzioni UPDATE, con una istruzione UPDATE per ogni colonna che ha subito modifiche. L'istruzione UPDATE multicolonna risulta in genere più efficiente, ma è consigliabile valutare la possibilità di impostare l'opzione su **False** nel caso in cui i trigger nella tabella siano impostati per rispondere agli aggiornamenti di determinate colonne e rispondano in maniera non appropriata a causa del ripristino di tali colonne durante gli aggiornamenti.  
  
> [!IMPORTANT]  
>  questa opzione è deprecata e verrà rimossa a partire da una delle prossime versioni.  
  
### <a name="resolver-tab"></a>Scheda Sistema di risoluzione  
 **Usa il sistema di risoluzione predefinito**  
 Se si seleziona il sistema di risoluzione predefinito, i conflitti vengono risolti in base alla priorità assegnata a ogni Sottoscrittore o alla prima modifica scritta nel server di pubblicazione, a seconda del tipo di sottoscrizioni utilizzate. Per altre informazioni, vedere [Rilevare e risolvere i conflitti tra repliche di tipo merge](merge/advanced-merge-replication-conflict-detection-and-resolution.md).  
  
 **Usa un sistema di risoluzione personalizzato (registrato nel server di distribuzione)**  
 Se si sceglie di utilizzare un sistema di risoluzione dei conflitti dell'articolo fornito da [!INCLUDE[msCoName](../../includes/msconame-md.md)] o scritto dall'utente, è necessario selezionare un sistema di risoluzione nella casella di riepilogo. Per altre informazioni, vedere [Advanced Merge Replication Conflict Detection and Resolution](merge/advanced-merge-replication-conflict-detection-and-resolution.md).  
  
 Se il sistema di risoluzione necessita di un input, specificarlo nella casella di testo **Immettere le informazioni necessarie per il sistema di risoluzione** . Per ulteriori informazioni sull'input richiesto dai sistemi di risoluzione dei conflitti personalizzati forniti da [!INCLUDE[msCoName](../../includes/msconame-md.md)] , vedere [Microsoft COM-Based Resolvers](merge/advanced-merge-replication-conflict-com-based-resolvers.md).  
  
 **Consenti la risoluzione interattiva dei conflitti nel Sottoscrittore durante la sincronizzazione su richiesta**  
 Selezionare questa opzione se i Sottoscrittori utilizzeranno la sincronizzazione su richiesta, ovvero l'impostazione predefinita per la replica di tipo merge, e si desidera risolvere i conflitti in modo interattivo. Specificare la sincronizzazione su richiesta nella pagina **Pianificazione della sincronizzazione** della Creazione guidata nuova sottoscrizione. Per risolvere i conflitti in modo interattivo, utilizzare l'interfaccia utente del sistema di risoluzione dei conflitti interattivo. Per altre informazioni, vedere [Interactive Conflict Resolution](merge/advanced-merge-replication-conflict-interactive-resolution.md).  
  
 **Prima di eseguire il processo di merge, richiedi la verifica della firma digitale**  
 Tutti i sistemi di risoluzione dei conflitti basati su COM forniti da [!INCLUDE[msCoName](../../includes/msconame-md.md)] sono firmati. Selezionare questa opzione per verificare la validità del sistema di risoluzione dei conflitti durante la sincronizzazione.  
  
## <a name="options-for-oracle-publications"></a>Opzioni per le pubblicazioni Oracle  
 La finestra di dialogo **Proprietà articolo** per le pubblicazioni Oracle dispone di due schede: **Proprietà** e **Mapping dei dati**. Le pubblicazioni Oracle non supportano tutte le proprietà supportate dalle pubblicazioni [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Per altre informazioni, vedere [Design Considerations and Limitations for Oracle Publishers](non-sql/design-considerations-and-limitations-for-oracle-publishers.md).  
  
### <a name="properties-tab"></a>Scheda Proprietà  
 **Copia stored procedure INSERT, UPDATE e DELETE**  
 Se l'articolo si trova in una pubblicazione transazionale e nella sezione **Recapito istruzione** di questa finestra di dialogo si sceglie di utilizzare le stored procedure per propagare modifiche ai Sottoscrittori (impostazione predefinita), specificare se copiare le procedure in ogni Sottoscrittore. Se si seleziona **False**, sarà necessario copiare le procedure in modo manuale, poiché diversamente il tentativo di recapito delle modifiche da parte dell'agente di distribuzione avrà esito negativo.  
  
 **Proprietario oggetto di destinazione**  
 Se si immette un valore diverso da **dbo**:  
  
-   Per i Sottoscrittori che eseguono [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] o versione successiva è necessario garantire che lo schema venga creato nel Sottoscrittore con lo stesso nome del valore immesso. Per altre informazioni, vedere [CREATE SCHEMA &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-schema-transact-sql).  
  
-   Per i Sottoscrittori che eseguono versioni di SQL Server precedenti a [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], per ogni schema aggiungere un utente al database di sottoscrizione utilizzando lo stesso nome dello schema.  
  
 **Nome spazio tabella**  
 Spazio tabella in cui creare le tabelle per il rilevamento delle modifiche della replica nell'istanza del server Oracle. Per altre informazioni, vedere [Gestire spazi di tabella Oracle](non-sql/manage-oracle-tablespaces.md).  
  
 **Statement delivery**  
 Le opzioni descritte in questa sezione si applicano a tutte le tabelle contenute in pubblicazioni transazionali. [!INCLUDE[msCoName](../../includes/msconame-md.md)] consiglia di utilizzare le opzioni predefinite, a meno che l'applicazione utilizzata non richieda caratteristiche diverse. Per impostazione predefinita, la replica transazionale propaga le modifiche ai Sottoscrittori utilizzando un set di stored procedure installate in ogni Sottoscrittore. Quando viene eseguito un inserimento, un aggiornamento o un'eliminazione in una tabella nel server di pubblicazione, l'operazione viene tradotta in una chiamata alla stored procedure nel Sottoscrittore.  
  
 Le opzioni relative al **recapito dell'istruzione** consentono di specificare se utilizzare una stored procedure e quale formato deve essere utilizzato per i parametri passati alla procedura. Le opzioni relative alla **stored procedure** consentono di utilizzare le procedure create automaticamente dalla replica o di sostituire le procedure personalizzate create dall'utente.  
  
 Per altre informazioni, vedere [Specificare la modalità di propagazione delle modifiche per gli articoli transazionali](transactional/transactional-articles-specify-how-changes-are-propagated.md).  
  
### <a name="data-mapping-tab"></a>Scheda Mapping dei dati  
 **Nome colonna**  
 Nome della colonna nel server di pubblicazione (informazione di sola lettura).  
  
 **Tipo di dati server di pubblicazione**  
 Tipo di dati Oracle per la colonna nel server di pubblicazione (informazione di sola lettura). È possibile modificare direttamente il tipo di dati solo nel database Oracle. Per ulteriori informazioni, vedere la documentazione di Oracle.  
  
 **Tipo di dati del Sottoscrittore**  
 Tipo di dati [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a cui viene eseguito il mapping del tipo di dati Oracle durante la replica dei dati:  
  
-   Per alcuni tipi di dati è disponibile un solo tipo di mapping. In questo caso, la colonna nella proprietà è di sola lettura.  
  
-   Per alcuni tipi è possibile selezionare più tipi di mapping. [!INCLUDE[msCoName](../../includes/msconame-md.md)] consiglia di utilizzare il mapping predefinito, a meno che l'applicazione utilizzata non richieda un tipo di mapping diverso. Per altre informazioni, vedere [Data Type Mapping for Oracle Publishers](non-sql/data-type-mapping-for-oracle-publishers.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Create a Publication](publish/create-a-publication.md)   
 [Visualizzare e modificare le proprietà della pubblicazione](publish/view-and-modify-publication-properties.md)   
 [Creare e applicare lo snapshot iniziale](create-and-apply-the-initial-snapshot.md)   
 [Reinizializzare una sottoscrizione](reinitialize-a-subscription.md)   
 [Pubblicare dati e oggetti di database](publish/publish-data-and-database-objects.md)  
  
  
