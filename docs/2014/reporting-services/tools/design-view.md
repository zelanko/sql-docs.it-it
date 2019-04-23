---
title: Visualizzazione Progettazione | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.rtp.rptdesigner.layoutview.f1
helpviewer_keywords:
- Layout View dialog box
ms.assetid: 6fa378aa-442f-4d2f-beab-02a0fb5cd3ce
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: fad4cf000bda343970c0c2b6c18adb8f5e7fb548
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/22/2019
ms.locfileid: "59946697"
---
# <a name="design-view"></a>Visualizzazione Progettazione
  Utilizzare Visualizzazione progettazione per disporre gli elementi nel report. Tale visualizzazione viene talvolta denominata superficie di progettazione o visualizzazione Layout.  
  
## <a name="report-design-surface"></a>Area di progettazione del report  
 L'area di progettazione è costituita da tre sezioni: corpo del report, intestazione di pagina e piè di pagina. Utilizzare la casella degli strumenti per selezionare gli elementi da inserire nelle tre sezioni. Utilizzare il riquadro dei dati del report per visualizzare immagini, parametri, origini dati e set di dati, inclusi gli elenchi di campi e le query dei set di dati. Dopo avere aggiunto gli elementi del report all'area di progettazione, trascinare i campi dei set di dati dal riquadro **Dati report** in un'area dati, ad esempio una tabella, una matrice o un elenco. Ogni elemento dell'area di progettazione del report contiene proprietà che possono essere gestite tramite la relativa finestra di dialogo delle proprietà o il riquadro Proprietà.  
  
## <a name="toolbox"></a>Casella degli strumenti  
 Nella casella degli strumenti sono elencate le aree dati e gli altri elementi disponibili per il report. Per aggiungere un elemento del report dalla casella degli strumenti, fare doppio clic sull'elemento o trascinarlo nell'area di progettazione. In seguito è possibile modificarne forma e dimensioni tramite gli handle dell'oggetto.  
  
## <a name="report-data-pane"></a>Riquadro dei dati del report  
 Per visualizzare il riquadro dei dati del report, scegliere **Dati report** dal menu **Visualizza**. Utilizzare questo riquadro per definire parametri, immagini, origini dati e set di dati e per fare riferimento a campi predefiniti, ad esempio ReportName. Per aggiungere un nuovo elemento, fare clic sul menu **Nuovo** e selezionare l'elemento. Per aggiungere campi calcolati a un set di dati esistente, fare clic su **Set di dati**e nella finestra di dialogo **Proprietà set di dati** selezionare **Campi**. Selezionare un elemento e fare clic su **Modifica** per aprire la finestra di dialogo **Proprietà** . È inoltre possibile fare clic con il pulsante destro del mouse sugli elementi nel riquadro dei dati del report per aggiungere elementi o aggiornarne le proprietà.  
  
 È possibile aggiungere dati e immagini a un report trascinando gli elementi dal riquadro dei dati del report nelle aree dati e nelle caselle di testo nell'area di progettazione.  
  
 Per altre informazioni, vedere [Report Data Pane](../report-data/report-data-pane.md).  
  
## <a name="grouping-pane"></a>Riquadro di raggruppamento  
 I gruppi vengono utilizzati per organizzare i dati del report in una gerarchia visiva e per calcolare i totali. Utilizzare il Riquadro di raggruppamento per visualizzare i gruppi definiti per una tabella, una matrice, un elenco o un'area dati. Per impostazione predefinita, nel Riquadro di raggruppamento vengono visualizzati tutti i gruppi per l'area dati selezionata sotto forma di elenco bidimensionale. Il Riquadro di raggruppamento è disabilitato per le aree dati Grafico e Misuratore.  
  
 Per vedere le relazioni esistenti tra i gruppi, attivare la modalità Avanzata per il Riquadro di raggruppamento. In questa modalità è possibile vedere la gerarchia dei membri dei gruppi, ovvero ottenere una rappresentazione visiva delle celle dell'area dati che corrispondono a ogni gruppo.  
  
 Per altre informazioni, vedere [Raggruppamento date](grouping-pane.md).  
  
## <a name="page-header-and-page-footer"></a>Intestazione pagina e Piè di pagina  
 Nella parte superiore e inferiore di ogni pagina sono presenti rispettivamente un'intestazione e un piè di pagina. Le intestazioni e i piè di pagina possono contenere testo statico, immagini, linee, rettangoli, bordi, colore di sfondo e immagini di sfondo. Per aggiungere elementi del report all'intestazione o al piè di pagina, fare clic con il pulsante destro del mouse sull'area di progettazione e scegliere Intestazione o Piè di pagina. Le sezioni dell'intestazione e del piè di pagina vengono visualizzate nell'area di progettazione.  
  
## <a name="properties-pane"></a>Riquadro delle proprietà  
 Utilizzare il riquadro Proprietà per visualizzare nell'area di progettazione le proprietà dell'elemento del report selezionato o nel Riquadro di raggruppamento le proprietà del gruppo selezionato. In alternativa, è possibile fare clic con il pulsante destro del mouse su un gruppo o elemento del report selezionato, quindi scegliere **Proprietà** per aprire la finestra di dialogo **Proprietà** corrispondente per l'elemento del report o il gruppo.  
  
## <a name="see-also"></a>Vedere anche  
 [Intestazioni di pagina e piè di pagina &#40;Generatore report e SSRS&#41;](../report-design/page-headers-and-footers-report-builder-and-ssrs.md)   
 [Suggerimenti relativi alla progettazione di report &#40;Generatore report e SSRS&#41;](../report-design/report-design-tips-report-builder-and-ssrs.md)  
  
  
