---
title: Diagramma delle relazioni tra attributi (scheda relazione tra attributi, Progettazione dimensioni) (Analysis Services-Dati multidimensionali) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.dimensiondesigner.ardesigner.ardiagram.f1
ms.assetid: 320989ad-bd95-43f4-a2e7-b262d66dbda7
author: minewiskan
ms.author: owend
ms.openlocfilehash: 0f0e03c8d06d018390a3537ec15c4ab06c927bf4
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/08/2020
ms.locfileid: "84527897"
---
# <a name="attribute-relationship-diagram-attribute-relationship-designer-tab-dimension-designer-analysis-services---multidimensional-data"></a>Diagramma delle relazioni tra attributi (scheda Relazione tra attributi, Progettazione dimensioni) (Analysis Services - Dati multidimensionali)
  Utilizzare il riquadro immediatamente sotto la barra degli strumenti sulla scheda **Relazione tra attributi** per visualizzare il diagramma delle relazioni tra attributi e per creare, modificare ed eliminare relazioni tra attributi.  
  
 **Per visualizzare il riquadro che contiene il diagramma delle relazioni tra attributi**  
  
-   In [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]fare doppio clic su una dimensione in Esplora soluzioni per aprire Progettazione dimensioni, quindi fare clic sulla scheda **Relazione tra attributi** .  
  
## <a name="using-the-attribute-relationship-diagram"></a>Utilizzo del diagramma delle relazioni tra attributi  
 Utilizzare il diagramma delle relazioni tra attributi per creare, modificare o eliminare relazioni tra attributi. Il diagramma delle relazioni tra attributi evidenzierà anche relazioni tra attributi problematiche e visualizzerà una descrizione del problema in una descrizione comandi.  
  
 Esistono tre menu di scelta rapida separati disponibili nel diagramma: il menu di scelta rapida del diagramma, il menu di scelta rapida dell'attributo e il menu di scelta rapida della relazione.  
  
### <a name="diagram-shortcut-menu"></a>Menu di scelta rapida del diagramma  
 Per aprire il menu di scelta rapida per il diagramma della relazione tra attributi, fare clic con il pulsante destro del mouse sullo sfondo del diagramma. Nel menu di scelta rapida del diagramma sono disponibili i seguenti comandi:  
  
 **Nuova relazione tra attributi**  
 Viene aperta la finestra di dialogo **Crea relazione tra attributi** in cui è possibile definire una nuova relazione tra attributi.  
  
 Per altre informazioni, vedere [Creare finestre di dialogo Relazione tra attributi e Modifica relazione tra attributi &#40;scheda Relazione tra attributi, Progettazione dimensioni&#41; &#40;Analysis Services - Dati multidimensionali&#41;](create-edit-attribute-relationships-dialog-boxes-analysis-services-multidimensional-data.md) e [Definire relazioni tra attributi](multidimensional-models/attribute-relationships-define.md).  
  
 **Disponi forme**  
 Dispone le forme secondo l'algoritmo del layout utilizzato dalla Finestra di Progettazione dimensioni.  
  
 **Disposizione automatica forme**  
 Dispone automaticamente le forme nel diagramma secondo l'algoritmo di layout utilizzato da Progettazione dimensioni. Per impostazione predefinita, l'opzione **Disposizione automatica forme** è attivata.  
  
 **Mostra visualizzazioni elenco**  
 Visualizza o nasconde gli elenchi **Attributi** e **Relazioni tra attributi** . Questi elenchi vengono visualizzati nei riquadri che si trovano sotto quello che contiene il diagramma delle relazioni tra attributi.  
  
 **Espandi tutte le forme**  
 Visualizza gli attributi raggruppati associati con gli attributi di livello superiore. Gli attributi raggruppati sono visibili solo quando le forme nel diagramma delle relazioni tra attributi sono espanse.  
  
> [!NOTE]  
>  Selezionando questa opzione, Progettazione dimensioni riporterà le forme nel diagramma delle relazioni tra attributi al layout predefinito utilizzato dalla finestra di progettazione.  
  
 **Comprimi tutte le forme**  
 Nasconde gli attributi raggruppati associati con gli attributi di livello superiore.  
  
> [!NOTE]  
>  Selezionando questa opzione, Progettazione dimensioni riporterà le forme nel diagramma delle relazioni tra attributi al layout predefinito utilizzato dalla finestra di progettazione.  
  
 **Zoom**  
 Visualizza un elenco di opzioni di zoom disponibili.  
  
### <a name="attribute-shortcut-menu"></a>Menu di scelta rapida dell’attributo  
 Per aprire il menu di scelta rapida dell’attributo, fare click con il pulsante destro del mouse su un attributo nel diagramma della relazione tra attributi. Nel menu di scelta rapida dell’attributo sono disponibili i seguenti comandi:  
  
 **Nuova relazione tra attributi**  
 Viene aperta la finestra di dialogo **Crea relazione tra attributi** in cui è possibile definire una nuova relazione tra attributi.  
  
 Per altre informazioni, vedere [Creare finestre di dialogo Relazione tra attributi e Modifica relazione tra attributi &#40;scheda Relazione tra attributi, Progettazione dimensioni&#41; &#40;Analysis Services - Dati multidimensionali&#41;](create-edit-attribute-relationships-dialog-boxes-analysis-services-multidimensional-data.md) e [Definire relazioni tra attributi](multidimensional-models/attribute-relationships-define.md).  
  
 **Proprietà**  
 Visualizza le proprietà dell'attributo nella finestra **Proprietà** .  
  
### <a name="relationship-shortcut-menu"></a>Menu di scelta rapida della relazione  
 Per aprire il menu di scelta rapida della relazione, fare clic con il pulsante destro del mouse sulla freccia che identifica la relazione tra due attributi. Nel menu di scelta rapida della relazione sono disponibili i seguenti comandi:  
  
 **Modifica relazione tra attributi**  
 Apre la finestra di dialogo **Modifica relazione tra attributi** nella quale è possibile modificare la relazione tra gli attributi.  
  
 Per altre informazioni, vedere [Creare finestre di dialogo Relazione tra attributi e Modifica relazione tra attributi &#40;scheda Relazione tra attributi, Progettazione dimensioni&#41; &#40;Analysis Services - Dati multidimensionali&#41;](create-edit-attribute-relationships-dialog-boxes-analysis-services-multidimensional-data.md) e [Definire relazioni tra attributi](multidimensional-models/attribute-relationships-define.md).  
  
 **Tipo di relazione**  
 Imposta il tipo di relazione su **Flessibile** o **Rigida**. In una relazione flessibile, le relazioni tra membri cambiano nel tempo. In una relazione rigida, le relazioni tra membri non cambiano nel tempo.  
  
 **Eliminazione**  
 Elimina la relazione tra attributi  
  
 **Proprietà**  
 Visualizza le proprietà della relazione nella finestra **Proprietà** .  
  
## <a name="see-also"></a>Vedere anche  
 [Relazioni tra attributi &#40;Progettazione dimensioni&#41; &#40;Analysis Services Dati multidimensionali&#41;](attribute-relationships-dimension-designer-analysis-services-multidimensional-data.md)   
 [Barra degli strumenti &#40;scheda Progettazione relazione tra attributi, Progettazione dimensioni&#41; &#40;Analysis Services Dati multidimensionali&#41;](toolbar-attribute-relationship-dimension-designer-analysis-services-multidimensional-data.md)   
 [Attributi &#40;scheda Progettazione relazione tra attributi, Progettazione dimensioni&#41; &#40;Analysis Services Dati multidimensionali&#41;](attributes-designer-tab-dimension-designer-analysis-services-multidimensional-data.md)   
 [Relazioni tra attributi &#40;scheda Progettazione relazione tra attributi, Progettazione dimensioni&#41; &#40;Analysis Services Dati multidimensionali&#41;](attribute-relationships-designer-tab-dimension-designer-analysis-services-multidimensional-data.md)  
  
  
