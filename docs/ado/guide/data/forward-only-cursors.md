---
title: Cursori di sola trasmissione | Microsoft Docs
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
ms.openlocfilehash: e84fbf2b8fda2fa2b14088af1e0830d8109aba8a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "67925300"
---
# <a name="forward-only-cursors"></a>Cursori forward-only
Il tipo di cursore predefinito tipico, denominato cursore di tipo "Avanti" o non scorrevole ", può essere spostato solo in avanti nel set di risultati. Un cursore di sola trasmissione non supporta lo scorrimento, ovvero la possibilità di spostarsi avanti e indietro nel set di risultati. supporta solo il recupero di righe dall'inizio alla fine del set di risultati. Con alcuni cursori di sola lettura (ad esempio con la libreria di cursori SQL Server), tutte le istruzioni INSERT, Update e DELETE eseguite dall'utente corrente (o di cui è stato eseguito il commit da altri utenti) che interessano le righe nel set di risultati sono visibili durante il recupero delle righe. Poiché lo scorrimento all'indietro del cursore non è consentito, tuttavia, le modifiche apportate alle righe nel database dopo il recupero delle righe stesse non sono visibili tramite il cursore.  
  
 Una volta elaborati i dati per la riga corrente, il cursore di sola trasmissione rilascia le risorse utilizzate per l'utilizzo di tali dati. I cursori forward-only sono dinamici per impostazione predefinita, vale a dire che tutte le modifiche vengono rilevate durante l'elaborazione della riga corrente. Questo consente maggiore rapidità di apertura del cursore e la visualizzazione nel set di risultati degli aggiornamenti apportati alle tabelle sottostanti.  
  
 Mentre i cursori di sola trasmissione non supportano lo scorrimento a ritroso, l'applicazione può tornare all'inizio del set di risultati chiudendo e riaprendo il cursore. Si tratta di un modo efficace per lavorare con piccole quantità di dati. In alternativa, l'applicazione potrebbe leggere il set di risultati una sola volta, memorizzare nella cache i dati localmente, quindi esplorare la cache di dati locale.  
  
 Se l'applicazione non richiede lo scorrimento del set di risultati, il cursore di tipo "solo" è il modo migliore per recuperare rapidamente i dati con la minima quantità di overhead. Usare **AdOpenForwardOnly CursorTypeEnum** per indicare che si vuole usare un cursore di sola trasmissione in ADO.  
  
## <a name="see-also"></a>Vedere anche  
 [Cursori statici](../../../ado/guide/data/static-cursors.md)   
 [Cursori keyset](../../../ado/guide/data/keyset-cursors.md)   
 [Cursori dinamici](../../../ado/guide/data/dynamic-cursors.md)
