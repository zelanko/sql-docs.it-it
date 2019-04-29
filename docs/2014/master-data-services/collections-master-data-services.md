---
title: Raccolte (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- collections [Master Data Services]
- collections [Master Data Services], about collections
ms.assetid: 5aa1d1e0-b4e5-4897-8e74-01dcf418df73
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 3533108054d1c65e73f3167d68a05727e95fa2d4
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62925610"
---
# <a name="collections-master-data-services"></a>Raccolte (Master Data Services)
  Una raccolta è un gruppo di membri foglia e membri consolidati da una singola entità. Utilizzare le raccolte quando non è necessaria una gerarchia completa e si desidera visualizzare raggruppamenti diversi dei membri per la creazione di report o l'analisi o quando è necessario creare una tassonomia.  
  
## <a name="what-collections-contain"></a>Contenuto delle raccolte  
 Le raccolte non impongono un limite sul numero o il tipo di membri che è possibile includere, purché questi si trovino all'interno della stessa entità. Una raccolta può contenere membri foglia e consolidati di più gerarchie esplicite obbligatorie e non obbligatorie.  
  
 Quando si crea una raccolta, non si crea una struttura gerarchica, ma un elenco semplice di membri. Quando si seleziona un nodo da una gerarchia e lo si aggiunge alla raccolta, il membro consolidato selezionato è l'unico membro aggiunto alla raccolta.  
  
 Una raccolta può inoltre contenere altre raccolte. È possibile utilizzare raccolte di raccolte per creare tassonomie.  
  
 L'utente che crea una raccolta viene elencato automaticamente come proprietario. Gli amministratori possono creare altri attributi per la raccolta in base alle necessità.  
  
> [!NOTE]  
>  Prima di creare una raccolta, è necessario abilitare l'entità per le gerarchie esplicite. Per altre informazioni, vedere [abilitare un'entità per gerarchie esplicite e raccolte &#40;Master Data Services&#41;](enable-an-entity-for-explicit-hierarchies-and-collections-master-data-services.md).  
  
## <a name="subscription-views-for-collections"></a>Viste sottoscrizioni per le raccolte  
 Sono disponibili due tipi di viste sottoscrizioni che mostrano le raccolte. Il formato **Attributi raccolta** mostra un elenco di raccolte e degli attributi correlati alle raccolte (come descrizione o proprietario). Il formato **Raccolte** mostra tutti i membri di tutte le raccolte,, nonché il peso e l'ordinamento dei membri. Per altre informazioni, vedere [esportazione di dati &#40;Master Data Services&#41;](overview-exporting-data-master-data-services.md).  
  
 Se si impostano valori di peso per membri specifici di una raccolta, questi valori sono disponibili nelle viste sottoscrizioni correlate.  
  
## <a name="related-tasks"></a>Attività correlate  
  
|Descrizione dell'attività|Argomento|  
|----------------------|-----------|  
|Abilitare un'entità per le gerarchie esplicite e le raccolte.|[Abilitare un'entità per gerarchie esplicite e raccolte di &#40;Master Data Services&#41;](enable-an-entity-for-explicit-hierarchies-and-collections-master-data-services.md)|  
|Creare una nuova raccolta.|[Creare una raccolta &#40;Master Data Services&#41;](../../2014/master-data-services/create-a-collection-master-data-services.md)|  
|Aggiungere membri a una raccolta esistente.|[Aggiungere membri a una raccolta &#40;Master Data Services&#41;](../../2014/master-data-services/add-members-to-a-collection-master-data-services.md)|  
  
## <a name="related-content"></a>Contenuto correlato  
  
-   [Gerarchie esplicite &#40;Master Data Services&#41;](../../2014/master-data-services/explicit-hierarchies-master-data-services.md)  
  
-   [Esportazione di dati &#40;Master Data Services&#41;](overview-exporting-data-master-data-services.md)  
  
  
