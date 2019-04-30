---
title: Inserimento, aggiornamento ed eliminazione di membri (XMLA) | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 3a409e21e925b3912aee5ec751747f61bce05276
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63138583"
---
# <a name="inserting-updating-and-dropping-members-xmla"></a>Inserimento, aggiornamento ed eliminazione di membri (XMLA)
  È possibile usare la [inserire](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/insert-element-xmla), [aggiornare](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/update-element-xmla), e [Drop](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/drop-element-xmla) comandi XML for Analysis (XMLA) consentono rispettivamente di inserire, aggiornare o eliminare membri da una dimensione abilitata per la scrittura. Per altre informazioni sulle dimensioni abilitate per la scrittura, vedere [dimensioni abilitate per la scrittura](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/write-enabled-dimensions.md).  
  
## <a name="inserting-new-members"></a>Inserimento di nuovi membri  
 Il **Inserisci** comando inserisce i nuovi membri in attributi specificati in una dimensione abilitata per la scrittura.  
  
 Prima di costruire il **Inserisci** comando, è necessario disponibili per i nuovi membri da inserire le informazioni seguenti:  
  
-   Dimensione in cui inserire i nuovi membri.  
  
-   Attributo della dimensione in cui inserire i nuovi membri.  
  
-   Nomi dei nuovi membri, inclusa qualsiasi conversione applicabile per il nome.  
  
-   Chiavi dei nuovi membri. Se un attributo utilizza una chiave composta, per la chiave può essere necessario utilizzare più valori.  
  
-   Valori per tutte le proprietà dell'attributo applicabili non implementate come altri attributi nella dimensione. Tali proprietà includono operazioni unarie, conversioni, rollup personalizzati e relative proprietà e livelli ignorati.  
  
 Il **Inserisci** comando accetta solo due proprietà:  
  
-   Il [oggetto](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/object-element-xmla) proprietà, che contiene un riferimento all'oggetto per la dimensione in cui devono essere inseriti i membri. Il riferimento all'oggetto contiene l'identificatore di database, l'identificatore di cubo e l'identificatore di dimensione per la dimensione.  
  
-   Il [attributi](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/attributes-element-xmla) proprietà, che contiene uno o più [attributo](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/attribute-element-xmla) elementi per identificare gli attributi in cui devono essere inseriti i membri. Ciascuna **attributo** elemento identifica un attributo e fornisce il nome, valore, traduzioni, operatore unario, personalizzate di rollup, proprietà di rollup personalizzato e i livelli ignorati per un singolo membro da aggiungere all'attributo identificato.  
  
    > [!NOTE]  
    >  Tutte le proprietà per il **attributo** elemento deve essere incluso. In caso contrario, è possibile che si verifichi un errore.  
  
## <a name="updating-existing-members"></a>Aggiornamento di membri esistenti  
 Il **Update** comando Aggiorna i membri esistenti in attributi specificati, in base alle relazioni con altri membri in altri attributi in una dimensione abilitata per la scrittura. Il **Update** comando è possibile spostare membri in altri livelli nelle gerarchie contenuti nella dimensione e possono essere utilizzati per ristrutturare gerarchie padre-figlio definite dagli attributi padre.  
  
 Prima di costruire il **Update** comando, è necessario disponibili per i membri da aggiornare le informazioni seguenti:  
  
-   Dimensione in cui aggiornare i membri esistenti.  
  
-   Attributi della dimensione in cui aggiornare i membri esistenti.  
  
-   Chiavi dei membri esistenti. Se un attributo utilizza una chiave composta, per la chiave può essere necessario utilizzare più valori.  
  
-   Valori per tutte le proprietà dell'attributo applicabili non implementate come altri attributi nella dimensione. Tali proprietà includono operazioni unarie, conversioni, rollup personalizzati e relative proprietà e livelli ignorati.  
  
 Il **Update** comando accetta solo tre proprietà obbligatorie:  
  
-   Il **oggetto** proprietà, che contiene un riferimento all'oggetto per la dimensione in cui i membri devono essere aggiornati. Il riferimento all'oggetto contiene l'identificatore di database, l'identificatore di cubo e l'identificatore di dimensione per la dimensione.  
  
-   Il **attributi** proprietà, che contiene uno o più **attributo** elementi per identificare gli attributi in cui devono essere aggiornati i membri. Il **attributo** elemento identifica un attributo e fornisce il nome, valore, traduzioni, operatore unario, personalizzate di rollup, proprietà di rollup personalizzato e i livelli ignorati per un singolo membro da aggiornare per l'attributo identificato.  
  
    > [!NOTE]  
    >  Tutte le proprietà per il **attributo** elemento deve essere incluso. In caso contrario, è possibile che si verifichi un errore.  
  
-   Il [in cui](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/where-element-xmla) proprietà, che contiene uno o più **attributo** gli elementi che vincolano gli attributi in cui devono essere aggiornati i membri. Il **in cui** proprietà è fondamentale per limitare un' **Update** per istanze specifiche di un membro. Se il **in cui** proprietà non è specificata, vengono aggiornate tutte le istanze di un membro specifico. Si supponga ad esempio che siano presenti tre clienti per cui si desidera modificare il nome di città da Redmond in Bellevue. Per modificare il nome della città, è necessario specificare una **in cui** proprietà che identifica il cliente i tre membri dell'attributo per cui devono essere modificati i membri dell'attributo City. Se non si specifica questo **in cui** proprietà di ogni cliente il cui nome di città è attualmente Redmond avrebbe il nome di città Bellevue dopo le **Update** comando esegue.  
  
    > [!NOTE]  
    >  Fatta eccezione per i nuovi membri, il **aggiornare** comando è possibile aggiornare solo valori di chiave di attributo per gli attributi non inclusi nel **in cui** clausola. Quando ad esempio viene aggiornato un cliente, il relativo nome di città non può essere aggiornato. In caso contrario, il nome di città viene modificato per tutti i clienti.  
  
### <a name="updating-members-in-parent-attributes"></a>Aggiornamento di membri in attributi padre  
 Per supportare gli attributi padre, il **Update** comando facoltativo [MoveWithDescendants](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/movewithdescendants-element-xmla)utilizza le proprietà. Impostando il **MoveWithDescendants** proprietà su true indica che i discendenti del membro padre inoltre devono essere spostati con il membro padre quando cambia l'identificatore di tale membro padre. Se questo valore è impostato su false, lo spostamento di un membro padre comporta la promozione dei relativi discendenti immediati al livello in cui il membro padre si trovava in precedenza.  
  
 Quando si aggiornano i membri di un attributo padre, il **aggiornare** comando non è possibile aggiornare i membri di altri attributi.  
  
## <a name="dropping-existing-members"></a>Eliminazione di membri esistenti  
 Prima di costruire il **Drop** comando, è necessario disponibili per i membri che si desidera eliminare le informazioni seguenti:  
  
-   Dimensione in cui eliminare i membri esistenti.  
  
-   Attributi della dimensione in cui eliminare i membri esistenti.  
  
-   Chiavi dei membri esistenti da eliminare. Se un attributo utilizza una chiave composta, per la chiave può essere necessario utilizzare più valori.  
  
 Il **Drop** comando accetta solo due proprietà obbligatorie:  
  
-   Il **oggetto** proprietà, che contiene un riferimento all'oggetto per la dimensione in cui devono essere eliminati i membri. Il riferimento all'oggetto contiene l'identificatore di database, l'identificatore di cubo e l'identificatore di dimensione per la dimensione.  
  
-   Il **in cui** proprietà, che contiene uno o più **attributo** elementi per limitare gli attributi in cui i membri devono essere eliminati. Il **in cui** proprietà è fondamentale per limitare un **Drop** per istanze specifiche di un membro. Se il **in cui** comando non è specificato, vengono eliminate tutte le istanze di un membro specifico. Si supponga ad esempio che siano presenti tre clienti che si desidera eliminare da Redmond. Per eliminare tali clienti, è necessario specificare una **in cui** proprietà che identifica il membro Redmond dell'attributo City da cui devono essere rimossi i tre clienti e i tre membri dell'attributo Customer da rimuovere. Se il **in cui** proprietà specifica solo il membro Redmond dell'attributo City, ogni cliente associato a Redmond verrebbe eliminato dalle **Drop** comando. Se il **in cui** proprietà specifica solo i tre membri dell'attributo Customer, i tre clienti verrebbero eliminati completamente dalle **Drop** comando.  
  
    > [!NOTE]  
    >  Il **attributo** gli elementi inclusi in un **Drop** comando deve contenere solo il **AttributeName** e **chiavi** proprietà. In caso contrario, è possibile che si verifichi un errore.  
  
### <a name="dropping-members-in-parent-attributes"></a>Eliminazione di membri in attributi padre  
 Impostando il [DeleteWithDescendants](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/deletewithdescendants-element-xmla) proprietà indica che i discendenti del membro padre devono essere eliminati anche con il membro padre. Se questo valore è impostato su false, i discendenti immediati del membro padre vengono invece promossi al livello in cui il membro padre si trovava in precedenza.  
  
> [!IMPORTANT]  
>  Per eliminare sia il membro padre che i relativi discendenti, è sufficiente che un utente disponga delle autorizzazioni per l'eliminazione del solo membro padre e non è necessario che disponga delle autorizzazioni per l'eliminazione dei discendenti.  
  
## <a name="see-also"></a>Vedere anche  
 [Elemento DROP &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/drop-element-xmla)   
 [Inserire l'elemento &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/insert-element-xmla)   
 [Aggiornare l'elemento &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/update-element-xmla)   
 [Definizione e identificazione di oggetti &#40;XMLA&#41;](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/defining-and-identifying-objects-xmla.md)   
 [Sviluppo con XMLA in Analysis Services](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/developing-with-xmla-in-analysis-services.md)  
  
  
