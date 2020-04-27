---
title: Implementazione della compressione di pagina | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- page compression [Database Engine]
- compression [SQL Server], page
ms.assetid: 78c83277-1dbb-4e07-95bd-47b14d2b5cd4
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 65777f25066cfb42093313b90ac198c6bc1796a6
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "62918219"
---
# <a name="page-compression-implementation"></a>Implementazione della compressione di pagina
  Questo argomento offre un riepilogo delle modalità di implementazione della compressione di pagina nel [!INCLUDE[ssDE](../../includes/ssde-md.md)] . Tale riepilogo fornisce informazioni di base che consentono di pianificare lo spazio di archiviazione necessario per i dati.  
  
 La compressione di pagina è simile per tabelle e indici e relative partizioni. La descrizione seguente della compressione di pagina per una tabella si applica in modo analogo alla compressione di pagina per tutti i tipi di oggetto. Negli esempi seguenti vengono compresse stringhe di caratteri, ma sia la compressione basata su prefisso che quella basata su dizionario applicano gli stessi principi agli altri tipi di dati.  
  
 La compressione del livello foglia di tabelle e indici con compressione di pagina è costituita da tre operazioni eseguite nell'ordine seguente:  
  
1.  Compressione di riga  
  
2.  Compressione basata su prefisso  
  
3.  Compressione basata su dizionario  
  
 Quando si usa la compressione di pagina, per le pagine di indici che non si trovano a livello foglia viene usata solo la compressione di riga. Per altre informazioni sulla compressione di riga, vedere [Implementazione della compressione di riga](../data-compression/row-compression-implementation.md).  
  
## <a name="prefix-compression"></a>Compressione basata su prefisso  
 Per ogni pagina da comprimere, la compressione basata su prefisso viene eseguita mediante i passaggi seguenti:  
  
1.  Per ogni colonna, viene identificato un valore che può essere utilizzato per ridurre lo spazio di archiviazione per i valori della colonna.  
  
2.  Viene creata una riga che rappresenta i valori del prefisso per ogni colonna. Tale riga viene archiviata nella struttura delle informazioni di compressione immediatamente seguente all'intestazione della pagina.  
  
3.  I valori del prefisso ripetuti nella colonna vengono sostituiti da un riferimento al prefisso corrispondente. Se il valore in una riga non corrisponde esattamente al valore del prefisso selezionato, è possibile indicare ancora una corrispondenza parziale.  
  
 Nell'illustrazione seguente viene mostrata una pagina di esempio di una tabella prima della compressione basata su prefisso.  
  
 ![Pagina prima della compressione basata su prefisso](../media/skt-tblcompression1c.gif "Pagina prima della compressione basata su prefisso")  
  
 Nell'illustrazione seguente viene mostrata la stessa pagina di esempio dopo la compressione basata su prefisso. Il prefisso viene spostato nell'intestazione e i valori della colonna vengono impostati sui riferimenti al prefisso.  
  
 ![Pagina dopo la compressione basata su prefisso](../media/tblcompression2.gif "Pagina dopo la compressione basata su prefisso")  
  
 Nella prima colonna della prima riga, il valore 4b indica che i primi quattro caratteri del prefisso (aaab) sono presenti per tale riga, così come il carattere b. Il valore risultante è aaabb, ovvero il valore originale.  
  
## <a name="dictionary-compression"></a>Compressione basata su dizionario  
 Dopo che la compressione basata su prefisso è stata completata, viene applicata quella basata su dizionario. In base a tale compressione, viene eseguita la ricerca di valori ripetuti in qualsiasi punto della pagina che successivamente vengono archiviati nell'area relativa alla struttura delle informazioni di compressione. A differenza di quella basata su prefisso, la compressione basata su dizionario non è limitata a una colonna e può sostituire valori ripetuti presenti in qualsiasi punto di una pagina. Nell'illustrazione seguente viene mostrata la stessa pagina di esempio dopo la compressione basata su dizionario.  
  
 ![Pagina dopo la compressione basata su dizionario](../media/tblcompression3.gif "Pagina dopo la compressione basata su dizionario")  
  
 Notare che al valore 4b viene fatto riferimento da colonne diverse della pagina.  
  
## <a name="when-page-compression-occurs"></a>Esecuzione della compressione di pagina  
 Quando si crea una nuova tabella con compressione di pagina, non viene eseguita alcuna compressione. I metadati per la tabella indicano tuttavia la compressione di pagina da utilizzare. Man mano che i dati vengono aggiunti alla prima pagina di dati, viene applicata la compressione di riga. Poiché la pagina non è completa, la compressione di pagina non consente di ottenere alcun beneficio. Quando la pagina è completa, la successiva riga da aggiungere avvia l'operazione di compressione di pagina. La pagina intera viene rivista, ogni colonna viene valutata per la compressione basata su prefisso, quindi tutte le colonne vengono valutate per eseguire la compressione basata su dizionario. Se la compressione di pagina ha creato spazio sufficiente per un'ulteriore riga, la riga viene aggiunta e ai dati viene applicata sia la compressione di riga che quella di pagina. Se lo spazio guadagnato in seguito alla compressione di pagina senza lo spazio necessario per la struttura delle informazioni di compressione non è significativo, la compressione di pagina non viene utilizzata. Le righe successive vengono inserite nella nuova pagina. Se lo spazio non è sufficiente, alla tabella viene aggiunta una nuova pagina. Analogamente alla prima pagina, alla nuova pagina non viene inizialmente applicata la compressione di pagina.  
  
 Quando una tabella esistente che contiene dati viene convertita in base alla compressione di pagina, ogni pagina viene ricompilata e valutata. La ricompilazione di tutte le pagine provoca la ricompilazione della tabella, dell'indice o della partizione.  
  
## <a name="see-also"></a>Vedere anche  
 [Compressione dei dati](data-compression.md)   
 [Implementazione della compressione di riga](row-compression-implementation.md)  
  
  
