---
title: Pagina delle proprietà generale, set di impostazioni condivise (Gestione report) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 10798e41-24c3-4e69-893b-7ee6af7fc958
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: bf433f27a5d8dc7f5e0efcf6f5774ed292d1e1a1
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66109070"
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
 **Nome**  
 Digitare un nome per il set di dati condiviso utilizzato per identificare l'elemento nella gerarchia di cartelle del server di report.  
  
 **Descrizione**  
 Consente di immettere informazioni sul set di dati condiviso. Questa descrizione viene visualizzata nella pagina Contenuto.  
  
 **Nascondi in visualizzazione Elenco**  
 Fa in modo che il set di dati condiviso non venga visualizzato dagli utenti che utilizzano la modalità di visualizzazione Elenco in Gestione report. La modalità di visualizzazione Elenco è il formato di visualizzazione predefinito utilizzato per l'esplorazione della gerarchia di cartelle del server di report. Nella visualizzazione Elenco i nomi e le descrizioni degli elementi vengono disposti dall'alto in basso nella pagina. Il formato alternativo è costituito dalla visualizzazione Dettagli, in cui non sono incluse le descrizioni ma sono disponibili altre informazioni sugli elementi. Gli elementi possono essere nascosti nella visualizzazione Elenco ma non nella visualizzazione Dettagli. Se si desidera limitare l'accesso a un elemento, è necessario creare un'assegnazione di ruolo.  
  
 **Timeout esecuzione query**  
 Digitare il numero di secondi prima del timeout della query. Se è 0, la query non prevede il timeout.  
  
 **Applica**  
 Salvare le modifiche.  
  
 **Elimina**  
 Consente di rimuovere il set di dati condiviso dal database del server di report. L'eliminazione di un set di dati condiviso disattiva qualsiasi report o versione memorizzata nella cache. Per riattivare un report, è necessario aprirlo in uno strumento per la creazione di report e specificare un set di dati con lo stesso nome e la stessa raccolta di campi. In alternativa, è possibile aggiornare ogni riferimento all'area dati per utilizzare un set di dati diverso con la stessa raccolta di campi.  
  
 **Spostamento**  
 Consente di spostare un set di dati condiviso nella gerarchia di cartelle del server di report. Verrà visualizzata la pagina di spostamento degli elementi nella quale è possibile esplorare le cartelle per selezionare un nuovo percorso. Per ulteriori informazioni, vedere la [pagina di spostamento degli elementi &#40;Gestione report&#41;](../../2014/reporting-services/move-items-page-report-manager.md).  
  
 **Scaricare**  
 Consente di estrarre una copia della definizione del set di dati condiviso. A seconda delle associazioni di file definite nel computer, il file verrà aperto in Visual Studio o in un'altra applicazione. Nella maggior parte dei casi, il set di dati condiviso viene aperto come file XML.  
  
 **Sostituire**  
 Consente di sostituire la definizione del set di dati condiviso con una definizione diversa contenuta in un file con estensione rsd presente nel file system.  
  
## <a name="see-also"></a>Vedere anche  
 [Gestione report &#40;modalità nativa SSRS&#41;](../../2014/reporting-services/report-manager-ssrs-native-mode.md)   
 [Pagina contenuti &#40;Gestione report&#41;](../../2014/reporting-services/contents-page-report-manager.md)   
 [Guida sensibile al contesto Gestione report](../../2014/reporting-services/report-manager-f1-help.md)   
 [Opzioni di aggiornamento della cache &#40;Gestione report&#41;](../../2014/reporting-services/cache-refresh-options-report-manager.md)   
 [Pagina memorizzazione nella cache, set di impostazioni &#40;Gestione report&#41;](../../2014/reporting-services/caching-page-shared-datasets-report-manager.md)   
 [Gestire set di dati condivisi](report-data/manage-shared-datasets.md)   
 [Memorizzare nella cache set di dati condivisi &#40;SSRS&#41;](report-server/cache-shared-datasets-ssrs.md)  
  
  
