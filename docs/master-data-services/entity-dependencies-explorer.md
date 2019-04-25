---
title: Esplorazione delle dipendenze di entità | Microsoft Docs
ms.custom: ''
ms.date: 04/06/2016
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
keywords:
- Master Data Services
ms.assetid: 9d922118-1412-4a9d-9c02-70d6c48d6c0d
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 0665b6f7d54b7f83f3edda224be4e9efad670e90
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62518129"
---
# <a name="entity-dependencies-explorer"></a>Esplorazione delle dipendenze di entità

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  
[!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] 2016 aggiunge una nuova pagina di esplorazione relativa alle dipendenze di entità che fornisce un modo alternativo per visualizzare le relazioni tra i membri di entità all'interno di un modello, come specificato dai relativi valori di attributo basati sul dominio (DBA), ma senza dover prima definire una gerarchia derivata.   
  
Tale pagina consente di conoscere chi sta utilizzando l'entità e in che modo. La visualizzazione è simile a quella della pagina di esplorazione Gerarchia derivata, ma è più completa. Consente di visualizzare tutte le relazioni DBA, non solo quelle definite come parte di una specifica gerarchia. Non è necessaria una definizione della gerarchia perché la struttura gerarchica visualizzata viene semplicemente dedotta dai DBA esistenti.  
  
Nel menu della pagina Esplora, la voce di menu relativa alle dipendenze di entità elenca tutte le entità nel modello che dipendono da almeno un'entità (ossia almeno un'entità dispone di un DBA che fa riferimento all'entità elencata). Il numero di dipendenze (dirette e indirette) viene visualizzato accanto al nome dell'entità e l'elenco è ordinato in base a questo numero con le entità a cui si fa riferimento più ampiamente nella parte superiore. La seguente schermata ricavata dal modello cliente dei [dati di esempio](https://msdn.microsoft.com/library/master-data-services-sample.aspx), mostra che all'entità BigArea viene fatto riferimento (direttamente o indirettamente) da 7 entità:  
  
![MDS_EntityDependencies_Menu.jpg](../master-data-services/media/mds-entitydependencies-menu-jpg.jpg)  
    
Facendo clic su questa voce di menu si apre la nuova pagina di esplorazione relativa alle dipendenze di entità per l'entità BigArea, che visualizza la modalità in cui vengono utilizzati i membri dell'entità. Viene mostrata una visualizzazione gerarchica con i membri di BigArea nella parte superiore della struttura e i membri delle relative 7 entità nidificate nella parte sottostante:  
  
![MDS_EntityDependencies_Tree.jpg](../master-data-services/media/mds-entitydependencies-tree-jpg.jpg)  
    
Un'entità può essere utilizzata direttamente da più di un'entità. Nell'esempio precedente, le entità SubRegion e RegionClimate vengono utilizzate dall'entità Region e hanno riferimenti DBA a tale entità. I membri di ogni entità utilizzata vengono raggruppati sotto un nodo padre che contiene il nome dell'entità:   
  
![MDS_EntityDependencies_Entity_Node.jpg](../master-data-services/media/mds-entitydependencies-entity-node-jpg.jpg)  
  
Questi nodi della struttura contenitore hanno un'icona a forma di griglia a sinistra del nome dell'entità e il testo ha un colore che dipende dalla profondità del livello della gerarchia. L'esempio precedente mostra che l'entità SubRegion "CDSR {Canada}" ha un riferimento DBA all'entità Region "CDR {Canada}", che fa riferimento all'entità Area "CDA {Canada}", che a sua volta fa riferimento all'entità BigArea "NAm {N. America}".  
  
La visualizzazione è completamente modificabile, come nella pagina del visualizzatore della gerarchia. È possibile modificare le relazioni padre-figlio nella struttura mediante operazioni taglia-incolla o di trascinamento di membri figlio da un elemento padre a un altro. È possibile modificare altri valori di attributo del membro nel riquadro dei dettagli a destra della struttura.   
  
  
  
  

