---
title: Editor trasformazione Raggruppamento fuzzy (scheda colonne) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.fuzzygroupingtransformation.columns.f1
helpviewer_keywords:
- Fuzzy Grouping Transformation Editor
ms.assetid: 24f4539f-2a9f-4acd-acc7-06228a07f7df
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: dc69475a26bde2045c06429462b5de306c4f932f
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62893246"
---
# <a name="fuzzy-grouping-transformation-editor-columns-tab"></a>Editor trasformazione Raggruppamento fuzzy (scheda Colonne)
  Utilizzare la scheda **Colonne** della finestra di dialogo **Editor trasformazione Raggruppamento fuzzy** per specificare le colonne utilizzate per raggruppare le righe contenenti valori duplicati  
  
 Per ulteriori informazioni sulla trasformazione Raggruppamento fuzzy, vedere [Fuzzy Grouping Transformation](data-flow/transformations/fuzzy-grouping-transformation.md).  
  
## <a name="options"></a>Opzioni  
 **Colonne di input disponibili**  
 Consente di selezionare le colonne di input utilizzate per raggruppare le righe contenenti valori duplicati.  
  
 **Name**  
 Consente di visualizzare i nomi delle colonne di input disponibili.  
  
 **Pass-through**  
 Consente di includere la colonna di input nell'output della trasformazione. Tutte le colonne utilizzate per il raggruppamento vengono copiate automaticamente nell'output. Selezionando questa colonna è possibile includere colonne aggiuntive.  
  
 **Colonna di input**  
 Consente di selezionare una delle colonne di input selezionate precedentemente nell'elenco **Colonne di input disponibili** .  
  
 **Alias di output**  
 Consente di immettere un nome descrittivo per la colonna di output corrispondente. Per impostazione predefinita, il nome della colonna di output corrisponde al nome della colonna di input.  
  
 **Alias di output gruppo**  
 Consente di immettere un nome descrittivo per la colonna che conterrà il valore canonico per i duplicati raggruppati. Il nome predefinito di questa colonna di output è il nome della colonna di input con l'aggiunta di _clean.  
  
 **Tipo di corrispondenza**  
 Consente di selezionare la corrispondenza fuzzy o esatta. Le righe vengono considerate duplicati se sono sufficientemente simili in tutte le colonne della corrispondenza fuzzy. Se inoltre si specifica la corrispondenza esatta su determinate colonne, vengono considerati possibili duplicati solo le righe contenenti valori identici nelle colonne della corrispondenza esatta. Se si sa pertanto che una determinata colonna non contiene errori o inconsistenze, è possibile specificare la corrispondenza esatta su tale colonna per aumentare la precisione della corrispondenza fuzzy su altre colonne.  
  
 **Somiglianza minima**  
 Consente di impostare la soglia di somiglianza minima a livello di join tramite un dispositivo di scorrimento. Più il valore è vicino a 1, maggiore deve essere la somiglianza tra il valore di ricerca e il valore di origine per essere considerata una corrispondenza. L'aumento della soglia può migliorare la velocità di confronto, poiché verrà considerato un numero minore di record candidati.  
  
 **Alias di output somiglianza**  
 Consente di specificare il nome di una nuova colonna di output contenente i punteggi di somiglianza per il join selezionato. Se non si specifica un valore, la colonna di output non viene creata.  
  
 **Numerali**  
 Consente di specificare l'importanza dei numerali iniziali e finali nel confronto dei dati della colonna. Ad esempio, se i numerali iniziali sono significativi, "2005 Vendite" non verrà raggruppato con "2004 Vendite".  
  
|Value|Descrizione|  
|-----------|-----------------|  
|**Nessuno**|I numerali iniziali e finali non sono significativi.|  
|**Iniziali**|Sono significativi solo i numerali iniziali.|  
|**Finali**|Sono significativi solo i numerali finali.|  
|**Iniziali e finali**|Sono significativi i numerali sia iniziali che finali.|  
  
 **Flag di confronto**  
 Per altre informazioni sulle opzioni per il confronto di stringhe, vedere [Confronto di dati stringa](data-flow/comparing-string-data.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento ai messaggi e agli errori di Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Identificazione di righe di dati simili tramite la trasformazione Raggruppamento fuzzy](data-flow/transformations/identify-similar-data-rows-by-using-the-fuzzy-grouping-transformation.md)  
  
  
