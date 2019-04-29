---
title: Editor trasformazione Raggruppamento fuzzy (scheda Avanzate) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.fuzzygroupingtransformation.advanced.f1
helpviewer_keywords:
- Fuzzy Grouping Transformation Editor
ms.assetid: dd820d75-b8a7-4515-aea4-3553ba5b442e
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 074a3d460a04180a5cfce1406b546fb6a3a3986a
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62893387"
---
# <a name="fuzzy-grouping-transformation-editor-advanced-tab"></a>Editor trasformazione Raggruppamento fuzzy (scheda Avanzate)
  La scheda **Avanzate** della finestra di dialogo **Editor trasformazione Raggruppamento fuzzy** consente di specificare le colonne di input e output, impostare le soglie di somiglianza e definire i delimitatori.  
  
> [!NOTE]  
>  Il `Exhaustive` e il `MaxMemoryUsage` le proprietà della trasformazione Raggruppamento Fuzzy non sono disponibili nel **Editor trasformazione Raggruppamento Fuzzy**, ma può essere impostata usando i **Editor avanzato**. Per ulteriori informazioni su queste proprietà, vedere la sezione relativa alla trasformazione Raggruppamento fuzzy in [Transformation Custom Properties](data-flow/transformations/transformation-custom-properties.md).  
  
 Per ulteriori informazioni sulla trasformazione Raggruppamento fuzzy, vedere [Fuzzy Grouping Transformation](data-flow/transformations/fuzzy-grouping-transformation.md).  
  
## <a name="options"></a>Opzioni  
 **Nome colonna chiave di input**  
 Consente di specificare il nome di una colonna di output contenente l'identificatore univoco per ogni riga di input. La colonna `_key_in` contiene un valore che identifica in modo univoco ogni riga.  
  
 **Nome colonna chiave di output**  
 Consente di specificare il nome di una colonna di output contenente l'identificatore univoco per la riga canonica di un gruppo di righe duplicate. La colonna `_key_out` corrisponde al valore `_key_in` della riga di dati canonica.  
  
 **Nome colonna punteggio somiglianza**  
 Consente di specificare un nome per la colonna contenente il punteggio di somiglianza. Il punteggio di somiglianza è un valore compreso tra 0 e 1 che indica la somiglianza della riga di input alla riga canonica. I punteggi più prossimi a 1 indicano una corrispondenza maggiore.  
  
 **Soglia di somiglianza**  
 Consente di impostare la soglia di somiglianza mediante il dispositivo di scorrimento. Le soglie vicine a 1 indicano che le righe devono avere una somiglianza maggiore per poter essere considerate duplicati. L'aumento della soglia può incrementare la velocità di ricerca della corrispondenza in quanto viene considerato un minor numero di record candidati.  
  
 **Delimitatori token**  
 La trasformazione genera un set predefinito di delimitatori per la suddivisione in token dei dati. È tuttavia possibile aggiungere o rimuovere i delimitatori in base alle esigenze modificando l'elenco.  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento ai messaggi e agli errori di Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Identificazione di righe di dati simili tramite la trasformazione Raggruppamento fuzzy](data-flow/transformations/identify-similar-data-rows-by-using-the-fuzzy-grouping-transformation.md)  
  
  
