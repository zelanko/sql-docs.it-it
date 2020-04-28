---
title: Cursori scorrevoli | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81304212"
---
# <a name="scrollable-cursors"></a>Cursori scorrevoli
Nelle applicazioni moderne basate su schermo, l'utente scorre in avanti e indietro i dati. Per tali applicazioni, il ritorno a una riga recuperata in precedenza costituisce un problema. Una possibilità consiste nel chiudere e riaprire il cursore, quindi recuperare le righe fino a quando il cursore non raggiunge la riga richiesta. Un'altra possibilità consiste nel leggere il set di risultati, memorizzarlo nella cache in locale e implementare lo scorrimento nell'applicazione. Entrambe le possibilità funzionano correttamente solo con set di risultati di piccole dimensioni e la seconda possibilità è difficile da implementare. Una soluzione migliore consiste nell'usare un *cursore scorrevole,* che può spostarsi avanti e indietro nel set di risultati.  
  
 Un *cursore scorrevole* viene comunemente utilizzato nelle applicazioni moderne basate sullo schermo in cui l'utente scorre verso l'interno dei dati. Tuttavia, le applicazioni devono utilizzare cursori scorrevoli solo quando i cursori di sola trasmissione non eseguono il processo, poiché i cursori scorrevoli sono in genere più costosi dei cursori di sola trasmissione.  
  
 La possibilità di spostare le versioni precedenti genera una domanda non applicabile ai cursori di sola trasmissione: se un cursore scorrevole rileva le modifiche apportate alle righe recuperate in precedenza? Ovvero dovrebbe rilevare le righe aggiornate, eliminate e appena inserite?  
  
 Questa domanda si verifica perché la definizione di un set di risultati, ovvero il set di righe che corrisponde a determinati criteri, non indica se le righe vengono controllate per verificare se corrispondono a tale criterio, né se le righe devono contenere gli stessi dati ogni volta che vengono recuperate. L'omissione precedente consente ai cursori scorrevoli di rilevare se le righe sono state inserite o eliminate, mentre quest'ultima consente di rilevare i dati aggiornati.  
  
 La possibilità di rilevare le modifiche è talvolta utile, a volte non. Per un'applicazione di contabilità, ad esempio, è necessario un cursore che ignori tutte le modifiche. il bilanciamento dei libri è impossibile se il cursore mostra le ultime modifiche. D'altra parte, per un sistema di prenotazione Airline è necessario un cursore che mostra le ultime modifiche apportate ai dati. senza tale cursore, deve continuamente eseguire una query sul database per visualizzare la disponibilità più aggiornata del volo.  
  
 Per soddisfare le esigenze di applicazioni diverse, ODBC definisce quattro tipi diversi di cursori scorrevoli. Questi cursori variano sia in spese che in grado di rilevare le modifiche apportate al set di risultati. Si noti che se un cursore scorrevole è in grado di rilevare le modifiche apportate alle righe, può rilevarle solo quando tenta di recuperare tali righe; per l'origine dati non è possibile notificare al cursore le modifiche apportate alle righe attualmente recuperate. Si noti inoltre che la visibilità delle modifiche viene controllata anche dal livello di isolamento della transazione. Per ulteriori informazioni, vedere [isolamento delle transazioni](../../../odbc/reference/develop-app/transaction-isolation.md).  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Tipi di cursore scorrevoli](../../../odbc/reference/develop-app/scrollable-cursor-types.md)  
  
-   [Utilizzo di cursori scorrevoli](../../../odbc/reference/develop-app/using-scrollable-cursors.md)  
  
-   [Scorrimento relativo e assoluto](../../../odbc/reference/develop-app/relative-and-absolute-scrolling.md)  
  
-   [Segnalibri](../../../odbc/reference/develop-app/bookmarks-odbc.md)
