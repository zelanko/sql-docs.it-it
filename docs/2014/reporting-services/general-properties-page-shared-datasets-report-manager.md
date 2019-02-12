---
title: Pagina delle proprietà generale, condivisi (gestione Report) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 10798e41-24c3-4e69-893b-7ee6af7fc958
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 72bd3d617fa14e785b29b9c89e3d53d7d5dd3da4
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/11/2019
ms.locfileid: "56032752"
---
# <a name="general-properties-page-shared-datasets-report-manager"></a>Pagina delle proprietà Generale, Set di dati condivisi (Gestione report)
  La pagina Set di dati condiviso consente di visualizzare e gestire le proprietà di un elemento del set di dati condiviso.  
  
 La definizione del set di dati condiviso, inclusa la query, non può essere visualizzata o modificata in Gestione report. Per modificare la definizione, è necessario utilizzare uno strumento di creazione per aprire e modificare la definizione e quindi salvarla nel server di report.  
  
 Un set di dati condiviso consente di gestire le impostazioni per un set di dati separatamente dai report, i componenti e gli altri elementi del catalogo che l'utilizzano.  
  
## <a name="navigation"></a>Navigazione  
 Utilizzare la procedura riportata di seguito per navigare fino a questo percorso nell'interfaccia utente.  
  
###### <a name="to-open-the-shared-dataset-properties-page-for-a-shared-dataset"></a>Per aprire la pagina delle proprietà Set di dati condiviso per un set di dati condiviso  
  
1.  Aprire Gestione report, quindi individuare il set di dati condiviso per il quale si desidera configurare le proprietà.  
  
2.  Passare con il puntatore del mouse sul set di dati condiviso, quindi fare clic sulla freccia a discesa.  
  
3.  Nell'elenco a discesa fare clic su **Gestisci**. Verrà visualizzata la pagina delle proprietà Generale.  
  
## <a name="options"></a>Opzioni  
 **Name**  
 Digitare un nome per il set di dati condiviso utilizzato per identificare l'elemento nella gerarchia di cartelle del server di report.  
  
 **Descrizione**  
 Consente di immettere informazioni sul set di dati condiviso. Questa descrizione viene visualizzata nella pagina Contenuto.  
  
 **Nascondi in visualizzazione elenco**  
 Fa in modo che il set di dati condiviso non venga visualizzato dagli utenti che utilizzano la modalità di visualizzazione Elenco in Gestione report. La modalità di visualizzazione Elenco è il formato di visualizzazione predefinito utilizzato per l'esplorazione della gerarchia di cartelle del server di report. Nella visualizzazione Elenco i nomi e le descrizioni degli elementi vengono disposti dall'alto in basso nella pagina. Il formato alternativo è costituito dalla visualizzazione Dettagli, in cui non sono incluse le descrizioni ma sono disponibili altre informazioni sugli elementi. Gli elementi possono essere nascosti nella visualizzazione Elenco ma non nella visualizzazione Dettagli. Se si desidera limitare l'accesso a un elemento, è necessario creare un'assegnazione di ruolo.  
  
 **Timeout esecuzione query**  
 Consente di digitare il numero di secondi di attesa prima del timeout della query. Se viene impostato 0, non si verificherà mai il timeout della query.  
  
 **Applica**  
 Salvare le modifiche.  
  
 **Elimina**  
 Consente di rimuovere il set di dati condiviso dal database del server di report. L'eliminazione di un set di dati condiviso disattiva qualsiasi report o versione memorizzata nella cache. Per riattivare un report, è necessario aprirlo in uno strumento per la creazione di report e specificare un set di dati con lo stesso nome e la stessa raccolta di campi. In alternativa, è possibile aggiornare ogni riferimento all'area dati per utilizzare un set di dati diverso con la stessa raccolta di campi.  
  
 **Sposta**  
 Consente di spostare un set di dati condiviso nella gerarchia di cartelle del server di report. Verrà visualizzata la pagina di spostamento degli elementi nella quale è possibile esplorare le cartelle per selezionare un nuovo percorso. Per altre informazioni, vedere [pagina spostamento elementi &#40;gestione Report&#41;](../../2014/reporting-services/move-items-page-report-manager.md).  
  
 **Scarica**  
 Consente di estrarre una copia della definizione del set di dati condiviso. A seconda delle associazioni di file definite nel computer, il file verrà aperto in Visual Studio o in un'altra applicazione. Nella maggior parte dei casi, il set di dati condiviso viene aperto come file XML.  
  
 **Sostituisci**  
 Consente di sostituire la definizione del set di dati condiviso con una definizione diversa contenuta in un file con estensione rsd presente nel file system.  
  
## <a name="see-also"></a>Vedere anche  
 [Gestione report &#40;modalità nativa SSRS&#41;](../../2014/reporting-services/report-manager-ssrs-native-mode.md)   
 [Pagina Contenuto &#40;Gestione report&#41;](../../2014/reporting-services/contents-page-report-manager.md)   
 [Guida F1 di gestione report](../../2014/reporting-services/report-manager-f1-help.md)   
 [Opzioni di aggiornamento cache &#40;gestione Report&#41;](../../2014/reporting-services/cache-refresh-options-report-manager.md)   
 [Pagina memorizzazione nella cache, set di dati condivisi &#40;gestione Report&#41;](../../2014/reporting-services/caching-page-shared-datasets-report-manager.md)   
 [Gestire set di dati condivisi](report-data/manage-shared-datasets.md)   
 [Memorizzare nella cache set di dati condivisi &#40;SSRS&#41;](report-server/cache-shared-datasets-ssrs.md)  
  
  
