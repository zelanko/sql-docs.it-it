---
title: Tipi di cursori (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- cursors [ADO], types
ms.assetid: 7cc01544-e814-403b-bbfe-a2750bf921bd
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: db77de95e83e596a8a301fa65885ee640c742a71
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/28/2018
ms.locfileid: "52543557"
---
# <a name="types-of-cursors-ado"></a>Tipi di cursori (ADO)
Come regola generale, l'applicazione deve usare il cursore più semplice che fornisce l'accesso ai dati necessari. Ogni caratteristica di cursore aggiuntive oltre le nozioni di base (forward-only, sola lettura, statici, scorrimento, non memorizzato nel buffer) prevede un prezzo - nella memoria del client, il carico di rete o delle prestazioni. In molti casi, le opzioni di cursore predefinito generano un cursore più complesso rispetto a effettivamente necessaria per l'applicazione.  
  
 La scelta del tipo di cursore dipende dal modo in cui l'applicazione usa il set di risultati e anche diverse considerazioni di progettazione, tra cui la dimensione del set di risultati, la percentuale dei dati che possono essere usati, sensibilità alle modifiche dei dati e le prestazioni dell'applicazione requisiti.  
  
 In parole semplici, la scelta di cursore dipende dalla necessità di modificare o semplicemente visualizzarne i dati:  
  
-   Se è necessario solo per lo scorrimento di un set di risultati, ma non i dati delle modifiche, usare una [forward-only](../../../ado/guide/data/forward-only-cursors.md) oppure [statico](../../../ado/guide/data/static-cursors.md) cursore.  
  
-   Se si dispone di un set di risultati di grandi dimensioni ed è necessario selezionare solo poche righe, usare una [keyset](../../../ado/guide/data/keyset-cursors.md) cursore.  
  
-   Se si desidera sincronizzare un set di risultati con recenti aggiunte, modifiche ed eliminazioni da tutti gli utenti simultanei, usare una [dinamica](../../../ado/guide/data/dynamic-cursors.md) cursore.  
  
 Sebbene sembri essere diverso ogni tipo di cursore, tenere presente che questi tipi di cursore non sono molto diverse varianti come semplicemente il risultato della combinazione di caratteristiche e le opzioni.  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Cursori forward-only](../../../ado/guide/data/forward-only-cursors.md)  
  
-   [Cursori statici](../../../ado/guide/data/static-cursors.md)  
  
-   [Cursori keyset](../../../ado/guide/data/keyset-cursors.md)  
  
-   [Cursori dinamici](../../../ado/guide/data/dynamic-cursors.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Cursori forward-Only](../../../ado/guide/data/forward-only-cursors.md)   
 [Cursori statici](../../../ado/guide/data/static-cursors.md)   
 [Cursori keyset](../../../ado/guide/data/keyset-cursors.md)   
 [Cursori dinamici](../../../ado/guide/data/dynamic-cursors.md)
