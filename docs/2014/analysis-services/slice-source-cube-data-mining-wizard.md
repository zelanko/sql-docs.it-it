---
title: Cubo di origine slice (creazione guidata modello di data mining) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.dm.dmwizard.slicesourcecube.f1
ms.assetid: 16485608-d3b9-49ee-8baa-948038cdd7ec
author: minewiskan
ms.author: owend
ms.openlocfilehash: 762248d4c2a268ac36b0dfa3ffeba20123017017
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84940502"
---
# <a name="slice-source-cube-data-mining-wizard"></a>Sezionamento cubo di origine (Creazione guidata modello di data mining)
  È possibile utilizzare la finestra di dialogo **Sezionamento cubo di origine** per limitare i dati utilizzati per il training del modello. In genere un cubo contiene i dati correlati a molti attributi e dimensioni diversi, ad esempio tutti i negozi, tutte le aree e tutti i prodotti. Poiché non è pratico eseguire il training di un modello su un numero illimitato di combinazioni di attributi, utilizzare questa finestra di dialogo per scegliere un set specifico da utilizzare per il training di un modello.  
  
 Ad esempio, nel cubo AdventureWorks è possibile sezionare per una linea di prodotti, un'area o un anno specifico per ottenere una parte dei dati.  
  
 Se non si ha familiarità con le sezioni e con i cubi, è consigliabile consultare questi articoli:  
  
-   [Impostare la proprietà Slice della partizione &#40;Analysis Services&#41;](multidimensional-models/set-the-partition-slice-property-analysis-services.md)  
  
-   [Creare e gestire una partizione locale &#40;Analysis Services&#41;](multidimensional-models/create-and-manage-a-local-partition-analysis-services.md)  
  
> [!NOTE]  
>  Si noti che le funzioni MDX dinamiche, ad esempio [Generate &#40;MDX&#41;](/sql/mdx/generate-mdx) o [Except &#40;MDX&#41;](/sql/mdx/except-mdx-function) non sono supportate nella proprietà Slice per le partizioni. È necessario definire la sezione usando tuple esplicite o riferimenti ai membri.  
>   
>  Ad esempio, anziché usare [: &#40;intervallo&#41; &#40;&#41;MDX](/sql/mdx/range-mdx) per definire un intervallo, è necessario enumerare ogni membro in base agli anni specifici.  
>   
>  Se occorre definire una sezione complessa, è consigliabile definire le tuple nella sezione mediante uno script XMLA Alter. È quindi possibile usare lo strumento da riga di comando ascmd o l'attività [Analysis Services Execute DDL Task](../integration-services/control-flow/analysis-services-execute-ddl-task.md) di SSIS per eseguire lo script e creare il set di membri specificato immediatamente prima dell'elaborazione della partizione.  
  
 **Per altre informazioni:** [Creazione guidata modello di data mining &#40;Analysis Services - Data mining&#41;](data-mining/data-mining-wizard-analysis-services-data-mining.md) e [Creare una struttura di data mining relazionale](data-mining/create-a-relational-mining-structure.md)  
  
## <a name="options"></a>Opzioni  
 **Dimensione**  
 Consente di selezionare la dimensione che si desidera sezionare.  
  
 **Gerarchia**  
 Consente di selezionare la gerarchia che si desidera sezionare. È possibile scegliere qualsiasi livello di una gerarchia, ma gli attributi utilizzati nel modello saranno valido solo al livello selezionato.  
  
 Se ad esempio si sceglie la gerarchia Geography e si seleziona Country come livello, non è possibile compilare un modello che utilizza City come attributi. Viceversa, se si sceglie City come livello della gerarchia in base a cui eseguire il sezionamento, non è possibile creare un modello di data mining basato su Country.  
  
 **Operatore**  
 Selezionare l'operatore da utilizzare per la compilazione di un'espressione di sezione.  
  
 Se ad esempio si sceglie geography come gerarchia, è possibile selezionare operator = e quindi digitare "Europe" come filtro per ottenere solo i dati del cubo per l'Europa.  
  
 **Espressione filtro**  
 Digitare un'espressione da utilizzare come criterio per filtrare il cubo in base alla dimensione selezionata.  
  
 **Parameters**  
 Questa opzione non è utilizzata per i modelli di data mining.  
  
## <a name="see-also"></a>Vedere anche  
 [Completamento della procedura guidata &#40;creazione guidata modello di data mining&#41;](completing-the-wizard-data-mining-wizard.md)   
 [Guida sensibile al contesto della creazione guidata modello di data mining &#40;Analysis Services-&#41;di data mining](data-mining-wizard-f1-help-analysis-services-data-mining.md)   
 [Impostazione utilizzo colonne modello di data mining &#40;creazione guidata modello di data mining&#41;](specify-mining-model-column-usage-data-mining-wizard.md)  
  
  
