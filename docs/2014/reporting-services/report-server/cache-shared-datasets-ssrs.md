---
title: Memorizzare nella cache set di dati condivisi (SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 4acb1bbe-1c04-4979-b893-dc1b1c5039b6
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 8fcb3e8c423e629a33a0c173e3264ee11ee178f1
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66104177"
---
# <a name="cache-shared-datasets-ssrs"></a>Memorizzare nella cache set di dati condivisi (SSRS)
  I risultati della query per un set di dati condiviso possono essere copiati in una cache per fornire dati coerenti per più report e migliorare il tempo di risposta per la query del set di dati. In modo analogo ai report, è possibile configurare un set di dati condiviso da memorizzare nella cache al momento del primo utilizzo o specificando una pianificazione.  
  
 Un set di dati condiviso può essere incluso in più report o come parte di definizioni del componente. Memorizzando nella cache il set di dati condiviso, viene fornito un set di dati coerente per tutti i report che lo utilizzano e viene inoltre ridotto il numero di esecuzioni della query del set di dati sull'origine dati esterna.  
  
 Nell'elenco seguente vengono indicate le situazioni in cui è opportuno memorizzare nella cache un set di dati condiviso:  
  
-   L'esecuzione della query richiede una notevole quantità di tempo.  
  
-   La query accetta parametri, ma il numero di combinazioni di parametri è ridotto durante la maggior parte del tempo. Ogni combinazione crea risultati della query memorizzati nella cache.  
  
-   La query viene eseguita in ore stimabili del giorno, della settimana o del mese.  
  
-   La query viene eseguita come risultato di un riferimento a un set di dati condiviso in un report recapitato tramite posta elettronica. In questo caso è probabile che un elevato numero di utenti selezioni il collegamento in un breve intervallo di tempo.  
  
-   Nell'elenco seguente vengono indicate le situazioni in cui non è opportuno memorizzare nella cache un set di dati condiviso:  
  
-   I risultati della query devono includere sempre i dati più recenti.  
  
-   La query viene eseguita rapidamente.  
  
-   La query viene eseguita raramente.  
  
-   La query accetta parametri, il numero di combinazioni di parametri è elevato e nessuna combinazione è più probabile di un'altra.  
  
-   All'origine dati su cui si basa il set di dati condiviso sono associate credenziali richieste o della sicurezza integrata di Windows.  
  
-   Il filtro o la query del set di dati condiviso contiene un'espressione con un riferimento alla raccolta globale dell'utente.  
  
 Se un utente sceglie valori dei parametri del report diversi dai valori predefiniti specificati per il set di risultati memorizzati nella cache, la query del set di dati viene eseguita in modo attivo e i risultati memorizzati nella cache non vengono utilizzati per tale query.  
  
## <a name="caching-shared-datasets"></a>Memorizzazione nella cache di set di dati condivisi  
 Per abilitare la memorizzazione nella cache per un set di dati condiviso, è necessario selezionare l'opzione relativa nel set stesso. Dopo che la memorizzazione nella cache è stata abilitata, i risultati della query per un set di dati condiviso vengono copiati nella cache al momento del primo utilizzo. Se al set di dati condiviso sono associati parametri, ogni combinazione di parametri crea una nuova voce nella cache.  
  
 Durante la permanenza nella cache dei risultati della query per una combinazione di parametri specifica, ogni report avviato per l'elaborazione che include un riferimento al set di dati condiviso con tali valori dei parametri utilizzerà i dati memorizzati nella cache.  
  
 È possibile specificare la quantità di tempo in cui mantenere i dati nella cache prima che scadano. Per altre informazioni, vedere [Pagina Memorizzazione nella cache, set di dati condivisi &40 #;Gestione report&#41;](../caching-page-shared-datasets-report-manager.md).  
  
## <a name="preloading-the-cache"></a>Precaricamento della cache  
 È possibile precaricare la cache creando un piano di aggiornamento che consente di specificare la frequenza di aggiornamento della cache tramite una pianificazione condivisa o specifica per l'elemento. Per evitare che per uno stesso elemento siano presenti più voci nella cache, è necessario specificare una pianificazione in base alla quale il tempo per l'elaborazione della query sull'origine dati esterna sia sufficiente. Se ad esempio il tempo necessario per l'esecuzione della query è di 20 minuti, l'aggiornamento deve essere pianificato con frequenza maggiore di 20 minuti. Per altre informazioni, vedere [Schedules](../subscriptions/schedules.md).  
  
 Per creare un piano di aggiornamento della cache per un set di dati condiviso, è necessario che siano rispettate le condizioni seguenti.  
  
-   Il set di dati condiviso deve essere abilitato per la memorizzazione nella cache.  
  
-   L'origine dati condivisa da cui dipende il set di dati condiviso non può utilizzare credenziali richieste o della sicurezza integrata di Windows.  
  
-   Se al set di dati condiviso sono associati parametri, è necessario specificare valori predefiniti statici per ogni parametro non contrassegnato come valore di sola lettura. I parametri di sola lettura utilizzeranno sempre il valore predefinito. Per memorizzare nella cache un set di dati condiviso per più combinazioni di parametri, è necessario creare un piano di aggiornamento della cache separato per ogni combinazione di valori. I parametri non possono contenere riferimenti ad altri set di dati.  
  
-   Ogni piano di aggiornamento della cache è associato a un unico set di dati condiviso o report.  
  
-   È necessario disporre delle autorizzazioni ReadPolicy e UpdatePolicy sul set di dati condiviso.  
  
 I piani di aggiornamento della cache si applicano sia ai set di dati condivisi che ai report. Per altre informazioni, vedere [Opzioni di aggiornamento cache &#40;Gestione report&#41;](../cache-refresh-options-report-manager.md).  
  
## <a name="conditions-that-cause-cache-expiration"></a>Condizioni che determinano la scadenza della cache  
 Le condizioni seguenti possono provocare l'invalidità di una cache di un set di dati condiviso.  
  
-   Scadenza di una condizione della pianificazione per timeout o scadenza della cache.  
  
-   Eliminazione di una pianificazione condivisa.  
  
-   Applicazione di modifiche a una pianificazione condivisa. L'eventuale sospensione di pianificazioni condivise può influire sulla scadenza di una cache.  
  
-   Esecuzione di modifiche alla definizione della query per il set di dati condiviso.  
  
-   Modifica delle credenziali per l'origine dati condivisa da cui dipende il set di dati condiviso.  
  
-   Modifica delle opzioni della cache per il set di dati condiviso.  
  
-   Modifica dei valori predefiniti per i parametri di sola lettura per il set di dati condiviso.  
  
-   Modifica dei filtri che appartengono alla definizione del set di dati condiviso.  
  
-   Eliminazione del set di dati condiviso dal server di report. L'eliminazione di un set di dati condiviso comporta l'eliminazione delle copie memorizzate nella cache associate e dei piani di aggiornamento della cache stessa.  
  
 Gli aggiornamenti dei piani di aggiornamento della cache per i set di dati condivisi non influiscono sui report già in elaborazione, ma influiscono solo su avvii futuri di report che fanno riferimento al set di dati condiviso.  
  
## <a name="see-also"></a>Vedere anche  
 [Gestire set di dati condivisi](../report-data/manage-shared-datasets.md)  
  
  
