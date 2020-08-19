---
description: Cursori misti
title: Cursori misti | Microsoft Docs
ms.custom: ''
ms.date: 01/20/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- mixed cursors [ODBC]
- cursors [ODBC], dynamic
- keyset-driven cursors [ODBC]
- dynamic cursors [ODBC]
- cursors [ODBC], key-set driven
- cursors [ODBC], mixed
ms.assetid: 9beb2db9-0b6d-491d-9529-d64e64e59014
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5b15aaee9d74319daa1a211610ce283d247fda2e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88424603"
---
# <a name="mixed-cursors"></a>Cursori misti

Un cursore misto è una combinazione di un cursore gestito da keyset e di un cursore dinamico. Viene utilizzato quando il set di risultati è troppo grande per risparmiare ragionevolmente le chiavi per l'intero set di risultati. I cursori misti vengono implementati creando un keyset più piccolo dell'intero set di risultati, ma maggiore del set di righe.  
  
 A condizione che l'applicazione scorra all'interno del keyset, il comportamento è gestito da keyset. Quando l'applicazione scorre all'esterno del keyset, il comportamento è dinamico: il cursore Recupera le righe richieste e crea un nuovo keyset. Dopo la creazione del nuovo keyset, il comportamento viene ripristinato in base a keyset all'interno di tale keyset.  
  
 Si supponga, ad esempio, che un set di risultati includa 1.000 righe e usi un cursore misto con una dimensione di keyset di 100 e una dimensione del set di righe pari a 10. Quando viene recuperato il primo set di righe, il cursore crea un keyset costituito dalle chiavi per le prime 100 righe. Restituisce quindi le prime 10 righe, come richiesto.  
  
 Si supponga ora che un'altra applicazione elimini le righe 11 e 101. Se il cursore tenta di recuperare la riga 11, si verificherà un gap perché contiene una chiave per questa riga, ma non esiste alcuna riga; si tratta di un comportamento gestito da keyset. Se il cursore tenta di recuperare la riga 101, il cursore non rileva che la riga è mancante perché non contiene una chiave per la riga. Verrà invece recuperato il risultato della riga precedente 102. Si tratta di un comportamento dinamico del cursore.  
  
 Un cursore misto è equivalente a un cursore gestito da keyset quando la dimensione del keyset è uguale alla dimensione del set di risultati. Un cursore misto è equivalente a un cursore dinamico quando la dimensione del keyset è pari a 1.
