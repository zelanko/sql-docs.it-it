---
title: Posizionamento dei recordset | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- record positioning [ADO]
- Recordset object [ADO]
- repositioning record [ADO]
- AbsolutePosition property [ADO]
ms.assetid: c8f6fbcb-6675-4133-b37e-430de43949c1
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: c01d24a5f92b4bca1e5b41a0cbece980237fd961
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66701675"
---
# <a name="recordset-positioning"></a>Posizionamento nei recordset
Usare la **esempio di AbsolutePosition** la posizione ordinale in base alle proprietà per passare a un record, il **Recordset** oggetto, o per determinare la posizione ordinale del record corrente. Il provider deve supportare le funzionalità appropriate per questa proprietà sia disponibile.  
  
 **Esempio di AbsolutePosition** è basato su 1 e uguale a 1 quando il record corrente è il primo record nel **Recordset**. Come accennato in precedenza, è possibile ottenere il numero totale di record nel **Recordset** dell'oggetto dalle **RecordCount** proprietà.  
  
 Quando si impostano i **esempio di AbsolutePosition** proprietà, anche se è in un record di cache corrente, ADO consente di ricaricare la cache con un nuovo gruppo di record che iniziano con il record è specificati. Il **CacheSize** proprietà determina la dimensione di questo gruppo.  
  
> [!NOTE]
>  È consigliabile non usare la **esempio di AbsolutePosition** proprietà come un numero di record di surrogati. La posizione di un determinato record viene modificato quando si elimina un record precedente. Non sono inoltre alcuna garanzia che un determinato record avrà lo stesso **esempio di AbsolutePosition** se il **Recordset** oggetto viene rieseguito o riaperto. I segnalibri sono lo strumento consigliato per mantenere e restituire dati in una posizione specificata e sono l'unico modo il posizionamento in tutti i tipi di **Recordset** oggetti.
