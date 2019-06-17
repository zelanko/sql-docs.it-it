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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 80be6994c7094b365bc24dd135bdda6ec4e561ab
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62468387"
---
# <a name="scrollable-cursors"></a>Cursori scorrevoli
Nelle moderne applicazioni basate su schermo, l'utente scorre avanti e indietro tra i dati. Per tali applicazioni, tornare a una riga recuperata in precedenza è un problema. Una possibilità consiste nel chiudere e riaprire il cursore e quindi recuperare le righe finché il cursore raggiunge la riga necessaria. Un'altra possibilità consiste nel leggere il set di risultati, memorizzarlo nella cache in locale e implementare lo scorrimento nell'applicazione. Entrambe le possibilità funzionano bene solo con set di risultati di piccole dimensioni e la possibilità di quest'ultima è difficile da implementare. Una soluzione migliore consiste nell'usare un *cursori scorrevoli,* che può spostarsi avanti e indietro nel set di risultati.  
  
 Oggetto *cursore scorrevole* viene comunemente usato nelle moderne applicazioni basate su schermo in cui l'utente scorre avanti e indietro tra i dati. Tuttavia, le applicazioni utilizzino i cursori scorrevoli solo quando i cursori forward-only non eseguirà il processo, come i cursori scorrevoli risultano in genere più costosi di cursori forward-only.  
  
 La possibilità di spostarsi all'indietro, pone una questione non applicabile per i cursori forward-only: Un cursore scorrevole deve rilevare le modifiche apportate alle righe recuperate in precedenza? Vale a dire lo rileverà righe aggiornate, eliminate e appena inserite?  
  
 Questa domanda si verifica perché la definizione di un set di risultati: il set di righe che soddisfa determinati criteri - non indica quando le righe vengono controllate per verificare se corrispondono i relativi criteri, né se non se righe devono contenere gli stessi dati ogni volta che vengono richiamate di stato. L'omissione precedente rende possibile per i cursori scorrevoli rilevare se righe viene inserite o eliminate, mentre quest'ultimo consente di rilevare i dati aggiornati.  
  
 La possibilità di rilevare le modifiche è talvolta utile, in alcuni casi non. Ad esempio, un'applicazione di contabilità richiede un cursore che consente di ignorare tutte le modifiche; documentazione di bilanciamento del carico è possibile se il cursore mostra le modifiche più recenti. D'altra parte, un sistema di prenotazione compagnia aerea deve un cursore che visualizza le modifiche più recenti per i dati. senza un cursore, continuamente necessario rieseguire la query del database per visualizzare la disponibilità più aggiornata di volo.  
  
 Per coprire le esigenze delle diverse applicazioni, ODBC definisce quattro diversi tipi di cursori scorrevoli. I cursori variano entrambe spese e la capacità di rilevare le modifiche apportate al risultato del set. Si noti che se un cursore scorrevole può rilevare le modifiche alle righe, può solo rilevare li durante il tentativo di recupero di tali righe; non è possibile per l'origine dati notificare al cursore le modifiche apportate alle righe attualmente recuperate. Si noti anche che la visibilità delle modifiche viene controllata anche dal livello di isolamento delle transazioni; per altre informazioni, vedere [isolamento delle transazioni](../../../odbc/reference/develop-app/transaction-isolation.md).  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Tipi di cursore scorrevoli](../../../odbc/reference/develop-app/scrollable-cursor-types.md)  
  
-   [Utilizzo di cursori scorrevoli](../../../odbc/reference/develop-app/using-scrollable-cursors.md)  
  
-   [Scorrimento relativo e assoluto](../../../odbc/reference/develop-app/relative-and-absolute-scrolling.md)  
  
-   [Segnalibri](../../../odbc/reference/develop-app/bookmarks-odbc.md)
