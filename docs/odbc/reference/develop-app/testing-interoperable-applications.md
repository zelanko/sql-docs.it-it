---
title: Test delle applicazioni interoperabili Documenti Microsoft
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c1d43c7aad2501591c497475f6c250ac33712aa7
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307742"
---
# <a name="testing-interoperable-applications"></a>Test delle applicazioni interoperative
Testare applicazioni interoperabili è nella migliore delle ipotesi un'azienda che richiede molto tempo e, nel peggiore dei casi, è impossibile perché nuovi driver appaiono continuamente sul mercato. Tuttavia, un ragionevole grado di test è possibile. Le applicazioni con interoperabilità limitata o bassa devono essere testate solo rispetto a tali driver che sono garantiti per supportare. Tuttavia, devono essere completamente testati contro questi driver.  
  
 Le applicazioni altamente interoperabili non possono essere testate praticamente contro tutti i conducenti. Il meglio che la maggior parte degli sviluppatori di applicazioni può fare è quello di testarli completamente su un piccolo numero di driver e superficialmente su molti altri. I driver testati dovrebbero includere i driver più popolari per i DBSMO più popolari nel mercato dell'applicazione; se il mercato copre tutti i DBSMO, i driver per DBS per desktop e server devono essere testati.  
  
 Uno dei problemi nel test delle applicazioni ODBC è il numero di componenti coinvolti: l'applicazione stessa, Gestione Driver, il driver, il DBMS ed eventualmente il software di rete o gateway. Le applicazioni possono semplificare il rilevamento degli errori registrando i messaggi di errore restituiti dalle funzioni ODBC tramite **SQLGetDiagField** e **SQLGetDiagRec**. Questi messaggi identificano il produttore e il componente in cui si verificano errori. Per ulteriori informazioni, vedere [Diagnostica](../../../odbc/reference/develop-app/diagnostics.md).
