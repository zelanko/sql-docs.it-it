---
title: Test di applicazioni interoperative | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81307742"
---
# <a name="testing-interoperable-applications"></a>Test delle applicazioni interoperative
Il test delle applicazioni interoperative è al meglio un'attività che richiede molto tempo e non è più possibile perché i nuovi driver vengono continuamente visualizzati sul mercato. Tuttavia, è possibile un livello di test ragionevole. Le applicazioni con interoperabilità limitata o limitata devono essere testate solo a fronte di questi driver garantiti per il supporto. Tuttavia, devono essere testati completamente rispetto a questi driver.  
  
 Le applicazioni altamente interoperabili non possono essere testate praticamente rispetto a tutti i driver. Il modo migliore per la maggior parte degli sviluppatori di applicazioni consiste nel testarli completamente rispetto a un numero ridotto di driver e superficialmente rispetto a diversi altri. I driver testati dovrebbero includere i driver più diffusi per i DBMS più diffusi nel mercato dell'applicazione; Se il mercato copre tutti i sistemi DBMS, i driver per i sistemi DBMS desktop e server devono essere testati.  
  
 Uno dei problemi relativi al test delle applicazioni ODBC è costituito dal numero di componenti necessari: l'applicazione stessa, gestione driver, il driver, il sistema DBMS ed eventualmente il software o i gateway di rete. Le applicazioni possono semplificare il rilevamento degli errori pubblicando i messaggi di errore restituiti dalle funzioni ODBC tramite **SQLGetDiagField** e **SQLGetDiagRec**. Questi messaggi identificano il produttore e il componente in cui si verificano gli errori. Per ulteriori informazioni, vedere [diagnostica](../../../odbc/reference/develop-app/diagnostics.md).
