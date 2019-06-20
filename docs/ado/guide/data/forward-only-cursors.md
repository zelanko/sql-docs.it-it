---
title: I cursori forward-Only | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- cursors [ADO], forward-only
- forward-only cursors [ADO]
ms.assetid: 2b1e062f-3294-4a6f-8241-a17045c4df18
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 15d11b8882e8e39a03ffb7509526a4f66b6553b3
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66700707"
---
# <a name="forward-only-cursors"></a>Cursori forward-only
Il tipo di cursore predefinito tipico, chiamato un cursore forward-only (o non scorrevole), possa spostarsi solo in avanti il set di risultati. Con cursori forward-only non supporta lo scorrimento (la possibilità di spostarsi avanti e indietro nel set di risultati); supporta solo il recupero di righe dall'inizio alla fine del set di risultati. Con alcuni cursori forward-only (ad esempio con la libreria di cursori SQL Server), tutte le istruzioni delete, update e insert eseguite dall'utente corrente (o da altri utenti) che coinvolgono le righe nel set di risultati sono visibili come le righe vengono recuperate. Poiché lo scorrimento all'indietro del cursore non è consentito, tuttavia, le modifiche apportate alle righe nel database dopo il recupero delle righe stesse non sono visibili tramite il cursore.  
  
 Dopo l'elaborazione dati per la riga corrente, il cursore forward-only rilascia le risorse che sono state usate per contenere i dati. I cursori forward-only sono dinamici per impostazione predefinita, vale a dire che tutte le modifiche vengono rilevate durante l'elaborazione della riga corrente. Questo consente maggiore rapidità di apertura del cursore e la visualizzazione nel set di risultati degli aggiornamenti apportati alle tabelle sottostanti.  
  
 Mentre i cursori forward-only non supportano lo scorrimento all'indietro, l'applicazione può tornare all'inizio del set di risultati tramite la chiusura e riapertura del cursore. Si tratta di un metodo efficace per lavorare con piccole quantità di dati. In alternativa, l'applicazione è stato possibile leggere il set di risultati una volta, memorizzare nella cache i dati in locale e quindi selezionare la cache locale dei dati.  
  
 Se l'applicazione non richiede lo scorrimento di set di risultati, i cursori forward-only sono il modo migliore per recuperare i dati rapidamente con la minima quantità di overhead. Usare la **adOpenForwardOnly CursorTypeEnum** per indicare che si desidera utilizzare un cursore forward-only in ADO.  
  
## <a name="see-also"></a>Vedere anche  
 [Cursori statici](../../../ado/guide/data/static-cursors.md)   
 [Cursori keyset](../../../ado/guide/data/keyset-cursors.md)   
 [Cursori dinamici](../../../ado/guide/data/dynamic-cursors.md)
