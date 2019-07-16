---
title: Configurare l'utilizzo di spazio su disco (Power Pivot per SharePoint) | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ppvt-sharepoint
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 6fa6090a675326db06491d54b82a6844363ee3e9
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "68208315"
---
# <a name="configure-disk-space-usage-power-pivot-for-sharepoint"></a>Configurare l'uso di spazio su disco (PowerPivot per SharePoint)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Una distribuzione di [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] per SharePoint consente di usare lo spazio su disco del computer host per memorizzare nella cache i database [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] per ricaricarli in modo più veloce. Ogni database [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] caricato in memoria viene prima memorizzato nella cache su disco in modo che possa essere ricaricato rapidamente in un secondo momento per soddisfare nuove richieste. Per impostazione predefinita, [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] per SharePoint usa tutto lo spazio su disco disponibile per memorizzare i database nella cache, ma è possibile modificare questo comportamento impostando le proprietà che limitano la quantità di spazio su disco usata.  
  
 In questo argomento viene illustrato come impostare i limiti all'utilizzo dello spazio su disco.  
  
 Questo argomento non offre istruzioni sulla gestione dello spazio su disco di database [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] , incorporati in cartelle di lavoro di Excel, archiviati all'interno di database di contenuto. [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] possono essere di grandi dimensioni, creando quindi nuovi problemi alla capacità di memoria della farm. Inoltre, se il controllo delle versioni è abilitato, si potrebbe disporre facilmente di più copie di dati nello stesso database di contenuto, aumentando ulteriormente la quantità di spazio su disco richiesta per l'archiviazione del contenuto. Anche se i database [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] sono importanti dal punto di vista della gestione dei dischi, non possono essere gestiti indipendentemente da altro contenuto archiviato in una farm di SharePoint. È necessario monitorare continuamente lo spazio su disco man mano che l'azienda incrementa l'uso di cartelle di lavoro di [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . È anche possibile tenere traccia dell'attività delle cartelle di lavoro di [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] nel dashboard di gestione di [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] , nonché rimuovere le cartelle di lavoro non più usate.  
  
## <a name="how-power-pivot-for-sharepoint-manages-cached-databases"></a>Modalità di gestione dei database memorizzati nella cache in PowerPivot per SharePoint  
 Per gestire la cache, il servizio di sistema di [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] esegue un processo in background a intervalli regolari per eliminare i database obsoleti o non usati per i quali esistono versioni più recenti in una raccolta contenuto. Lo scopo del processo di pulizia è quello di scaricare i database inattivi dalla memoria ed eliminare i database inutilizzati memorizzati nella cache dal file system. Il processo di pulizia viene utilizzato per la manutenzione a lungo termine, assicurando che i database non rimangano nel sistema per un periodo illimitato. In un server attivo, i database potrebbero essere rimossi più spesso per la richiesta di memoria nel server, l'eliminazione del database in SharePoint o per versioni più recenti del database in una raccolta contenuto.  
  
 Anche se non è possibile pianificare il processo di pulizia, è possibile personalizzare le gestione dei file di cache impostando proprietà di configurazione del server che consentono di effettuare le operazioni seguenti:  
  
-   Impostare limiti sulla quantità di spazio su disco utilizzata dalla cache.  
  
-   Specificare la quantità di dati da eliminare quando viene raggiunto lo spazio massimo su disco.  
  
## <a name="how-to-check-disk-space-usage"></a>Modalità di controllo dell'utilizzo dello spazio su disco  
 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] per SharePoint viene installato in server applicazioni in una farm di SharePoint. Ogni installazione dispone di una directory dati che include una cartella di backup. La cartella di backup contiene tutti i file di dati memorizzati nella cache dall'istanza di Analysis Services nel computer. Per impostazione predefinita, questa cartella può essere trovata nel percorso seguente:  
  
 `%drive%:\Program Files\Microsoft SQL Server\MSAS10_50.PowerPivot\OLAP\Backup\Sandboxes\<serviceApplicationName>`  
  
 Per controllare la quantità totale di spazio su disco utilizzata dalla cache, è necessario controllare le dimensioni della cartella Backup. Non è disponibile alcuna proprietà in Amministrazione centrale che consenta di segnalare le dimensioni della cache corrente.  
  
 La cartella Backup consente l'archiviazione in una cache comune per qualsiasi database di [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] caricato in memoria nel computer locale. Se nella farm sono definite più applicazioni del servizio [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] , una può usare il server locale per caricare e successivamente memorizzare nella cache dati [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . Sia il caricamento sia la memorizzazione nella cache dei dati sono operazioni del server Analysis Services. Pertanto, l'utilizzo dello spazio su disco totale è gestito a livello dell'istanza di Analysis Services nella cartella Backup. Le impostazioni di configurazione che limitano l'utilizzo dello spazio su disco vengono pertanto impostate sulla singola istanza di SQL Server Analysis Services in esecuzione in un server applicazioni di SharePoint.  
  
 La cache contiene solo database [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] - I database vengono archiviati in più file all'interno di un'unica cartella padre, la cartella Backup. Poiché i database [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] devono essere usati come dati interni a una cartella di lavoro di Excel, i nomi dei database sono basati su GUID anziché su descrizioni. Una cartella GUID in  **\<Nomeapplicazioneservizio >** è la cartella padre di un [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] database. Quando i database [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] vengono caricati nel server, vengono create cartelle aggiuntive per ognuno.  
  
 Poiché i dati [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] possono essere caricati in qualsiasi istanza di Analysis Services in una farm, gli stessi dati possono anche essere memorizzati nella cache in più computer della farm. Questa procedura favorisce le prestazioni rispetto all'utilizzo dello spazio su disco, ma in questo modo gli utenti ottengono accesso più veloce ai dati se già disponibili su disco.  
  
 Per ridurre immediatamente l'uso di spazio su disco, è possibile arrestare il servizio e quindi eliminare un database [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] dalla cartella Backup. L'eliminazione manuale di file è una misura temporanea, poiché una copia più recente del database verrà memorizzata di nuovo nella cache alla successiva esecuzione di query sui dati [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . Tra le soluzioni permanenti è inclusa la limitazione di spazio su disco utilizzato dalla cache.  
  
 A livello di sistema, è possibile creare avvisi di posta elettronica tramite cui si notifica all'utente quando lo spazio su disco non è sufficiente. In Microsoft System Center è disponibile una funzionalità di avvisi di posta elettronica. Per impostare gli avvisi, è possibile utilizzare anche Gestione risorse file server, l'Utilità di pianificazione o uno script di PowerShell. Nei collegamenti seguenti vengono fornite informazioni utili per la configurazione di notifiche di spazio su disco insufficiente:  
  
-   [Quali sono le novità in Gestione risorse File Server](http://technet.microsoft.com/library/hh831746.aspx) (http://technet.microsoft.com/library/hh831746.aspx).  
  
-   [Guida dettagliata alla gestione risorse file Server per Windows Server 2008 R2](http://go.microsoft.com/fwlink/?LinkID=204875) (http://go.microsoft.com/fwlink/?LinkID=204875).  
  
-   [L'impostazione di avvisi di spazio su disco insufficiente in Windows Server 2008](http://go.microsoft.com/fwlink/?LinkID=204870) ( http://go.microsoft.com/fwlink/?LinkID=204870).  
  
## <a name="how-to-limit-the-amount-of-disk-space-used-for-storing-cached-files"></a>Come limitare la quantità di spazio su disco utilizzata per l'archiviazione di file memorizzati nella cache  
  
1.  In Gestione applicazioni di Amministrazione centrale fare clic su **Gestisci servizi nel server**.  
  
2.  Scegliere **SQL Server Analysis Services**.  
  
     Si noti che i limiti vengono impostati sull'istanza di Analysis Services eseguita nel server fisico e non a livello di applicazione di servizio. Tutte le applicazioni di servizio in cui viene utilizzata l'istanza di Analysis Services locale sono soggette al singolo limite massimo dello spazio su disco impostato per tale istanza.  
  
3.  In Utilizzo disco impostare un valore (in gigabyte) per **Totale spazio su disco utilizzato** per impostare un limite massimo per la quantità di spazio usato per la memorizzazione nella cache. Il valore predefinito è 0, che consente ad Analysis Services di utilizzare tutto lo spazio su disco disponibile.  
  
4.  In utilizzo disco nel **Elimina dalla cache database nelle ultime ' n'ore** impostazione, specificare ultimi criteri utilizzati per svuotare la cache quando lo spazio su disco è al limite massimo.  
  
     Il valore predefinito è 4 ore, pertanto tutti i database inattivi per almeno 4 ore vengono eliminati dal file system. I database che sono inattivi ma ancora in memoria vengono scaricati e quindi eliminati dal file system.  
  
## <a name="how-to-limit-how-long-a-database-is-kept-in-the-cache"></a>Come limitare la durata di un database nella cache  
  
1.  In Gestione applicazioni di Amministrazione centrale fare clic su **Gestisci applicazioni di servizio**.  
  
2.  Fare clic su **Applicazione del servizio [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] predefinita** per aprire il dashboard di gestione.  
  
3.  In Azioni fare clic su **Configura impostazioni dell'applicazione di servizio**.  
  
4.  Nella sezione Cache su disco è possibile specificare la durata in memoria di un database inattivo per soddisfare nuove richieste (per impostazione predefinita, 48 ore) e la relativa durata nella cache (per impostazione predefinita, 120 ore).  
  
     L'opzione**Mantieni in memoria database inattivo** consente di specificare la durata in memoria di un database inattivo per soddisfare nuove richieste per tali dati. Un database attivo viene mantenuto sempre in memoria purché vengano eseguite query su di esso. Una volta inattivo, tuttavia, viene mantenuto in memoria per un ulteriore periodo di tempo, in caso vi siano ulteriori richieste per tali dati.  
  
     Poiché i database [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] vengono memorizzati prima nella cache e successivamente caricati in memoria, i file dei database usano spazio su disco immediatamente. Tuttavia, mentre il database è attivo (e per le 48 ore successive), tutte le richieste vengono indirizzate prima al database in memoria, ignorando il database memorizzato nella cache. Dopo 48 ore di inattività, il file viene scaricato dalla memoria, ma rimane nella cache, da dove può essere rapidamente ricaricato se viene intercettata una nuova richiesta di connessione per tali dati dall'istanza del server [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] locale. Le richieste di connessione a un database inattivo vengono soddisfatte dalla cache piuttosto che dalla raccolta contenuto, riducendo l'impatto sui database di contenuto.  
  
     È importante notare che la raccolta contenuto è l'unica posizione permanente per i database [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . Le copie memorizzate nella cache vengono utilizzate solo se il database nella raccolta è lo stesso della copia su disco.  
  
     L'opzione**Mantieni nella cache database inattivo** consente di specificare il tempo di permanenza di un database nel file system dopo che è stato scaricato dalla memoria. Questa impostazione viene utilizzata dal processo di pulizia per determinare i file da eliminare. Tutti i database [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] che sono inattivi per 168 ore (48 ore in memoria e 120 nella cache) vengono eliminati dal disco dal processo di pulizia.  
  
5.  Scegliere **OK** per salvare le modifiche.  
  
## <a name="next-steps"></a>Passaggi successivi  
 Un'installazione di [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] per SharePoint specifica regole di analisi dell'integrità in modo che sia possibile eseguire azioni correttive in caso di problemi di integrità, configurazione o disponibilità del server. Alcune di queste regole consentono di utilizzare le impostazioni di configurazione per stabilire le condizioni in base alle quali vengono attivate le regole di integrità. Se si ottimizzano le prestazioni del server, è necessario rivedere queste impostazioni anche per assicurarsi che le impostazioni predefinite rappresentino la scelta migliore per il sistema. Per altre informazioni, vedere [Configurare le regole di integrità di Power Pivot](../../analysis-services/power-pivot-sharepoint/configure-power-pivot-health-rules.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Amministrazione e configurazione del server PowerPivot in Amministrazione centrale](../../analysis-services/power-pivot-sharepoint/power-pivot-server-administration-and-configuration-in-central-administration.md)  
  
  
