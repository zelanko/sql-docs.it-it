---
title: Posizionamento del recordset | Microsoft Docs
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
ms.openlocfilehash: cdce4c7b08a8b15cdb0a9ee1111a216aeef005bf
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "67924437"
---
# <a name="recordset-positioning"></a>Posizionamento nei recordset
Utilizzare la proprietà **AbsolutePosition** per spostarsi in un record, in base alla relativa posizione ordinale nell'oggetto **Recordset** , oppure per determinare la posizione ordinale del record corrente. Il provider deve supportare la funzionalità appropriata affinché questa proprietà sia disponibile.  
  
 **AbsolutePosition** è in base 1 e è uguale a 1 quando il record corrente è il primo record nel **Recordset**. Come indicato in precedenza, è possibile ottenere il numero totale di record nell'oggetto **Recordset** dalla proprietà **RecordCount** .  
  
 Quando si imposta la proprietà **AbsolutePosition** , anche se si tratta di un record nella cache corrente, ADO ricarica la cache con un nuovo gruppo di record a partire dal record specificato. La proprietà **CacheSize** determina le dimensioni di questo gruppo.  
  
> [!NOTE]
>  Non usare la proprietà **AbsolutePosition** come numero di record surrogato. La posizione di un determinato record viene modificata quando si elimina un record precedente. Non esiste inoltre alcuna garanzia che un determinato record avrà lo stesso **AbsolutePosition** se l'oggetto **Recordset** viene nuovamente sottoposto a query o riaperto. I segnalibri rappresentano il metodo consigliato per mantenere e tornare a una posizione specificata e sono l'unico modo per posizionare tutti i tipi di oggetti **Recordset** .
