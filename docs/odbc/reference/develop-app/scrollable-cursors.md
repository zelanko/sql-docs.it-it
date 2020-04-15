---
title: Cursori scorrevoli . Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- scrollable cursors [ODBC]
- cursors [ODBC], scrollable
ms.assetid: 2c8a5f50-9b37-452f-8160-05f42bc4d97e
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2762ffc7fa179fc6a68f92c23f92ca12803f5ab7
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304212"
---
# <a name="scrollable-cursors"></a>Cursori scorrevoli
Nelle moderne applicazioni basate su schermo, l'utente scorre avanti e indietro tra i dati. Per tali applicazioni, tornare a una riga recuperata in precedenza è un problema. Una possibilità consiste nel chiudere e riaprire il cursore e quindi recuperare le righe fino a quando il cursore raggiunge la riga richiesta. Un'altra possibilità consiste nel leggere il set di risultati, memorizzarlo nella cache locale e implementare lo scorrimento nell'applicazione. Entrambe le possibilità funzionano bene solo con set di risultati di piccole dimensioni e quest'ultima possibilità è difficile da implementare. Una soluzione migliore consiste nell'utilizzare un *cursore scorrevole,* che può spostarsi avanti e indietro nel set di risultati.  
  
 Un *cursore scorrevole* è comunemente usato nelle moderne applicazioni basate su schermo in cui l'utente scorre avanti e indietro tra i dati. Tuttavia, le applicazioni devono utilizzare cursori scorrevoli solo quando i cursori forward-only non eseguono il processo, poiché i cursori scorrevoli sono in genere più costosi dei cursori forward-only.  
  
 La possibilità di spostarsi all'indietro genera una domanda non applicabile ai cursori forward-only: un cursore scorrevole deve rilevare le modifiche apportate alle righe recuperate in precedenza? Vale a dire, deve rilevare le righe aggiornate, eliminate e appena inserite?  
  
 Questa domanda sorge perché la definizione di un set di risultati, ovvero il set di righe che soddisfa determinati criteri, non indica quando le righe vengono controllate per verificare se corrispondono a tali criteri, né indica se le righe devono contenere gli stessi dati ogni volta che vengono recuperate. La prima omissione consente ai cursori scorrevoli di rilevare se le righe sono state inserite o eliminate, mentre la seconda consente loro di rilevare i dati aggiornati.  
  
 La capacità di rilevare i cambiamenti a volte è utile, a volte no. Ad esempio, un'applicazione di contabilità necessita di un cursore che ignori tutte le modifiche; bilanciamento dei libri è impossibile se il cursore mostra le ultime modifiche. D'altra parte, un sistema di prenotazione aerea ha bisogno di un cursore che mostri le ultime modifiche ai dati; senza tale cursore, deve continuamente rieseguire una query sul database per mostrare la disponibilità di volo più aggiornata.  
  
 Per soddisfare le esigenze di diverse applicazioni, ODBC definisce quattro diversi tipi di cursori scorrevoli. Questi cursori variano sia in termini di spesa che nella capacità di rilevare le modifiche al set di risultati. Si noti che se un cursore scorrevole è in grado di rilevare le modifiche apportate alle righe, può rilevarle solo quando tenta di recuperare nuovamente tali righe; non è possibile per l'origine dati notificare al cursore le modifiche apportate alle righe attualmente recuperate. Si noti inoltre che la visibilità delle modifiche è controllata anche dal livello di isolamento della transazione; Per ulteriori informazioni, vedere [Isolamento delle transazioni](../../../odbc/reference/develop-app/transaction-isolation.md).  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Tipi di cursore scorrevoli](../../../odbc/reference/develop-app/scrollable-cursor-types.md)  
  
-   [Utilizzo di cursori scorrevoli](../../../odbc/reference/develop-app/using-scrollable-cursors.md)  
  
-   [Scorrimento relativo e assoluto](../../../odbc/reference/develop-app/relative-and-absolute-scrolling.md)  
  
-   [Segnalibri](../../../odbc/reference/develop-app/bookmarks-odbc.md)
