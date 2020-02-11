---
title: Formattare il testo in una casella di testo (Generatore report e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: df0794b5-96b0-4034-bd17-1be7f31e29db
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 976130697e759fa4231ad73113d0970e345dbb3a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66105871"
---
# <a name="format-text-in-a-text-box-report-builder-and-ssrs"></a>Formattare il testo in una casella di testo (Generatore report e SSRS)
  È possibile formattare qualsiasi parte del testo all'interno di una casella di testo in modo indipendente e combinare testo segnaposto e testo statico in un'unica casella di testo. La possibilità di combinare i formati e aggiungere testo segnaposto consente di creare stampe unione o modelli per il testo nel report. Qualsiasi espressione può essere definita e formattata separatamente utilizzando un segnaposto.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-combine-multiple-formats-in-a-text-box"></a>Per combinare più formati in una casella di testo  
  
1.  Fare clic su **Casella testo** nella scheda **Inserisci**. Fare clic nell'area di progettazione, quindi trascinare il mouse per creare una casella delle dimensioni desiderate.  
  
2.  All'interno della casella di testo selezionare il testo che si desidera formattare.  
  
3.  Fare clic con il pulsante destro del mouse sul testo selezionato, quindi scegliere **Proprietà testo**.  
  
4.  Impostare le opzioni di formattazione. Ad esempio, nella scheda **Generale** :  
  
    -   **Descrizione comando** Digitare un testo o un'espressione che restituisca una descrizione comando. La descrizione comando viene visualizzata quando l'utente posiziona il puntatore del mouse su un elemento nel report.  
  
    -   **Tipo di markup** Selezionare un'opzione per indicare come verrà visualizzato il testo selezionato:  
  
         **Testo normale** Il testo selezionato viene visualizzato come testo normale. Il testo in formato HTML verrà gestito come testo letterale.  
  
         **HTML**  Il testo selezionato viene visualizzato in formato HTML. Se il valore dell'espressione del segnaposto contiene tag HTML validi, questi verranno visualizzati in formato HTML. Per altre informazioni, vedere [Importazione di codice HTML in un report &#40;Generatore report e SSRS&#41;](importing-html-into-a-report-report-builder-and-ssrs.md).  
  
5.  Fare clic su **OK**.  
  
6.  Ripetere i passaggi da 2 a 5 per la parte di testo rimanente che si desidera formattare.  
  
### <a name="to-format-text-and-placeholders-differently-in-the-same-text-box"></a>Per formattare in modo diverso testo e segnaposti presenti nella stessa casella di testo  
  
1.  Fare clic su **Elenco** nella scheda **Inserisci**. Fare clic nell'area di progettazione, quindi trascinare il mouse per creare una casella delle dimensioni desiderate. Verrà visualizzata la finestra di dialogo **Proprietà set di dati** . È possibile utilizzare un set di dati condiviso o un set di dati incorporato nel report. Per altre informazioni, fare clic su [Finestra di dialogo Proprietà set di dati, Query &#40;Generatore report&#41;](../report-data/dataset-properties-dialog-box-query-report-builder.md) o [Finestra di dialogo Proprietà set di dati, Query](../dataset-properties-dialog-box-query.md).  
  
2.  Fare clic su **Casella testo** nella scheda **Inserisci**. Fare clic nell'elenco, quindi trascinare il mouse per creare una casella con le dimensioni desiderate.  
  
3.  Digitare un'etichetta nella casella di testo, ad esempio **Mio campo**:.  
  
4.  Trascinare un campo dal set di dati nella casella di testo. Verrà creato un segnaposto per il campo.  
  
5.  Per una formattazione di base, selezionare il testo segnaposto, quindi fare clic su una delle opzioni di formattazione nel gruppo **Carattere** della scheda **Home** . Fare clic, ad esempio, sul pulsante **Grassetto**.  
  
     Per applicare più opzioni di formattazione, fare clic con il pulsante destro del mouse sul testo segnaposto, quindi fare clic su **Proprietà segnaposto**.  
  
6.  Fare clic su **OK**. Nella visualizzazione Progettazione report, la casella di testo conterrà "**Mio campo**: [*NomeCampo*]", dove *NomeCampo* è il nome del campo.  
  
7.  Fare clic su **Esegui**.  
  
 L'elenco viene ripetuto una volta per ogni valore nel campo e il segnaposto *NomeCampo* viene sostituito ogni volta dal valore di quel campo nel set di dati.  
  
## <a name="see-also"></a>Vedere anche  
 [Caselle di testo &#40;Generatore report e SSRS&#41;](text-boxes-report-builder-and-ssrs.md)   
 [Formattazione di testo e segnaposto &#40;Generatore report e SSRS&#41;](formatting-text-and-placeholders-report-builder-and-ssrs.md)   
 [Utilizzo delle espressioni nei report &#40;Generatore report e SSRS&#41;](expression-uses-in-reports-report-builder-and-ssrs.md)   
 [Esempi di espressioni &#40;Generatore report e SSRS&#41;](expression-examples-report-builder-and-ssrs.md)   
 [Aggiungere il codice HTML a un report &#40;Generatore report e SSRS&#41;](add-html-into-a-report-report-builder-and-ssrs.md)   
 [Elenchi &#40;Generatore report e SSRS&#41;](tables-matrices-and-lists-report-builder-and-ssrs.md)   
 [Formattazione di numeri e date &#40;Generatore report e SSRS&#41;](formatting-numbers-and-dates-report-builder-and-ssrs.md)   
 [Finestra di dialogo Proprietà segnaposto, Generale &#40;Generatore report e SSRS&#41;](../placeholder-properties-dialog-box-general-report-builder-and-ssrs.md)  
  
  
