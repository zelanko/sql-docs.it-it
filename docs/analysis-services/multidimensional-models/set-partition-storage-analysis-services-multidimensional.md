---
title: Impostare l'archiviazione delle partizioni (Analysis Services - multidimensionale) | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 3410a8b26b9b9e26046a39f8ed5250ae9b82e67d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "68165155"
---
# <a name="set-partition-storage-analysis-services---multidimensional"></a>Impostare l'archiviazione delle partizioni (Analysis Services - Multidimensionale)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] offre diverse configurazioni di archiviazione standard per le modalità di archiviazione e le opzioni di memorizzazione nella cache. Si tratta delle configurazioni utilizzate di frequente per notifiche di aggiornamento, latenza e ricompilazione dei dati.  
  
 È possibile specificare l'archiviazione delle partizioni nella scheda Partizioni del cubo in [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]o nella pagina delle proprietà delle partizioni in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
## <a name="guidelines-for-choosing-a-storage-mode"></a>Linee guida per la scelta di una modalità di archiviazione  
 Una prassi comune per gruppi di misure di grandi dimensioni consiste nel configurare tipi di archiviazione diversi per le varie partizioni. Tenere presenti le linee guida seguenti:  
  
-   Utilizzare l'impostazione ROLAP in tempo reale per i dati correnti che vengono aggiornati continuamente.  
  
-   Utilizzare la memorizzazione nella cache attiva con latenza bassa o media per le partizioni basate su origini dei dati aggiornate con minore frequenza.  
  
-   Utilizzare l'impostazione MOLAP automatico per le origini dei dati per cui sono richieste prestazioni elevate ed è possibile consentire un certo intervallo di latenza dei dati.  
  
-   Utilizzare l'impostazione MOLAP pianificato per le origini dei dati per cui gli utenti devono accedere continuamente ai dati ma necessitano di vedere le modifiche solo periodicamente.  
  
-   Utilizzare l'archiviazione MOLAP senza memorizzazione nella cache attiva per le partizioni modificate poco frequentemente o non modificate, per le partizioni per cui gli utenti non necessitano l'accesso ai dati più recenti e per i casi in cui non è necessario che i dati siano continuamente disponibili agli utenti durante eventuali aggiornamenti ed elaborazioni non necessari.  
  
 Quelle indicate sono linee guida generali. Per lo sviluppo dello schema di archiviazione migliore per i dati in uso, è necessario eseguire analisi e test accurati. Se nessuna delle configurazioni standard soddisfa le proprie esigenze, è inoltre possibile configurare manualmente le impostazioni per una partizione.  
  
## <a name="storage-settings-descriptions"></a>Descrizione delle impostazioni di archiviazione  
  
|Impostazione di archiviazione standard|Descrizione|  
|------------------------------|-----------------|  
|ROLAP in tempo reale|La tecnologia OLAP è in tempo reale. I dati dettaglio e le aggregazioni vengono archiviati in formato relazionale. Il server è in attesa di notifiche quando i dati vengono modificati e tutte le query riflettono lo stato corrente dei dati (latenza zero).<br /><br /> Questa impostazione viene in genere utilizzata per un'origine dei dati con aggiornamenti molto frequenti e continui quando per gli utenti sono necessari i dati più recenti. In base ai tipi di query generate dalle applicazioni client, questo metodo può comportare i tempi di risposta più lenti.|  
|HOLAP in tempo reale|La tecnologia OLAP è in tempo reale. I dati dettaglio vengono archiviati in un formato relazionale mentre le aggregazioni vengono archiviate in un formato multidimensionale. Il server è in attesa di notifiche quando i dati vengono modificati e aggiorna, quando necessario, le aggregazioni OLAP multidimensionali (MOLAP). Non viene creta alcuna cache MOLAP. Quando l'origine dei dati viene aggiornata, il server passa in modalità ROLAP in tempo reale fino a quando le aggregazioni vengono aggiornate. Tutte le query riflettono lo stato corrente dei dati (latenza zero).<br /><br /> Questa impostazione viene in genere utilizzata per un'origine dei dati con aggiornamenti frequenti e continui, ma non così frequenti da richiedere la modalità ROLAP in tempo reale, quando per gli utenti sono necessari i dati più recenti. Questo metodo offre in genere prestazioni globali migliori rispetto all'archiviazione ROLAP. Se l'origine dati rimane inattiva per un periodo di tempo sufficientemente lungo, questa impostazione può offrire prestazioni simili a quelle della modalità MOLAP.|  
|MOLAP a bassa latenza|I dati dettaglio e le aggregazioni vengono archiviati in formato multidimensionale. Il server è in attesa di notifiche di modifiche ai dati e passa in modalità ROLAP in tempo reale durante la rielaborazione di oggetti MOLAP in una cache. Prima di aggiornare la cache, è necessario un intervallo di inattività di almeno 10 secondi. Se l'intervallo di inattività non viene raggiunto, si verifica un intervallo sostitutivo di 10 minuti. L'elaborazione avviene automaticamente quando i dati vengono modificati, con una latenza di 30 minuti dopo la prima modifica.<br /><br /> Questa impostazione viene in genere utilizzata per un'origine dei dati con aggiornamenti frequenti quando le prestazioni di esecuzione delle query sono più importanti rispetto alla continua disponibilità dei dati più recenti. Questa impostazione consente di elaborare automaticamente gli oggetti MOLAP quando necessario, dopo l'intervallo di latenza. Durante la rielaborazione degli oggetti MOLAP, le prestazioni vengono rallentate.|  
|MOLAP a media latenza|I dati dettaglio e le aggregazioni vengono archiviati in formato multidimensionale. Il server è in attesa di notifiche di modifiche ai dati e passa in modalità ROLAP in tempo reale durante la rielaborazione di oggetti MOLAP nella cache. Prima di aggiornare la cache, è necessario un intervallo di inattività di almeno 10 secondi. Se l'intervallo di inattività non viene raggiunto, si verifica un intervallo sostitutivo di 10 minuti. L'elaborazione avviene automaticamente quando i dati vengono modificati, con una latenza di quattro ore.<br /><br /> Questa impostazione viene in genere utilizzata per un'origine dei dati con aggiornamenti frequenti, o meno frequenti, quando le prestazioni di esecuzione delle query sono più importanti rispetto alla continua disponibilità dei dati più recenti. Questa impostazione consente di elaborare automaticamente gli oggetti MOLAP quando necessario, dopo l'intervallo di latenza. Durante la rielaborazione degli oggetti MOLAP, le prestazioni vengono rallentate.|  
|MOLAP automatico|I dati dettaglio e le aggregazioni vengono archiviati in formato multidimensionale. Il server è in attesa di notifiche ma mantiene la cache MOLAP corrente durante la compilazione di quella nuova. Il server non passa mai in modalità OLAP in tempo reale e, durante la compilazione della nuova cache, le query possono diventare non aggiornate.<br /><br /> Prima di creare la nuova cache MOLAP, è necessario un intervallo di inattività di almeno 10 secondi. Se l'intervallo di inattività non viene raggiunto, si verifica un intervallo sostitutivo di 10 minuti. L'elaborazione avviene automaticamente quando i dati vengono modificati, con una latenza di due ore.<br /><br /> Questa impostazione viene in genere utilizzata per un'origine dei dati in cui le prestazioni di esecuzione delle query sono estremamente importanti. Questa impostazione consente di elaborare automaticamente gli oggetti MOLAP quando necessario, dopo l'intervallo di latenza. Durante la compilazione e l'elaborazione della nuova cache, le query non restituiscono i dati più recenti.|  
|MOLAP pianificato|I dati dettaglio e le aggregazioni vengono archiviati in formato multidimensionale. Il server non riceve notifiche quando i dati vengono modificati. L'elaborazione avviene automaticamente ogni 24 ore.<br /><br /> Questa impostazione viene in genere utilizzata per un'origine dei dati in cui sono necessari solo aggiornamenti giornalieri. Le query vengono eseguite sempre su dati della cache MOLAP, che non viene scartata fino a quando non è stata compilata una nuova cache e i relativi oggetti non sono stati elaborati.|  
|MOLAP|La memorizzazione nella cache attiva non è attivata. I dati dettaglio e le aggregazioni vengono archiviati in formato multidimensionale. Il server non riceve notifiche quando i dati vengono modificati. L'elaborazione deve essere pianificata o eseguita manualmente.<br /><br /> Questa impostazione viene in genere utilizzata per un'origine dei dati in cui non sono necessari aggiornamenti periodici per le applicazioni client ma è fondamentale disporre di prestazioni elevate.<br /><br /> L'archiviazione MOLAP senza memorizzazione nella cache attiva garantisce le migliori prestazioni possibili nei casi in cui per le applicazioni non sono necessari i dati più aggiornati. Questa modalità richiede un tempo di inattività per l'elaborazione degli oggetti aggiornati, che può tuttavia essere ridotto al minimo aggiornando ed elaborando i cubi in un server dell'area di gestione temporanea e utilizzando la funzionalità di sincronizzazione del database per copiare gli oggetti MOLAP aggiornati ed elaborati nel server di produzione.|  
  
## <a name="custom-storage-options"></a>Opzioni di archiviazione personalizzate  
 Anziché utilizzare una delle impostazioni di archiviazione standard, è possibile configurare manualmente l'archiviazione e la memorizzazione nella cache attiva. Prima di creare impostazioni di archiviazione personalizzate, è necessario innanzitutto fare clic sull'opzione **Impostazione standard** e spostare il dispositivo di scorrimento sull'impostazione standard che corrisponde maggiormente alla configurazione desiderata. Quindi, per creare una configurazione personalizzata fare clic sull'opzione **Impostazione personalizzata** e quindi su **Opzioni**.  
  
-   È possibile specificare se le modifiche apportate a un'origine dei dati devono attivare aggiornamenti della cache. Per consentire un livello di trasferimento tollerabile, è possibile specificare un intervallo di inattività minimo dopo gli aggiornamenti all'origine dei dati, nonché un intervallo di attività sostitutivo per l'aggiornamento della cache dopo un periodo specificato nel caso in cui l'intervallo tra le modifiche all'origine dei dati non raggiunga mai il valore minimo.  
  
-   È possibile specificare se eliminare la cache obsoleta dopo gli aggiornamenti. Se si seleziona tale opzione, quando viene superata la latenza specificata, il server passa in modalità OLAP relazionale (ROLAP) in tempo reale mentre aggiorna la cache. Se non si seleziona questa opzione, il server continua la query sulla cache OLAP multidimensionale (MOLAP) non aggiornata mentre compila la nuova cache.  
  
     È possibile specificare l'intervallo di latenza che deve intercorrere tra le modifiche e l'eliminazione di una cache obsoleta. Durante tale intervallo, gli utenti possono continuare a visualizzare i dati di una cache obsoleta prima che venga eliminata. Se vengono apportate modifiche e la cache è ancora in fase di aggiornamento o di elaborazione al termine di tale intervallo, le query verranno reindirizzate all'elaborazione ROLAP.  
  
-   Se si desidera aggiornare periodicamente gli oggetti MOLAP memorizzati nella cache indipendentemente dalle modifiche apportate all'origine dei dati, è possibile pianificare aggiornamenti forzati della cache. I vantaggi dell'elaborazione OLAP in tempo reale variano a seconda delle dimensioni del database e del periodo di latenza assegnato in base alla frequenza di modifiche dell'origine dei dati. Gli utenti devono inviare le query a una cache il più spesso possibile, non all'elaborazione ROLAP.  
  
 Se si seleziona la casella di controllo **Applica impostazioni alle dimensioni** , le stesse impostazioni di archiviazione verranno applicate alle dimensioni correlate al gruppo di misure. I valori delle dimensioni sono inizialmente identici ai valori delle partizioni.  
  
## <a name="see-also"></a>Vedere anche  
 [Partizioni nei modelli multidimensionali](../../analysis-services/multidimensional-models/partitions-in-multidimensional-models.md)  
  
  
