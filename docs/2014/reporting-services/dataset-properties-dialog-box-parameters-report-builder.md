---
title: Finestra di dialogo Proprietà set di dati, parametri (Generatore Report) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10023"
ms.assetid: 3a0672ad-c969-455b-b952-585164ce1dda
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: fe7194c8a6f54da50eeef21891bc1049735ddd1e
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63164988"
---
# <a name="dataset-properties-dialog-box-parameters-report-builder"></a>Finestra di dialogo Proprietà set di dati, Parametri (Generatore report)
  Selezionare **parametri** nel **proprietà set di dati** finestra di dialogo per aggiungere, modificare ed eliminare parametri di query.  
  
 Relativamente ai set di dati incorporati, le opzioni vengono applicate al set di dati nella definizione del report.  
  
 Relativamente ai set di dati condiviso, le opzioni vengono applicate alla definizione del set di dati condiviso nel server di report.  
  
 Per altre informazioni, vedere [Set di dati condivisi e incorporati &#40;Generatore report e SSRS&#41;](report-data/embedded-and-shared-datasets-report-builder-and-ssrs.md).  
  
## <a name="options"></a>Opzioni  
 **Aggiungi**  
 Consente di aggiungere un nuovo parametro all'elenco.  
  
 **Elimina**  
 Consente di rimuovere il parametro selezionato dall'elenco.  
  
 **Freccia in su**  
 Consente di spostare il parametro selezionato verso l'alto nell'elenco.  
  
 **Freccia GIÙ**  
 Consente di spostare il parametro selezionato verso il basso nell'elenco.  
  
 **Nome parametro**  
 Digitare il nome di un parametro di query aggiunto al set di dati nella scheda **Query** della finestra di dialogo **Proprietà set di dati** .  
  
 **Valore parametro**  
 Solo per i set di dati incorporati.  
  
 Immettere un valore per il parametro di query. Può trattarsi di un valore statico o di un'espressione che fa riferimento a un oggetto nel report, ma non a un campo o a un elemento del report. Per impostazione predefinita, in **Valore** è contenuta un'espressione che punta a un parametro del report.  
  
 **Valore predefinito**  
 Solo per i set di dati condivisi.  
  
 Selezionare la casella di controllo per specificare un valore predefinito.  
  
 Immettere un valore predefinito. Può trattarsi di un valore statico o di un'espressione che fa riferimento a un oggetto all'interno del report, ad eccezione di elementi del report, parametri del report e campi.  
  
 Per specificare un valore vuoto, lasciare la casella di testo vuota.  
  
 Per specificare un valore Null, selezionare l'opzione Ammette i valori Null.  
  
 **Sola lettura**  
 Solo per i set di dati condivisi.  
  
 Selezionare questa opzione per contrassegnare questo parametro per la sola lettura nella definizione del set di dati condiviso. Quando si aggiunge il set di dati condiviso a un report, il parametro non viene visualizzato nelle proprietà. Quando si memorizza il set di dati condiviso nella cache del server di report, non è possibile modificare il valore.  
  
 **Ammette i valori Null**  
 Solo per i set di dati condivisi.  
  
 Selezionare questa opzione per consentire un valore Null.  
  
 **Ometti dalla Query**  
 Solo per i set di dati condivisi.  
  
 Selezionare questa opzione quando un riferimento a un parametro del report si trova in un'espressione del filtro del set di dati condiviso e non della query. Se si seleziona questa opzione, non è necessario specificare un valore predefinito per questo parametro quando la query è in esecuzione.  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di Generatore report per finestre di dialogo, riquadri e procedure guidate](../../2014/reporting-services/report-builder-help-for-dialog-boxes-panes-and-wizards.md)   
 [Finestra di dialogo Proprietà set di dati, la Query &#40;Generatore Report&#41;](report-data/dataset-properties-dialog-box-query-report-builder.md)   
 [Espressioni &#40;Generatore report e SSRS&#41;](report-design/expressions-report-builder-and-ssrs.md)   
 [Esercitazione: Aggiungere un parametro al report &#40;Generatore report&#41;](tutorial-add-a-parameter-to-your-report-report-builder.md)   
 [Parametri report &#40;Generatore report e Progettazione report&#41;](report-design/report-parameters-report-builder-and-report-designer.md)   
 [Set di dati condivisi e incorporati del report &#40;Generatore report e SSRS&#41;](report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)   
 [Finestre di progettazione query &#40;Generatore report&#41;](../../2014/reporting-services/query-designers-report-builder.md)   
 [Set di dati condivisi e incorporati del report &#40;Generatore report e SSRS&#41;](report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)   
 [Creare un set di dati condiviso o un set di dati incorporato &#40;Generatore report e SSRS&#41;](report-data/create-a-shared-dataset-or-embedded-dataset-report-builder-and-ssrs.md)  
  
  
