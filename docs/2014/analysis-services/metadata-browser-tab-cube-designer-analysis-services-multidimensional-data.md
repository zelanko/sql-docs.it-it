---
title: Metadati (scheda esplorazione, Progettazione cubi) (Analysis Services - dati multidimensionali) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.cubeeditor.browsecube.metadatapane.f1
ms.assetid: a1ace545-488d-4645-8330-56408a5e8abd
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 31c14a039d22238450023c4a7f9b7b099e9a2a53
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62727947"
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
  
 Suggerimento: Le cartelle contenenti funzioni DAX sono elencate tutte le lettere maiuscole. Tutte le altre cartelle contengono funzioni MDX. Ad esempio, sono presenti due cartelle per le funzioni statistiche: **STATISTICA** contiene le funzioni DAX correlate.  
  
## <a name="context-menu"></a>Menu di scelta rapida  
 Le opzioni seguenti sono disponibili nel menu di scelta rapida visualizzato quando si fa clic con il pulsante destro del mouse su un elemento visualizzato nel riquadro **Metadati** :  
  
|Opzione|Descrizione|  
|------------|-----------------|  
|**Aggiungere alla Query**|Fare clic per aggiungere l'oggetto selezionato al riquadro inferiore dell'area di compilazione della query.|  
|**Aggiungi a filtro**|Fare clic per aggiungere la dimensione, l'attributo, la gerarchia o il livello selezionato all'area filtro di **Esplorazione**.<br /><br /> Nota: Questa opzione è abilitata solo se una dimensione, attributo, gerarchia o livello sia selezionato.|  
|**Copia**|Fare clic su questo pulsante per aggiungere l'elemento selezionato agli Appunti.<br /><br /> Nota: Questa opzione consente di copiare il nome completo dell'oggetto.|  
  
## <a name="see-also"></a>Vedere anche  
 [Sulla barra degli strumenti &#40;scheda esplorazione, Progettazione cubi&#41; &#40;Analysis Services - dati multidimensionali&#41;](toolbar-browser-tab-cube-designer-analysis-services-multidimensional-data.md)   
 [Analizza in Excel &#40;scheda esplorazione, Progettazione cubi&#41; &#40;Analysis Services - dati multidimensionali&#41;](analyze-in-excel-browser-cube-designer-analysis-services-multidimensional-data.md)   
 [Progettazione query e filtro &#40;scheda esplorazione, Progettazione cubi&#41; &#40;Analysis Services - dati multidimensionali&#41;](query-filter-browser-cube-designer-analysis-services-multidimensional-data.md)   
 [Browser &#40;Progettazione cubi&#41; &#40;Analysis Services - dati multidimensionali&#41;](browser-cube-designer-analysis-services-multidimensional-data.md)  
  
  
