---
title: Risolvere i problemi di progettazione dei report con Reporting Services | Microsoft Docs
ms.date: 02/27/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: troubleshooting
ms.topic: conceptual
ms.assetid: a0d103da-5a3e-475c-a71a-9e23476095e2
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: b3eb298bc6b359b0df92566f9add8d7011cdc907
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/29/2020
ms.locfileid: "65573847"
---
# <a name="troubleshoot-report-design-issues-with-reporting-services"></a>Risolvere i problemi di progettazione dei report con Reporting Services
I problemi di progettazione del report si possono verificare quando si crea il layout del report nella visualizzazione Progettazione in un'applicazione per la progettazione di report. Utilizzare le informazioni presenti in questo argomento per risolvere questi problemi.   
  
## <a name="why-does-my-text-box-show-only-a-single-value-and-not-repeat-for-every-row"></a>Nella casella di testo è visualizzato un solo valore, il quale non viene ripetuto per ogni riga  
Una casella di testo con un riferimento di campo del set di dati viene visualizzata solo una volta e contiene il primo valore nel set di dati.   
  
**Il padre della casella di testo è il corpo del report**  
  
  
Una casella di testo aggiunta direttamente all'area di progettazione può visualizzare solo un valore di aggregazione per un set di dati.  
  
Per verificare il contenitore padre di una casella di testo, selezionare la casella di testo e scorrere fino a **Padre**nel riquadro Proprietà.   
  
Se nelle caselle di testo devono essere visualizzati tutti i valori in un set di dati, utilizzare un'area dati, ad esempio una tabella o una matrice. Per impostazione predefinita, in ogni cella di una tabella o matrice è contenuta una casella di testo. Trascinare i campi del set di dati in ogni cella.   
  
## <a name="why-cant-i-add-total-pages-to-my-report"></a>Impossibile aggiungere il numero complessivo di pagine al report  
I campi predefiniti `[&PageNumber]` e `[&TotalPages]` non sono validi nel corpo del report.   
  
PageNumber e TotalPages sono validi solo nell'intestazione e nel piè di pagina.  
  
  
I campi predefiniti [&PageNumber] e [&TotalPages] sono validi solo nell'intestazione e nel piè di pagina.   
  
Per aggiungere [&PageNumber] o [&TotalPages] a un report, è necessario prima aggiungere un'intestazione o un piè di pagina. Per altre informazioni, vedere [Aggiungere o rimuovere un'intestazione di pagina](../../reporting-services/report-design/add-or-remove-a-page-header-or-footer-report-builder-and-ssrs.md).  
  
> [!NOTE]  
> Se si include [&TotalPages] nell'intestazione o nel piè di pagina si possono verificare problemi durante l'elaborazione del report. Per altre informazioni, vedere Risoluzione dei problemi dei report: report esportati in un formato di file specifico.  
[Risolvere i problemi di elaborazione dei report di Reporting Services](../../reporting-services/troubleshooting/troubleshoot-processing-of-reporting-services-reports.md).  
  
## <a name="how-do-i-design-two-tables-or-a-chart-and-a-table-to-display-side-by-side"></a>Progettazione di due tabelle o un grafico e una tabella da visualizzare affiancati  
La progettazione di un report non prevede la visualizzazione WYSISYG ("What You See Is What You Get"). Il componente Elaborazione report combina dati, elementi del report, informazioni sul layout del report, ad esempio spazio vuoto, contenitori ed espressioni, per produrre un report compilato che viene poi passato a un renderer del report che definisce il layout del report per la visualizzazione specificata: interattiva per un browser HTML o come formato di file. Gli algoritmi di layout automatici possono produrre un layout del report che si desidera modificare.   
  
### <a name="rendering-rules-use-page-size-containers-peer-objects-relative-placement-and-white-space-to-determine-layout"></a>Per determinare il layout le regole del rendering utilizzano le dimensioni della pagina, contenitori, oggetti peer, posizione relativa e spazio vuoto  
In generale, la larghezza di un report aumenta per ricevere i dati mentre altri elementi del report non vengono presi in considerazione.   
  
Per raggruppare più aree dati o elementi di report, posizionarli nello stesso contenitore padre. Ad esempio, posizionare un grafico e una tabella in un contenitore rettangolare e allineare i margini superiori per visualizzarli affiancati. Per altre informazioni, vedere [Tipi di rendering (Generatore report e SSRS)](../../reporting-services/report-design/rendering-behaviors-report-builder-and-ssrs.md).  
  
## <a name="see-also"></a>Vedere anche  
[Risolvere i problemi di recupero dei dati con i report di Reporting Services](../../reporting-services/troubleshooting/troubleshoot-data-retrieval-issues-with-reporting-services-reports.md)  
[Risolvere i problemi di sottoscrizioni e recapito di Reporting Services](../../reporting-services/troubleshooting/troubleshoot-reporting-services-subscriptions-and-delivery.md)  
  
  
  

[!INCLUDE[feedback_stackoverflow_msdn_connect](../../includes/feedback-stackoverflow-msdn-connect-md.md)]

