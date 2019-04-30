---
title: Test delle applicazioni interoperative | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- interoperability [ODBC], testing interoperable applications
- testing interoperable applications [ODBC]
ms.assetid: 489083cb-8430-40be-9ef2-d75b9a2eea88
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 509dd17efeeb982c51938d7a18fad99a2e84ba5b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63148935"
---
# <a name="testing-interoperable-applications"></a>Test delle applicazioni interoperative
Test delle applicazioni interoperative è nella migliore delle ipotesi richiede un tempo impossibili nel peggiore dei casi poiché i nuovi driver vengono visualizzati continuamente disponibili sul mercato e aziendali. Tuttavia, un livello ragionevole di test è possibile. Le applicazioni a basso o limitato interoperability devono solo essere controllate rispetto a questi driver è garantito che per il supporto. Tuttavia, essi devono essere completamente testati rispetto a tali driver.  
  
 Non è possibile testare le applicazioni altamente interoperabile praticamente su tutti i driver. Il meglio che possono eseguire la maggior parte degli sviluppatori di applicazioni consiste nell'eseguirne il test completamente su un numero ridotto di driver e cursorily su diversi altri. Driver testato deve includere i driver più diffusi per il DBMS più diffuso nel mercato dell'applicazione; Se il mercato copre tutti i DBMS, è opportuno sottoporre i driver per i desktop e server DBMS.  
  
 Uno dei problemi nel test le applicazioni ODBC è il numero di componenti coinvolti: l'applicazione stessa, gestione Driver, driver, DBMS e possibilmente un software di rete o i gateway. Le applicazioni rendono più semplice rilevare errori inviando i messaggi di errore restituiti dalle funzioni ODBC attraverso **SQLGetDiagField** e **SQLGetDiagRec**. Questi messaggi identificano il produttore e il componente in cui si verificano errori. Per altre informazioni, vedere [diagnostica](../../../odbc/reference/develop-app/diagnostics.md).
