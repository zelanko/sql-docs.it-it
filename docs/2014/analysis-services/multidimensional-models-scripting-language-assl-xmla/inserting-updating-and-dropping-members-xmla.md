---
title: Inserimento, aggiornamento ed eliminazione di membri (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- inserting dimension members
- XML for Analysis, members
- removing dimension members
- dropping dimension members
- write-enabled dimensions [Analysis Services]
- XMLA, members
- deleting dimension members
- dimensions [Analysis Services], XML for Analysis
ms.assetid: bba922b5-8b88-4051-9506-ff055248182a
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 98da3e0f7a9b61b178372d9b24b8b595ab6b6626
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62727165"
---
# <a name="inserting-updating-and-dropping-members-xmla"></a>Inserimento, aggiornamento ed eliminazione di membri (XMLA)
  È possibile usare la [inserire](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/insert-element-xmla), [aggiornare](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/update-element-xmla), e [Drop](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/drop-element-xmla) comandi XML for Analysis (XMLA) consentono rispettivamente di inserire, aggiornare o eliminare membri da una dimensione abilitata per la scrittura. Per altre informazioni sulle dimensioni abilitate per la scrittura, vedere [dimensioni abilitate per la scrittura](../multidimensional-models-olap-logical-dimension-objects/write-enabled-dimensions.md).  
  
## <a name="inserting-new-members"></a>Inserimento di nuovi membri  
 Il comando `Insert` consente di inserire nuovi membri in attributi specificati in una dimensione abilitata per la scrittura.  
  
 Prima di creare il comando `Insert`, è necessario che siano disponibili le seguenti informazioni relative ai nuovi membri da inserire:  
  
-   Dimensione in cui inserire i nuovi membri.  
  
-   Attributo della dimensione in cui inserire i nuovi membri.  
  
-   Nomi dei nuovi membri, inclusa qualsiasi conversione applicabile per il nome.  
  
-   Chiavi dei nuovi membri. Se un attributo utilizza una chiave composta, per la chiave può essere necessario utilizzare più valori.  
  
-   Valori per tutte le proprietà dell'attributo applicabili non implementate come altri attributi nella dimensione. Tali proprietà includono operazioni unarie, conversioni, rollup personalizzati e relative proprietà e livelli ignorati.  
  
 Il comando `Insert` accetta solo due proprietà:  
  
-   Il [oggetto](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/object-element-xmla) proprietà, che contiene un riferimento all'oggetto per la dimensione in cui devono essere inseriti i membri. Il riferimento all'oggetto contiene l'identificatore di database, l'identificatore di cubo e l'identificatore di dimensione per la dimensione.  
  
-   Il [attributi](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/attributes-element-xmla) proprietà, che contiene uno o più [attributo](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/attribute-element-xmla) elementi per identificare gli attributi in cui devono essere inseriti i membri. Ogni elemento `Attribute` identifica un attributo e fornisce il nome, il valore, le conversioni, l'operatore unario, il rollup personalizzato e le relative proprietà e i livelli ignorati per un singolo membro da aggiungere all'attributo identificato.  
  
    > [!NOTE]  
    >  Tutte le proprietà per l'elemento `Attribute` devono essere incluse. In caso contrario, è possibile che si verifichi un errore.  
  
## <a name="updating-existing-members"></a>Aggiornamento di membri esistenti  
 Il comando `Update` consente di aggiornare membri esistenti in attributi specificati in una dimensione abilitata per la scrittura in base a relazioni con altri membri in altri attributi. Il comando `Update` consente di spostare i membri in altri livelli delle gerarchie contenute nella dimensione e può essere utilizzato per ristrutturare gerarchie padre-figlio definite dagli attributi padre.  
  
 Prima di creare il comando `Update`, è necessario che siano disponibili le informazioni seguenti relative ai membri da aggiornare:  
  
-   Dimensione in cui aggiornare i membri esistenti.  
  
-   Attributi della dimensione in cui aggiornare i membri esistenti.  
  
-   Chiavi dei membri esistenti. Se un attributo utilizza una chiave composta, per la chiave può essere necessario utilizzare più valori.  
  
-   Valori per tutte le proprietà dell'attributo applicabili non implementate come altri attributi nella dimensione. Tali proprietà includono operazioni unarie, conversioni, rollup personalizzati e relative proprietà e livelli ignorati.  
  
 Il comando `Update` accetta solo tre proprietà obbligatorie:  
  
-   Proprietà `Object` che contiene un riferimento all'oggetto per la dimensione in cui devono essere aggiornati i membri. Il riferimento all'oggetto contiene l'identificatore di database, l'identificatore di cubo e l'identificatore di dimensione per la dimensione.  
  
-   Proprietà `Attributes` che contiene uno o più elementi `Attribute` per identificare gli attributi in cui devono essere aggiornati i membri. L'elemento `Attribute` identifica un attributo e fornisce il nome, il valore, le conversioni, l'operatore unario, il rollup personalizzato e le relative proprietà e i livelli ignorati per un singolo membro da aggiornare per l'attributo identificato.  
  
    > [!NOTE]  
    >  Tutte le proprietà per l'elemento `Attribute` devono essere incluse. In caso contrario, è possibile che si verifichi un errore.  
  
-   Il [in cui](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/where-element-xmla) proprietà, che contiene uno o più `Attribute` gli elementi che vincolano gli attributi in cui devono essere aggiornati i membri. La proprietà `Where` è di importanza fondamentale per limitare l'esecuzione di un comando `Update` su istanze specifiche di un membro. Se il `Where` proprietà non è specificata, vengono aggiornate tutte le istanze di un membro specifico. Si supponga ad esempio che siano presenti tre clienti per cui si desidera modificare il nome di città da Redmond in Bellevue. Per modificare il nome di città, è necessario specificare una proprietà `Where` che identifichi i tre membri dell'attributo Customer per cui è necessario modificare i membri dell'attributo City. Se non si specifica la proprietà `Where`, dopo l'esecuzione del comando `Update` a ogni cliente il cui nome di città è attualmente Redmond risulterebbe associato il nome di città Bellevue.  
  
    > [!NOTE]  
    >  Ad eccezione dei nuovi membri, il comando `Update` consente di aggiornare solo i valori di chiave dell'attributo per attributi non inclusi nella clausola `Where`. Quando ad esempio viene aggiornato un cliente, il relativo nome di città non può essere aggiornato. In caso contrario, il nome di città viene modificato per tutti i clienti.  
  
### <a name="updating-members-in-parent-attributes"></a>Aggiornamento di membri in attributi padre  
 Per supportare gli attributi padre, il `Update` comando facoltativo [MoveWithDescendants](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/movewithdescendants-element-xmla)utilizza le proprietà. L'impostazione della proprietà `MoveWithDescendants` su true indica che lo spostamento del membro padre comporta lo spostamento dei relativi discendenti quando l'identificatore di tale membro padre viene modificato. Se questo valore è impostato su false, lo spostamento di un membro padre comporta la promozione dei relativi discendenti immediati al livello in cui il membro padre si trovava in precedenza.  
  
 Durante l'aggiornamento dei membri di un attributo padre, il comando `Update` non può aggiornare membri di altri attributi.  
  
## <a name="dropping-existing-members"></a>Eliminazione di membri esistenti  
 Prima di creare il comando `Drop`, è necessario che siano disponibili le informazioni seguenti relative ai nuovi membri da eliminare:  
  
-   Dimensione in cui eliminare i membri esistenti.  
  
-   Attributi della dimensione in cui eliminare i membri esistenti.  
  
-   Chiavi dei membri esistenti da eliminare. Se un attributo utilizza una chiave composta, per la chiave può essere necessario utilizzare più valori.  
  
 Il comando `Drop` accetta solo due proprietà obbligatorie:  
  
-   Proprietà `Object` che contiene un riferimento all'oggetto per la dimensione in cui devono essere eliminati i membri. Il riferimento all'oggetto contiene l'identificatore di database, l'identificatore di cubo e l'identificatore di dimensione per la dimensione.  
  
-   Proprietà `Where` che contiene uno o più elementi `Attribute` per applicare un vincolo agli attributi in cui devono essere eliminati i membri. La proprietà `Where` è di importanza fondamentale per limitare l'esecuzione di un comando `Drop` su istanze specifiche di un membro. Se la proprietà `Where` non è specificata, tutte le istanze di un membro specifico vengono eliminate. Si supponga ad esempio che siano presenti tre clienti che si desidera eliminare da Redmond. Per eliminare tali clienti, è necessario specificare una proprietà `Where` che identifichi i tre membri dell'attributo Customer da rimuovere e il membro Redmond dell'attributo City da cui i tre clienti devono essere rimossi. Se la proprietà `Where` specifica solo il membro Redmond dell'attributo City, ogni cliente associato a Redmond verrebbe eliminato dal comando `Drop`. Se la proprietà `Where` specifica solo i tre membri dell'attributo Customer, i tre clienti verrebbero completamente eliminati dal comando `Drop`.  
  
    > [!NOTE]  
    >  Gli elementi `Attribute` inclusi in un comando `Drop` devono contenere solo le proprietà `AttributeName` e `Keys`. In caso contrario, è possibile che si verifichi un errore.  
  
### <a name="dropping-members-in-parent-attributes"></a>Eliminazione di membri in attributi padre  
 Impostando il [DeleteWithDescendants](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/deletewithdescendants-element-xmla) proprietà indica che i discendenti del membro padre devono essere eliminati anche con il membro padre. Se questo valore è impostato su false, i discendenti immediati del membro padre vengono invece promossi al livello in cui il membro padre si trovava in precedenza.  
  
> [!IMPORTANT]  
>  Per eliminare sia il membro padre che i relativi discendenti, è sufficiente che un utente disponga delle autorizzazioni per l'eliminazione del solo membro padre e non è necessario che disponga delle autorizzazioni per l'eliminazione dei discendenti.  
  
## <a name="see-also"></a>Vedere anche  
 [Elemento DROP &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/drop-element-xmla)   
 [Inserire l'elemento &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/insert-element-xmla)   
 [Aggiornare l'elemento &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/update-element-xmla)   
 [Definizione e identificazione di oggetti &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-objects)   
 [Sviluppo con XMLA in Analysis Services](developing-with-xmla-in-analysis-services.md)  
  
  
