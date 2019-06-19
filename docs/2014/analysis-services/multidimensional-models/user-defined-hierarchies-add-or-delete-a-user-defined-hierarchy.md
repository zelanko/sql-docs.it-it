---
title: Aggiungere o eliminare una gerarchia definita dall'utente | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- hierarchies [Analysis Services], adding
- removing hierarchies
- adding hierarchies
- deleting hierarchies
- hierarchies [Analysis Services], removing
ms.assetid: 953818b4-9543-4c01-bb20-1d45ec6dfb91
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 14d63345020fbe76b727d9276585b17bb3406846
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66072585"
---
# <a name="add-or-delete-a-user-defined-hierarchy"></a>Aggiungere o eliminare una gerarchia definita dall'utente
  È possibile aggiungere o rimuovere una gerarchia definita dall'utente in una dimensione nella scheda **Struttura dimensione** di Progettazione dimensioni in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
 Quando si aggiunge una gerarchia definita dall'utente, questa non risulta disponibile per gli utenti finché non ne viene creata un'istanza in un'istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] e non viene elaborata la dimensione. Per altre informazioni, vedere [database modelli multidimensionali &#40;SSAS&#41; ](multidimensional-model-databases-ssas.md) e [l'elaborazione di oggetti modello multidimensionale](processing-a-multidimensional-model-analysis-services.md).  
  
### <a name="to-add-a-user-defined-hierarchy-to-a-dimension"></a>Per aggiungere una gerarchia definita dall'utente a una dimensione  
  
1.  In [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]aprire il progetto appropriato di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , quindi aprire la dimensione che si desidera utilizzare.  
  
     La dimensione viene aperta nella scheda **Struttura dimensione** di Progettazione dimensioni.  
  
2.  Trascinare l'attributo che si vuole usare nella gerarchia definita dall'utente dal riquadro **Attributi** al riquadro **Gerarchie** .  
  
3.  Trascinare ulteriori attributi per formare i livelli della gerarchia definita dall'utente.  
  
     L'ordine nel quale sono elencati gli attributi è determinante. Ad esempio, in una gerarchia temporale, gli anni devono essere visualizzati più in alto dei giorni nell'elenco della gerarchia.  
  
4.  Facoltativamente, riorganizzare i livelli della gerarchia definita dall'utente trascinandoli nelle posizioni corrette.  
  
5.  Facoltativamente, modificare le proprietà della gerarchia definita dall'utente o dei relativi livelli.  
  
     Può essere ad esempio utile specificare un nome per la gerarchia definita dall'utente, rinominarne uno o più livelli e definire un nome personalizzato per il livello Totale. Per altre informazioni, vedere [proprietà della gerarchia utente](../multidimensional-models-olap-logical-dimension-objects/user-hierarchies-properties.md), e [proprietà a livello di &#91;preparazione su&#93;](../multidimensional-models-olap-logical-dimension-objects/user-hierarchies-level-properties.md).  
  
    > [!NOTE]  
    >  Per impostazione predefinita, una gerarchia definita dall'utente è solo un percorso che consente agli utenti di eseguire il drill-down delle informazioni. Se esistono relazioni tra i livelli, tuttavia, è possibile incrementare le prestazioni di esecuzione delle query configurando relazioni tra attributi per i livelli. Per altre informazioni, vedere [Relazioni tra attributi](../multidimensional-models-olap-logical-dimension-objects/attribute-relationships.md) e [Definire relazioni tra attributi](attribute-relationships-define.md).  
  
### <a name="to-remove-a-user-defined-hierarchy-from-a-dimension"></a>Per rimuovere una gerarchia definita dall'utente da una dimensione  
  
-   Nella scheda **Struttura dimensione** fare clic sulla gerarchia definita dall'utente che si vuole rimuovere nel riquadro **Gerarchie** . Fare clic su **Elimina**sulla barra degli strumenti.  
  
     - \- oppure -  
  
-   Fare clic con il pulsante destro del mouse sulla gerarchia definita dall'utente che si vuole rimuovere nel riquadro **Gerarchie** e quindi scegliere **Elimina**.  
  
     - \- oppure -  
  
-   Trascinare la gerarchia definita dall'utente al di fuori dell'area di progettazione.  
  
## <a name="see-also"></a>Vedere anche  
 [Gerarchie definite dall'utente](../multidimensional-models-olap-logical-dimension-objects/user-hierarchies.md)   
 [Creare gerarchie definite dall'utente](user-defined-hierarchies-create.md)  
  
  
