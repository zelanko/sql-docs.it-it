---
title: Scheda set di elementi (Visualizzatore modello di data mining) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.dm.miningmodeleditor.associationrules.itemsets.f1
ms.assetid: 95b2b805-b142-4064-9c80-4b1b3fe2fe63
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: b34031f0554fd9743ba036c9ce0f1bebe2c3d44d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66079554"
---
# <a name="itemsets-tab-mining-model-viewer"></a>Scheda Set di elementi (Visualizzatore modello di data mining)
  È possibile usare il riquadro **Set di elementi** per visualizzare i set di elementi frequenti inclusi in un modello di data mining delle regole di associazione. Poiché in un modello di associazione possono essere inclusi molti set di elementi, i controlli vengono forniti nel visualizzatore come supporto per filtrare i set di elementi mostrati nel visualizzatore.  
  
 **Per altre informazioni:** [algoritmo Microsoft Association](data-mining/microsoft-association-algorithm.md), [visualizzare un modello usando il Visualizzatore Microsoft Association Rules](data-mining/browse-a-model-using-the-microsoft-association-rules-viewer.md)  
  
## <a name="options"></a>Opzioni  
 **Aggiorna contenuto visualizzatore**  
 Consente di ricaricare il modello di data mining nel visualizzatore.  
  
 **Modello di data mining**  
 Fare clic su un modello di data mining da visualizzare contenuto nella struttura di data mining corrente. Il modello di data mining verrà aperto nel visualizzatore associato.  
  
 **Visualizzatore**  
 Consente di scegliere un visualizzatore da utilizzare per la visualizzazione del modello di data mining selezionato. È possibile utilizzare il visualizzatore personalizzato per i modelli di associazione o [!INCLUDE[msCoName](../includes/msconame-md.md)] Generic Content Tree Viewer. Se disponibili, è anche possibile utilizzare i visualizzatori plug-in.  
  
 **Supporto minimo**  
 Modificare questo valore per impostare il supporto minimo che può essere contenuto in un set di elementi da visualizzare nel visualizzatore. Il valore predefinito visualizzato alla prima apertura del modello è calcolato dal modello, tuttavia è possibile modificarlo per vedere un numero maggiore o inferiore di set di elementi.  
  
 **Dimensioni minime set di elementi**  
 Modificare questo valore per impostare il numero minimo di elementi che devono essere inclusi in un set di elementi prima che quest'ultimo possa essere visualizzato nel visualizzatore.  
  
 **Filtra set di elementi**  
 Consente di digitare un valore stringa per filtrare il numero di set di elementi da mostrare nel visualizzatore.  
  
 È anche possibile digitare espressioni regolari .NET come criteri di filtro. Ad esempio, tramite l'espressione seguente vengono restituiti tutti i set di elementi contenenti 'Road Bottle Cage':  
  
 `\bRoad\b.\bBottle\b.\bCage\b.*`  
  
 Si noti che potrebbe essere necessario aggiornare la vista per visualizzare l'applicazione dei criteri di filtro. È anche possibile attivare e disattivare l'opzione **Mostra nomi lunghi** per aggiornare l'elenco.  
  
 Per impostazione predefinita, i criteri di filtro si applicano alla combinazione nome e cognome dell'attributo-valore; pertanto, se viene visualizzato solo il nome dell'attributo, è probabile che i criteri di filtro non siano stati applicati correttamente. Usare l'elenco a discesa **Mostra** per selezionare **Mostra nome e valore dell'attributo**, quindi verificare che l'elenco di set di elementi sia filtrato correttamente.  
  
 **Mostra**  
 Consente di impostare la modalità di visualizzazione del set di elementi nel visualizzatore. È possibile selezionare una delle tre opzioni seguenti:  
  
-   Mostra nome e valore dell'attributo  
  
-   Mostra solo il valore dell'attributo  
  
-   Mostra solo il nome dell'attributo  
  
 Si noti che questa opzione non consente di eseguire nuovamente una query sul modello, ma solo di filtrare gli attributi o i valori visualizzati.  
  
 **Mostra nomi lunghi**  
 Selezionare questa opzione per visualizzare il nome completo del set di elementi come viene visualizzato nel contenuto del modello di data mining.  
  
 **Righe massime**  
 Consente di impostare il limite del numero di set di elementi che è possibile visualizzare. Per impostazione predefinita, i set di elementi vengono ordinati per supporto in modo decrescente, pertanto abbassando questo valore, l'elenco viene limitato ai set di elementi più comuni.  
  
 **Supporto**  
 Consente di visualizzare il supporto per ogni set di elementi.  
  
 **Dimensione**  
 Consente di visualizzare il numero di elementi esistenti in ogni set.  
  
 **Set**  
 Consente di visualizzare la descrizione di ogni set di elementi. Per impostazione predefinita, i set di elementi vengono presentati come un elenco delimitato da virgole di attributi e dei relativi valori. È possibile modificare la modalità di visualizzazione tramite l'opzione **Mostra** .  
  
## <a name="see-also"></a>Vedere anche  
 [Algoritmi di data mining &#40;Analysis Services-&#41;di data mining](data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [Visualizzatori modello di data mining &#40;Progettazione modelli di data mining&#41;](mining-model-viewers-data-mining-model-designer.md)   
 [Visualizzatori modello di data mining](data-mining/data-mining-model-viewers.md)  
  
  
