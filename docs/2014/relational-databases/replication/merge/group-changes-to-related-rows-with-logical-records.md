---
title: Raggruppare modifiche alle righe correlate con record logici | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- merge replication logical records [SQL Server replication]
- articles [SQL Server replication], logical records
- logical records [SQL Server replication]
ms.assetid: ad76799c-4486-4b98-9705-005433041321
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 423cbb00f8c28cc1abca309c5a2d518da4511f1a
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "78175844"
---
# <a name="group-changes-to-related-rows-with-logical-records"></a>Raggruppamento di modifiche alla righe correlate con record logici
  
> [!NOTE]
>  [!INCLUDE[ssNoteDepFutureAvoid](../../../includes/ssnotedepfutureavoid-md.md)]

 Per impostazione predefinita, i dati dei processi di replica di tipo merge cambiano riga per riga. In molti casi questo comportamento è appropriato, ma per alcune applicazioni è essenziale che le righe correlate vengano elaborate come unità. La funzionalità di record logici della replica di tipo merge consente di definire una relazione tra righe correlate di tabelle diverse, in modo che le righe vengano elaborate come unità.

> [!NOTE]
>  La funzionalità di record logici può essere utilizzata da sola o unitamente a filtri join. Per ulteriori informazioni sui filtri join, vedere [Join Filters](join-filters.md). Per utilizzare i record logici, è necessario che il livello di compatibilità della pubblicazione sia almeno 90RTM.

 Si considerino le tre tabelle correlate seguenti:

 ![Record logico per tre tabelle con solo i nomi di colonna](../media/logical-records-01.gif "Record logico per tre tabelle con solo i nomi di colonna")

 La tabella **Customers** è la tabella padre in questa relazione e presenta una colonna chiave primaria **CustID**. La tabella **Orders** ha una colonna chiave primaria **OrderID**, con un vincolo di chiave esterna nella colonna **CustID** che fa riferimento alla colonna **CustID** nella tabella **Customers** . Analogamente, la tabella **OrderItems** ha una colonna chiave primaria **OrderItemID**, con un vincolo di chiave esterna nella colonna **OrderID** che fa riferimento alla colonna **OrderID** nella tabella **Orders** .

 In questo esempio un record logico è composto da tutte le righe della tabella **Orders** correlate a un unico valore di **CustID** e da tutte le righe della tabella **OrderItems** correlate a tali righe della tabella **Orders** . Nel grafico seguente vengono illustrate tutte le righe delle tre tabelle che si trovano nel record logico di Customer2:

 ![Record logico per tre tabelle con valori](../media/logical-records-02.gif "Record logico per tre tabelle con valori")

 Per definire una relazione tra record logici per gli articoli, vedere [Definizione di una relazione tra record logici degli articoli di tabelle di merge](../publish/define-a-logical-record-relationship-between-merge-table-articles.md).

## <a name="benefits-of-logical-records"></a>Vantaggi dei record logici
 La funzionalità di record logici offre due vantaggi principali:

-   Applicazione delle modifiche ai dati come unità.

-   Rilevamento e risoluzione di conflitti contemporaneamente in più righe di più tabelle.

### <a name="the-application-of-changes-as-a-unit"></a>Applicazione di modifiche come unità
 Se l'elaborazione di tipo merge viene interrotta, ad esempio nel caso di interruzione della connessione, se sono stati utilizzati record logici, viene eseguito il rollback del set parzialmente completato di modifiche replicate correlate. Si consideri, ad esempio, il caso in cui un Sottoscrittore aggiunga un nuovo ordine con **OrderID** = 6 e due nuove righe nella tabella **OrderItems** con **OrderItemID** = 10 e **OrderItemID** = 11 per **OrderID** = 6.

 ![Record logico per tre tabelle con valori](../media/logical-records-04.gif "Record logico per tre tabelle con valori")

 Se il processo di replica viene interrotto dopo che la riga **Orders** per **OrderID** = 6 è stata completata, ma prima che gli elementi 11 e 12 della tabella **OrderItems** siano completati e se i record logici non vengono utilizzati, il valore di **OrderTotal** per **OrderID** = 6 non coinciderà con la somma dei valori di **OrderAmount** per le righe di **OrderItems** . Se vengono utilizzati record logici, non verrà eseguito il commit della riga **Orders** per **OrderID** = 6 fino a quando le modifiche correlate nella tabella **OrderItems** non saranno replicate.

 In uno scenario diverso, se vengono utilizzati i record logici e si esegue una query sulle tabelle mentre il processo di tipo merge sta applicando le modifiche, l'utente non vedrà le modifiche parzialmente replicate fino a quando non saranno tutte complete. Se, ad esempio, tramite il processo di replica è stata caricata la riga Orders per **OrderID** = 6, ma un utente esegue una query sulle tabelle prima che tramite il processo di replica siano state replicate le righe di **OrderItems** , il valore di **OrderTotal** non sarà uguale alla somma dei valori di **OrderAmount** . Se vengono utilizzati record logici, la riga **Orders** non sarà visibile fino a quando le righe di **OrderItems** non saranno complete e non sarà stato eseguito il commit della transazione come unità.

### <a name="the-application-of-conflict-handling-to-more-than-one-table"></a>Applicazione della gestione dei conflitti a più di una tabella
 Si consideri il caso in cui due Sottoscrittori dispongono del set di dati illustrato in precedenza:

-   Un utente nel primo Sottoscrittore modifica il valore di **OrderAmount** per **OrderItemID** 5 da 100 a 150 e il valore di **OrderTotal** per **OrderID** 3 da 200 a 250.

-   Un utente nel secondo Sottoscrittore modifica il valore di **OrderAmount** per **OrderItemID** 6 da 25 a 125 e il valore di **OrderTotal** per **OrderID** 3 da 200 a 300.

 Se queste modifiche vengono replicate senza utilizzare record logici, i diversi valori di **OrderTotal** daranno luogo a un conflitto e solo uno di essi verrà replicato. Le modifiche non in conflitto presenti nella tabella **OrderItems** verranno tuttavia replicate senza alcun conflitto, lasciando i valori finali di **OrderTotal** in uno stato inconsistente rispetto alle righe di **OrderItems** . Se in questo scenario vengono utilizzati i record logici, verrà eseguito il rollback della modifica a **OrderItems** associata alla modifica della tabella **Orders** in perdita e il valore di **OrderTotal** finale sarà costituito da un riepilogo accurato delle righe di **OrderItems** .

 Per altre informazioni sulle opzioni correlate al rilevamento e alla risoluzione dei conflitti per i record logici, vedere [Rilevamento e risoluzione dei conflitti nei record logici](advanced-merge-replication-conflict-resolving-in-logical-record.md).

## <a name="considerations-for-using-logical-records"></a>Considerazioni sull'utilizzo di record logici
 Quando si utilizzano i record logici, tenere presenti le considerazioni seguenti:

### <a name="general-considerations"></a>Considerazioni generali

-   È consigliabile che il numero di tabelle in un record logico sia il più basso possibile, ad esempio cinque tabelle o un numero inferiore.

-   I record logici non possono fare riferimento a colonne con i tipi di dati seguenti:

    -   `varchar(max)` e `nvarchar(max)`

    -   `varbinary(max)`

    -   `text` e `ntext`

    -   `image`

    -   `XML`

    -   `UDT`

-   Le relazioni di chiavi esterne nelle tabelle pubblicate non possono essere definite mediante l'opzione CASCADE. Per altre informazioni, vedere [CREATE TABLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-table-transact-sql) e [ALTER TABLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-table-transact-sql).

-   Non è possibile aggiornare le colonne utilizzate nella clausola di relazione logica.

-   La risoluzione dei conflitti personalizzata con gestori della logica di business o sistemi di risoluzione personalizzati non è supportata per gli articoli inclusi in un record logico.

-   Se in una pubblicazione che include filtri con parametri vengono utilizzati record logici, è necessario inizializzare ogni Sottoscrittore con uno snapshot per la relativa partizione. Se si inizializza un Sottoscrittore con un altro metodo, l'agente di merge non verrà eseguito in modo corretto. Per altre informazioni, vedere [Snapshots for Merge Publications with Parameterized Filters](../snapshots-for-merge-publications-with-parameterized-filters.md).

-   I conflitti a livello di record logici non vengono visualizzati nel Visualizzatore conflitti. Per visualizzare informazioni relative a questi conflitti, utilizzare le stored procedure di replica. Per altre informazioni, vedere [Visualizzare le informazioni sui conflitti per le pubblicazioni di tipo merge &#40;programmazione Transact-SQL della replica&#41;](../view-conflict-information-for-merge-publications.md).

### <a name="publication-settings"></a>Impostazioni di pubblicazione

-   È necessario che la pubblicazione abbia un livello di compatibilità pari a 90RTM o superiore. Per altre informazioni, vedere la sezione "Livello di compatibilità della pubblicazione" in [Compatibilità con le versioni precedenti della replica](../replication-backward-compatibility.md).

-   È necessario che nella pubblicazione sia utilizzata la modalità snapshot nativa. Si tratta dell'impostazione predefinita a meno che non si esegua la replica in [!INCLUDE[ssEW](../../../includes/ssew-md.md)], che non supporta i record logici.

-   La pubblicazione non consente la sincronizzazione tramite il Web. Per ulteriori informazioni sulla sincronizzazione Web, vedere [Web Synchronization for Merge Replication](../web-synchronization-for-merge-replication.md).

-   Per utilizzare record logici in una pubblicazione filtrata:

    -   È necessario utilizzare partizioni pre-calcolate. I requisiti delle partizioni pre-calcolate si applicano anche ai record logici. Per altre informazioni, vedere [Ottimizzare le prestazioni dei filtri con parametri con le partizioni pre-calcolate](parameterized-filters-optimize-for-precomputed-partitions.md).

    -   Non è possibile utilizzare filtri con parametri non sovrapposti. Per ulteriori informazioni, vedere la sezione Impostazione delle opzioni delle partizioni in [Parameterized Row Filters](parameterized-filters-parameterized-row-filters.md).

-   Se nella pubblicazione sono utilizzati filtri join, è necessario che la proprietà **join unique key** sia impostata su **true** per tutti i filtri join coinvolti in relazioni tra record logici. Per altre informazioni, vedere [Join Filters](join-filters.md).

### <a name="relationships-between-tables"></a>Relazioni tra tabelle

-   È necessario che le tabelle correlate tramite record logici presentino una relazione tra chiave primaria e chiave esterna.

-   Non è possibile impostare l'opzione NOT FOR REPLICATION per i vincoli di chiave esterna.

-   Le tabelle figlio possono avere solo una tabella padre.

     Un database utilizzato per tenere traccia di classi e studenti potrebbe, ad esempio, avere una struttura simile alla seguente:

     ![Tabella figlio con più di una tabella padre](../media/logical-records-03.gif "Tabella figlio con più di una tabella padre")

     Non è possibile utilizzare un record logico per rappresentare le tre tabelle di questa relazione, in quanto le righe in **ClassMembers** non sono associate a una singola riga chiave primaria. Le tabelle **Classes** e **ClassMembers** potrebbero formare un record logico, così come potrebbero formarlo le tabelle **ClassMembers** e **Students**, ma non tutte e tre.

-   La pubblicazione non può contenere relazioni circolari tra filtri join.

     Utilizzando l'esempio con le tabelle **Customers**, **Orders**e **OrderItems**, non è possibile utilizzare record logici se la tabella **Orders** presenta anche un vincolo di chiave esterna che fa riferimento alla tabella **OrderItems** .

## <a name="performance-implications-of-logical-records"></a>Effetti dei record logici sulle prestazioni
 La funzionalità di record logici comporta alcuni costi relativi alle prestazioni. Se non vengono utilizzati record logici, l'agente di replica può elaborare contemporaneamente tutte le modifiche relative a un determinato articolo e poiché le modifiche vengono applicate riga per riga, i requisiti del log delle transazioni e di blocco necessari per l'applicazione di tali modifiche sono minimi.

 Se vengono utilizzati record logici, è necessario che l'agente di merge elabori insieme le modifiche per ogni record logico completo. Questa operazione influisce sulla quantità di tempo necessaria per la replica delle righe da parte dell'agente di merge. Poiché, inoltre, tramite l'agente viene aperta una transazione separata per ogni record logico, i requisiti di blocco possono aumentare.

## <a name="see-also"></a>Vedere anche
 [Opzioni degli articoli per la replica di tipo merge](article-options-for-merge-replication.md)


