---
title: Memorizzazione dei report nella cache (SSRS) | Microsoft Docs
ms.date: 05/14/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server
ms.topic: conceptual
helpviewer_keywords:
- report execution properties [Reporting Services]
- cache [Reporting Services]
- report processing [Reporting Services], caching
- cached instances [Reporting Services]
- refreshing cache
- cached reports [Reporting Services]
- preloading cache
- invalid cached reports [Reporting Services]
- performance [Reporting Services]
- expiration [Reporting Services]
- snapshots [Reporting Services], caching
ms.assetid: 146542c3-8efd-4b89-a8d8-77d22896630e
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: ba54a5c29245a178fb1b50139d64f1e05bfd92f1
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/31/2020
ms.locfileid: "66175588"
---
# <a name="caching-reports-ssrs"></a>Memorizzazione dei report nella cache (SSRS)
  Nel server di report è possibile memorizzare nella cache una copia di un report già elaborato, che verrà utilizzata quando un utente apre il report. Per l'utente, l'unico elemento disponibile per determinare che il report è una copia memorizzata nella cache è rappresentato dalla data e dall'ora di esecuzione del report. Se la data e l'ora non sono quelle correnti e se il report non è uno snapshot, significa che il report è stato recuperato dalla cache.  
  
 che consente di ridurre il tempo necessario per recuperare i report di grandi dimensioni o che vengono aperti di frequente. Se il server viene riavviato, tutte le istanze memorizzate nella cache vengono ripristinate quando il servizio Web ReportServer viene riportato online.  
  
 La memorizzazione nella cache è una tecnica per il miglioramento delle prestazioni Il contenuto della cache è volatile e può cambiare in seguito all'aggiunta, alla sostituzione e alla rimozione di report. Se si desidera una strategia di memorizzazione nella cache più prevedibile, è consigliabile creare uno snapshot del report. Per altre informazioni, vedere [Impostare proprietà di elaborazione dei report](../../reporting-services/report-server/set-report-processing-properties.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] archivia i file temporanei in un database per supportare le sessioni utente e l'elaborazione dei report. Questi file vengono memorizzati nella cache per uso interno e per il supporto di una visualizzazione uniforme nel corso di un'unica sessione del browser. Per altre informazioni sulle modalità di memorizzazione nella cache di file temporanei a uso interno, vedere [Database del server di report &#40;modalità nativa SSRS&#41;](../../reporting-services/report-server/report-server-database-ssrs-native-mode.md).  
  
## <a name="cached-instances"></a>Istanze memorizzate nella cache  
 Un'istanza di un report memorizzata nella cache si basa sul formato temporaneo di un report. Nella cache del server di report viene in genere memorizzata una sola istanza di un report basata sul nome del report. Se tuttavia un report può contenere dati diversi in base ai parametri delle query, potrebbero risultare memorizzate nella cache più versioni del report contemporaneamente. Si supponga, ad esempio, di disporre di un report con parametri che accetta un indicativo di paese come valore di parametro. Se quattro utenti diversi specificano quattro indicativi di paese diversi, nella cache vengono create quattro copie del report.  
  
 Il primo utente che esegue il report con un indicativo di paese specifico determina la memorizzazione nella cache di un report che contiene i dati per tale paese. Per gli utenti che successivamente richiederanno il report con lo stesso indicativo di paese, verrà utilizzata la copia memorizzata nella cache.  
  
 Non tutti i report possono essere memorizzati nella cache. Se per un report sono inclusi dati in base agli utenti, vengono richieste credenziali agli utenti, oppure viene utilizzata l'autenticazione di Windows, il report non viene memorizzato nella cache.  
  
## <a name="refreshing-the-cache"></a>Aggiornamento della cache  
 Quando un utente seleziona un report dopo la scadenza della copia precedentemente memorizzata nella cache, il report memorizzato nella cache viene sostituito con una versione più recente. I report che sono configurati per l'esecuzione come istanze memorizzate nella cache vengono rimossi dalla cache a intervalli regolari, in base alle impostazioni relative alla scadenza. È possibile impostare la scadenza di un report in minuti o a un'ora pianificata, come determinato dal requisito di attualità dei dati. Non è possibile eliminare direttamente i report dalla cache, a meno che non si utilizzi l'API SOAP.  
  
 Per configurare la scadenza della cache, è possibile utilizzare una pianificazione condivisa o una pianificazione specifica del report. Se si utilizza una pianificazione condivisa che in seguito viene sospesa, la cache non scadrà durante l'intervallo di sospensione. Se una pianificazione condivisa viene eliminata, una copia delle impostazioni della pianificazione verrà salvata come pianificazione specifica del report.  
  
 Se una pianificazione scade o se il motore di pianificazione non è disponibile alla data della scadenza della cache, il server di report esegue un report live fino a quando non sarà possibile riprendere le operazioni pianificate (estendendo la pianificazione o avviando il servizio di pianificazione).  
  
## <a name="preloading-the-cache"></a>Precaricamento della cache  
 Per ottimizzare le prestazioni del server, è possibile eseguire il precaricamento della cache. È possibile precaricare la cache con una raccolta di istanze del report con parametri in due modi:  
  
1.  Creazione di un piano di aggiornamento della cache. Quando si crea un piano di aggiornamento, è possibile specificare una pianificazione per un report singolo o una pianificazione condivisa.  
  
2.  Creazione di una sottoscrizione guidata dai dati che utilizza il Provider recapito Null. Quando viene specificato il Provider recapito Null come metodo di recapito nella sottoscrizione, il server di report indica il database del server di report come destinazione del recapito e utilizza un'estensione per il rendering specializzata, denominata estensione per il rendering Null. A differenza delle altre estensioni per il recapito, l'estensione Provider recapito Null non ha impostazioni per il recapito che possono essere configurate tramite una definizione di sottoscrizione.  
  
 La memorizzazione nella cache del report è particolarmente utile se si desidera memorizzare nella cache più istanze di un report con parametri, dove vengono utilizzati valori di parametro diversi per generare istanze del report diverse. Si noti che nel report è possibile specificare solo parametri basati su query.  
  
 Quando si specifica una pianificazione o si crea una sottoscrizione guidata dai dati, è necessario pianificare la frequenza con cui i report vengono recapitati alla cache. Per recapitare le nuove copie alla cache, è necessario che le vecchie copie siano scadute. Pertanto, le proprietà di esecuzione del report devono essere configurate per includere le impostazioni di scadenza della cache. Le impostazioni di scadenza devono essere coerenti con la pianificazione della sottoscrizione definita dall'utente. Se, ad esempio, si crea una sottoscrizione che deve essere eseguita ogni notte, anche la cache deve scadere ogni notte prima dell'ora di esecuzione della sottoscrizione. Se le Proprietà di esecuzione non prevedono l'ora di scadenza, i recapiti più recenti vengono ignorati. Per altre informazioni sui piani di aggiornamento della cache, vedere [Pianificazioni](../../reporting-services/subscriptions/schedules.md). Per altre informazioni sull'impostazione delle proprietà, vedere [Impostare proprietà di elaborazione dei report](../../reporting-services/report-server/set-report-processing-properties.md). Per altre informazioni sull'uso delle sottoscrizioni guidate dai dati, vedere [Sottoscrizioni guidate dai dati](../../reporting-services/subscriptions/data-driven-subscriptions.md).  
  
## <a name="conditions-that-cause-cache-expiration"></a>Condizioni che determinano la scadenza della cache  
 Un report memorizzato nella cache può venire invalidato a causa della modifica degli elementi seguenti: definizione del report, parametri del report, credenziali dell'origine dei dati oppure opzioni di esecuzione del report. Se si elimina un report memorizzato nella cache, anche la copia del report presente nella cache viene eliminata.  
  
 Se per qualsiasi motivo non è possibile eseguire il rendering del report da un'istanza memorizzata nella cache (ad esempio se i valori dei parametri specificati da un utente sono diversi da quelli utilizzati per creare il report memorizzato nella cache) il report viene eseguito nuovamente dal server di report.  
  
## <a name="see-also"></a>Vedere anche  
 [Impostare le opzioni di elaborazione &#40;Reporting Services in modalità integrata SharePoint&#41;](../../reporting-services/report-server-sharepoint/set-processing-options-reporting-services-in-sharepoint-integrated-mode.md)   
 [Impostare proprietà di elaborazione dei report](../../reporting-services/report-server/set-report-processing-properties.md)   
 [Concetti relativi a Reporting Services &#40;SSRS&#41;](../../reporting-services/reporting-services-concepts-ssrs.md)   
 [Precaricare la cache](../../reporting-services/report-server/preload-the-cache-report-manager.md)   
 [Pianificazioni](../../reporting-services/subscriptions/schedules.md)   
 [Memorizzare nella cache set di dati condivisi &#40;SSRS&#41;](../../reporting-services/report-server/cache-shared-datasets-ssrs.md)   
  
  
