---
title: Aggiungere ed eliminare articoli in pubblicazioni esistenti | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- articles [SQL Server replication], dropping
- deleting articles
- removing articles
- dropping articles
- adding articles
- administering replication, articles
- publications [SQL Server replication], adding and dropping articles
- articles [SQL Server replication], adding
ms.assetid: b148e907-e1f2-483b-bdb2-59ea596efceb
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: f72f15886e7105dde8d0e15dd0598a7474ed7e39
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85038133"
---
# <a name="add-articles-to-and-drop-articles-from-existing-publications"></a>Aggiunta ed eliminazione di articoli a e da pubblicazioni esistenti
  Dopo la creazione di una pubblicazione, è possibile aggiungere ed eliminare articoli. Gli articoli possono essere aggiunti in qualsiasi momento, ma le azioni necessarie per eliminarli dipendono dal tipo di replica e dal momento in cui avviene l'eliminazione.  
  
## <a name="adding-articles"></a>aggiunta di articoli  
 L'aggiunta di un articolo comporta l'aggiunta dell'articolo alla pubblicazione, la creazione di un nuovo snapshot per la pubblicazione e la sincronizzazione della sottoscrizione per applicare lo schema e i dati per il nuovo articolo.  
  
> [!NOTE]
>  Se si aggiunge un articolo a una pubblicazione di tipo merge e un articolo esistente dipende dal nuovo articolo, è necessario specificare un ordine di elaborazione per entrambi gli articoli utilizzando il parametro ** \@ processing_order** di [sp_addmergearticle](/sql/relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql) e [sp_changemergearticle](/sql/relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql). Si consideri lo scenario seguente: viene pubblicata una tabella, ma non viene pubblicata una funzione a cui fa riferimento la tabella. Se non si pubblica la funzione, la tabella non può essere creata nel Sottoscrittore. Quando si aggiunge la funzione alla pubblicazione: specificare il valore **1** per il parametro ** \@ processing_order** di **sp_addmergearticle**e specificare il valore **2** per il parametro ** \@ processing_order** di **sp_changemergearticle**, specificando il nome della tabella per l' ** \@ articolo**del parametro. Questo ordine di elaborazione consente di creare la funzione nel Sottoscrittore prima della tabella dipendente. È possibile utilizzare numeri diversi per ogni articolo, purché il numero per la funzione sia inferiore a quello per la tabella.  
  
1.  Aggiungere uno o più articoli tramite uno dei metodi seguenti:  
  
    -   [Aggiungere ed eliminare articoli in una pubblicazione &#40;SQL Server Management Studio&#41;](add-articles-to-and-drop-articles-from-a-publication.md)  
  
    -   [Definire un articolo](define-an-article.md)  
  
2.  Dopo avere aggiunto un articolo a una pubblicazione, è necessario creare un nuovo snapshot per la pubblicazione. Nel caso si tratti di una pubblicazione di tipo merge con filtri con parametri, sarà necessario creare tutte le partizioni. Tramite l'agente di distribuzione o l'agente di merge vengono quindi copiati lo schema e i dati per il nuovo articolo nel Sottoscrittore, senza reinizializzare l'intera pubblicazione.  
  
    -   Per creare un nuovo snapshot, vedere [Create and Apply the Initial Snapshot](../create-and-apply-the-initial-snapshot.md).  
  
    -   Per creare un nuovo snapshot per una pubblicazione di tipo merge con filtri con parametri, vedere [Creare uno snapshot per una pubblicazione di tipo merge con filtri con parametri](../create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md).  
  
3.  Dopo la creazione dello snapshot, sincronizzare la sottoscrizione per copiare lo schema e i dati per il nuovo articolo.  
  
    -   Per sincronizzazione di una sottoscrizione push, vedere [Synchronize a Push Subscription](../synchronize-a-push-subscription.md).  
  
    -   Per sincronizzazione di una sottoscrizione pull, vedere [Synchronize a Pull Subscription](../synchronize-a-pull-subscription.md).  
  
## <a name="dropping-articles"></a>rimozione di articoli  
 Gli articoli possono essere eliminati da una pubblicazione in qualsiasi momento, ma è necessario tenere in considerazione i comportamenti seguenti:  
  
-   L'eliminazione di un articolo da una pubblicazione non comporta la rimozione dell'oggetto dal database di pubblicazione o dell'oggetto corrispondente dal database di sottoscrizione. Usare DROP \<Object> per rimuovere questi oggetti, se necessario. Quando si elimina un articolo correlato ad altri articoli pubblicati tramite vincoli di chiave esterna, è consigliabile eliminare la tabella nel Sottoscrittore manualmente o tramite l'esecuzione di script su richiesta: specificare uno script che includa le istruzioni DROP appropriate \<Object> . Per altre informazioni, vedere [Eseguire script durante la sincronizzazione &#40;programmazione Transact-SQL della replica&#41;](../execute-scripts-during-synchronization-replication-transact-sql-programming.md).  
  
-   Per pubblicazioni di tipo merge con un livello di compatibilità di 90RTM o superiore, gli articoli possono essere eliminati in qualsiasi momento, ma è necessario un nuovo snapshot. Inoltre:  
  
    -   Se un articolo è un articolo padre in una relazione tra record logici o filtri join, è necessario che prima vengano eliminate le relazioni e di conseguenza sarà necessario eseguire una reinizializzazione.  
  
    -   Se un articolo ha l'ultimo filtro con parametri in una pubblicazione, è necessario reinizializzare le sottoscrizioni.  
  
-   Per pubblicazioni di tipo merge con un livello di compatibilità inferiore a 90RTM, gli articoli possono essere eliminati senza particolari considerazioni prima della sincronizzazione iniziale delle sottoscrizioni. Se un articolo viene eliminato dopo la sincronizzazione di una o più sottoscrizioni, è necessario che le sottoscrizioni vengano eliminate, ricreate e sincronizzate.  
  
-   Per le pubblicazioni snapshot o transazionali, gli articoli possono essere eliminati senza particolari considerazioni prima della creazione delle sottoscrizioni. Se un articolo viene eliminato dopo la creazione di una o più sottoscrizioni, è necessario che le sottoscrizioni vengano eliminate, ricreate e sincronizzate. Per altre informazioni sull'eliminazione delle sottoscrizioni, vedere [Sottoscrivere le pubblicazioni](../subscribe-to-publications.md) e [sp_dropsubscription &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-dropsubscription-transact-sql). **sp_dropsubscription** consente all'utente di eliminare un solo articolo dalla sottoscrizione anziché la sottoscrizione intera.  
  
1.  L'eliminazione di un articolo da una pubblicazione implica l'eliminazione dell'articolo e la creazione di un nuovo snapshot per la pubblicazione. Se si elimina un articolo, lo snapshot corrente non è più valido ed è perciò necessario creare un nuovo snapshot.  
  
    -   Per eliminare un articolo da una pubblicazione, vedere [Aggiungere ed eliminare articoli in una pubblicazione &#40;SQL Server Management Studio&#41;](add-articles-to-and-drop-articles-from-a-publication.md) o [Eliminare un articolo](delete-an-article.md).  
  
2.  Dopo avere eliminato un articolo da una pubblicazione, è necessario creare un nuovo snapshot per la pubblicazione. Nel caso si tratti di una pubblicazione di tipo merge con filtri con parametri, sarà necessario creare tutte le partizioni.  
  
    -   Per creare un nuovo snapshot, vedere [Create and Apply the Initial Snapshot](../create-and-apply-the-initial-snapshot.md).  
  
    -   Per creare un nuovo snapshot per una pubblicazione di tipo merge con filtri con parametri, vedere [Creare uno snapshot per una pubblicazione di tipo merge con filtri con parametri](../create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md).  
  
 Come evidenziato sopra, in alcuni casi l'eliminazione di un articolo richiede che le sottoscrizioni vengano eliminate, ricreate e quindi sincronizzate. Per altre informazioni, vedere [Sottoscrivere le pubblicazioni](../subscribe-to-publications.md) e [Sincronizzare i dati](../synchronize-data.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Pubblicare dati e oggetti di database](publish-data-and-database-objects.md)   
 [Reinizializza sottoscrizioni](../reinitialize-subscriptions.md)   
 [Apportare modifiche allo schema nei database di pubblicazione](make-schema-changes-on-publication-databases.md)  
  
  
