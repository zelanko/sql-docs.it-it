---
title: Editor form membro calcolato (scheda calcoli, Progettazione cubi) (Analysis Services-Dati multidimensionali) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.cubeeditor.calculationexpression.calculatedmember.f1
ms.assetid: f7719b9e-b1e6-4792-90a6-30d9d8eb1196
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 432300f54a7678970f394b27712bcb28ba8a7e7d
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "66088364"
---
# <a name="calculated-member-form-editor-calculations-tab-cube-designer-analysis-services---multidimensional-data"></a>Editor form membro calcolato (scheda Calcoli, Progettazione cubi) (Analysis Services - Dati multidimensionali)
  Il riquadro **Editor form membro calcolato** nella scheda **Calcoli** di Progettazione cubi consente di creare o modificare un membro calcolato.  
  
 **Nota** Questo riquadro viene visualizzato solo nella visualizzazione Form.  
  
## <a name="options"></a>Opzioni  
 **Nome**  
 Consente di digitare il nome del membro calcolato.  
  
 **Proprietà padre**  
 Espandere la finestra per visualizzare le opzioni **Gerarchia padre**, **Membro padre**e **Cambia** .  
  
 **Gerarchia padre**  
 Consente di selezionare la dimensione e la gerarchia nel cubo selezionato che dovrà includere il membro calcolato. Selezionare MEASURES per definire una misura calcolata.  
  
 **Membro padre**  
 Consente di selezionare il membro sotto cui verrà visualizzato il membro calcolato.  
  
 **Nota** Questa opzione è disponibile se **Gerarchia padre** specifica una gerarchia diversa da MEASURES.  
  
 **Modificare**  
 Selezionare questa opzione per visualizzare la finestra di dialogo **Seleziona membro padre** e scegliere un membro per **Membro padre**. Per altre informazioni sulla finestra di dialogo **Seleziona membro padre**, vedere [Finestra di dialogo Seleziona membro padre &#40;Analysis Services - Dati multidimensionali&#41;](select-parent-member-dialog-box-analysis-services-multidimensional-data.md).  
  
 **Espressione**  
 Espandere la finestra per visualizzare o modificare l'espressione MDX per il membro calcolato.  
  
 Trascinare gli elementi selezionati dal riquadro **Strumenti di calcolo** alla casella di questa opzione per includere la sintassi MDX per l'elemento selezionato.  
  
> [!NOTE]  
>  È consigliabile che questa espressione restituisca una stringa o un valore numerico.  
  
 **Proprietà aggiuntive**  
 Espandere la finestra per visualizzare le opzioni **Stringa di formato**, **Visibile**, **Gestione NON EMPTY**, **Espressioni colori**ed **Espressioni caratteri** .  
  
 **Stringa di formato**  
 Consente di digitare la stringa di formato MDX utilizzata per formattare il valore restituito dal membro calcolato oppure di selezionare una stringa di formato predefinita.  
  
 Per altre informazioni sulle stringhe di formato MDX, vedere [Contenuto di FORMAT_STRING &#40;MDX&#41;](multidimensional-models/mdx/mdx-cell-properties-format-string-contents.md).  
  
 **Visibile**  
 Selezionare **True** per consentire la visualizzazione del membro calcolato alle applicazioni client.  
  
 **Comportamento non vuoto**  
 Consente di selezionare il nome della misura utilizzata per risolvere le query NON EMPTY in formato MDX per il membro calcolato. Se la proprietà **Gestione NON EMPTY** è vuota, il membro calcolato dovrà essere valutato più volte per determinare se un membro è vuoto. Se la proprietà **Gestione NON EMPTY** contiene il nome di una misura, il membro calcolato verrà considerato vuoto nel caso in cui la misura specificata sia vuota.  
  
> [!WARNING]  
>  Questa proprietà è deprecata. Evitare di impostarla. Per informazioni dettagliate, vedere [deprecated Analysis Services features in SQL Server 2014](deprecated-analysis-services-features-in-sql-server-2014.md) .  
  
 **Espressioni colori**  
 Espandere la finestra per visualizzare le opzioni **Colore primo piano** e **Colore sfondo** .  
  
 **Colore primo piano**  
 Consente di digitare l'espressione MDX che offre il colore di primo piano del membro calcolato.  
  
 Trascinare gli elementi selezionati dal riquadro **Strumenti di calcolo** alla casella di questa opzione per includere la sintassi MDX per l'elemento selezionato.  
  
 Fare clic sul pulsante di selezione del colore per visualizzare la finestra di dialogo **Colore** e inserire il valore RGB (Red-Green-Blue) relativo a un colore specificato nell'espressione MDX. Per altre informazioni sui valori RGB, vedere [Contenuto di FORE_COLOR e BACK_COLOR &#40;MDX&#41;](multidimensional-models/mdx/mdx-cell-properties-fore-color-and-back-color-contents.md).  
  
 **Colore sfondo**  
 Consente di digitare l'espressione MDX che offre il colore di sfondo del membro calcolato.  
  
 Trascinare gli elementi selezionati dal riquadro **Strumenti di calcolo** alla casella di questa opzione per includere la sintassi MDX per l'elemento selezionato.  
  
 Fare clic sul pulsante di selezione del colore per visualizzare la finestra di dialogo **Colore** e inserire il valore RGB (Red-Green-Blue) relativo a un colore specificato nell'espressione MDX. Per altre informazioni sui valori RGB, vedere [Contenuto di FORE_COLOR e BACK_COLOR &#40;MDX&#41;](multidimensional-models/mdx/mdx-cell-properties-fore-color-and-back-color-contents.md).  
  
 **Espressioni caratteri**  
 Espandere la finestra per visualizzare le opzioni **Tipo carattere**, **Dimensione carattere**e **Flag carattere** .  
  
 **Nome carattere**  
 Consente di digitare l'espressione MDX che offre il nome del carattere utilizzato per il membro calcolato.  
  
 Trascinare gli elementi selezionati dal riquadro **Strumenti di calcolo** alla casella di questa opzione per includere la sintassi MDX per l'elemento selezionato.  
  
 Fare clic sul pulsante di selezione del carattere per visualizzare la finestra di dialogo **Carattere** e inserire i valori di proprietà relativi a un carattere specificato nell'espressione MDX. Per altre informazioni sui valori delle proprietà, vedere [Creazione e utilizzo di valori di proprietà &#40;MDX&#41;](creating-and-using-property-values-mdx.md).  
  
 **Dimensioni carattere**  
 Consente di digitare l'espressione MDX che offre le dimensioni del carattere utilizzato per il membro calcolato.  
  
 Trascinare gli elementi selezionati dal riquadro **Strumenti di calcolo** alla casella di questa opzione per includere la sintassi MDX per l'elemento selezionato.  
  
 Fare clic sul pulsante di selezione del carattere per visualizzare la finestra di dialogo **Carattere** e inserire i valori di proprietà relativi a un carattere specificato nell'espressione MDX. Per altre informazioni sui valori delle proprietà, vedere [Creazione e utilizzo di valori di proprietà &#40;MDX&#41;](creating-and-using-property-values-mdx.md).  
  
 **Flag carattere**  
 Consente di digitare l'espressione MDX che offre il valore bitmap contenente i flag, quali sottolineato o grassetto, del carattere utilizzato per il membro calcolato.  
  
 Trascinare gli elementi selezionati dal riquadro **Strumenti di calcolo** alla casella di questa opzione per includere la sintassi MDX per l'elemento selezionato.  
  
 Fare clic sul pulsante di selezione del carattere per visualizzare la finestra di dialogo **Carattere** e inserire i valori di proprietà relativi a un carattere specificato nell'espressione MDX. Per altre informazioni sui valori delle proprietà, vedere [Creazione e utilizzo di valori di proprietà &#40;MDX&#41;](creating-and-using-property-values-mdx.md).  
  
## <a name="see-also"></a>Vedi anche  
 [Calcoli](multidimensional-models-olap-logical-cube-objects/calculations.md)   
 [Creazione di membri calcolati](multidimensional-models/create-calculated-members.md)   
 [Progettazione cubi &#40;Analysis Services-Dati multidimensionali&#41;](cube-designer-analysis-services-multidimensional-data.md)   
 [Calcoli &#40;Progettazione cubi&#41; &#40;Analysis Services Dati multidimensionali&#41;](calculations-cube-designer-analysis-services-multidimensional-data.md)   
 [Barra degli strumenti &#40;scheda calcoli, Progettazione cubi&#41; &#40;Analysis Services Dati multidimensionali&#41;](toolbar-calculations-tab-cube-designer-analysis-services-multidimensional-data.md)   
 [Libreria script &#40;scheda calcoli, Progettazione cubi&#41; &#40;Analysis Services Dati multidimensionali&#41;](script-organizer-cube-designer-analysis-services-multidimensional-data.md)   
 [Strumenti di calcolo &#40;scheda calcoli, Progettazione cubi&#41; &#40;Analysis Services Dati multidimensionali&#41;](calculation-tools-cube-designer-analysis-services-multidimensional-data.md)   
 [Editor form set denominato &#40;scheda calcoli, Progettazione cubi&#41; &#40;Analysis Services Dati multidimensionali&#41;](named-set-form-editor-cube-designer-analysis-services-multidimensional-data.md)   
 [Editor di script &#40;scheda calcoli, Progettazione cubi&#41; &#40;Analysis Services Dati multidimensionali&#41;](script-editor-calculations-cube-designer-analysis-services-multidimensional-data.md)  
  
  
