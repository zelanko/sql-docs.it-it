---
title: Metadati (scheda Esplorazione, Progettazione cubi) (Analysis Services-Dati multidimensionali) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.cubeeditor.browsecube.metadatapane.f1
ms.assetid: a1ace545-488d-4645-8330-56408a5e8abd
author: minewiskan
ms.author: owend
ms.openlocfilehash: dcca1e1e5eec19c81c26fd917e3f557006926233
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/09/2020
ms.locfileid: "84545503"
---
# <a name="metadata-browser-tab-cube-designer-analysis-services---multidimensional-data"></a>Metadati (scheda Esplorazione, Progettazione cubi) (Analysis Services - Dati multidimensionali)
  Usare il riquadro **Metadati** della scheda **Esplorazione** in Progettazione cubi per esplorare la struttura del cubo, visualizzare le misure correlate e visualizzare e creare dimensioni. È possibile eseguire il drill-down in gerarchie, visualizzare un elenco di misure e Indicatori KPI disponibili e copiare i nomi completi di oggetti.  
  
 È anche possibile trascinare gli oggetti e le gerarchie nel riquadro **Metadati** nell'area di compilazione di query, per creare nuove query o esportare dati per visualizzarli in Excel.  
  
## <a name="options"></a>Opzioni  
 **Metadati**  
 Visualizza i metadati disponibili nella vista corrente. È possibile modificare la vista (ovvero, la prospettiva o il cubo attualmente selezionato) facendo clic sull'icona del cubo e usando quindi la finestra di dialogo **Seleziona cubo** per scegliere un nuovo cubo o una nuova prospettiva. È anche possibile fare clic su **Gruppo di misure**e seleziona un nuovo gruppo di misure nell'elenco a discesa per filtrare gli oggetti disponibili nel riquadro **Metadati** .  
  
 Trascinare gli elementi selezionati nelle aree relative a filtro, dati, riga o colonna del controllo Tabella pivot di [!INCLUDE[msCoName](../includes/msconame-md.md)] Office 11.0 nel riquadro **Report** per visualizzare i dati per l'elemento selezionato.  
  
 **Funzioni**  
 Visualizza un elenco di tutte le funzioni, operatori e costanti che è possibile usare per creare query o viste dati in **Esplorazione**. Per utilizzare una funzione, individuare quella desiderato e trascinarla nell'area della query. La definizione della sintassi viene aggiunta al testo  
  
> [!WARNING]  
>  L'elenco **Funzione** non è disponibile quando si usa la visualizzazione della struttura grafica.  
  
 Quando si utilizza un modello tabulare, l'elenco di funzioni include le funzioni MDX e le funzioni DAX. In caso contrario, l'elenco include solo funzioni MDX. In un modello multidimensionale non è possibile utilizzare funzioni DAX direttamente, anche se come parte della definizione di un oggetto potrebbe essere inclusa un'espressione DAX.  
  
 Suggerimento: le cartelle contenenti funzioni DAX sono elencate tutte in lettere maiuscole. Tutte le altre cartelle contengono funzioni MDX. Ad esempio, per le funzioni statistiche sono presenti due cartelle: **STATISTICAL** contiene le funzioni DAX correlate.  
  
## <a name="context-menu"></a>Menu di scelta rapida  
 Le opzioni seguenti sono disponibili nel menu di scelta rapida visualizzato quando si fa clic con il pulsante destro del mouse su un elemento visualizzato nel riquadro **Metadati** :  
  
|Opzione|Descrizione|  
|------------|-----------------|  
|**Aggiungi a query**|Fare clic per aggiungere l'oggetto selezionato al riquadro inferiore dell'area di compilazione della query.|  
|**Aggiungi a filtro**|Fare clic per aggiungere la dimensione, l'attributo, la gerarchia o il livello selezionato all'area filtro di **Esplorazione**.<br /><br /> Nota: questa opzione è abilitata solo se è selezionato un attributo, una dimensione, una gerarchia o un livello.|  
|**Copia**|Fare clic su questo pulsante per aggiungere l'elemento selezionato agli Appunti.<br /><br /> Nota: questa opzione consente di copiare il nome completo dell'oggetto.|  
  
## <a name="see-also"></a>Vedere anche  
 [Barra degli strumenti &#40;scheda Esplorazione, Progettazione cubi&#41; &#40;Analysis Services Dati multidimensionali&#41;](toolbar-browser-tab-cube-designer-analysis-services-multidimensional-data.md)   
 [Analizza in Excel &#40;scheda Esplorazione, Progettazione cubi&#41; &#40;Analysis Services Dati multidimensionali&#41;](analyze-in-excel-browser-cube-designer-analysis-services-multidimensional-data.md)   
 [Eseguire query e filtrare &#40;scheda Esplorazione, Progettazione cubi&#41; &#40;Analysis Services Dati multidimensionali&#41;](query-filter-browser-cube-designer-analysis-services-multidimensional-data.md)   
 [Progettazione cubi &#40;browser&#41; &#40;Analysis Services Dati multidimensionali&#41;](browser-cube-designer-analysis-services-multidimensional-data.md)  
  
  
