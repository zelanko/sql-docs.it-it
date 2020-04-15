---
title: Scrittura di un'applicazione interoperabile Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- interoperability [ODBC], feature support and variability
- interoperability [ODBC], writing interoperable applications
- feature support in interoperable applications [ODBC]
- feature variability in interoperable applications [ODBC]
ms.assetid: 8b42b8ae-7862-4b63-a0b3-2a204e0c43a5
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 553e718e0759e47701e7f8c04561693358d5dc52
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81289083"
---
# <a name="writing-an-interoperable-application"></a>Scrittura di un'applicazione interoperativa
Ogni volta che un'applicazione utilizza lo stesso codice su più di un driver, tale codice deve essere interoperabile tra tali driver. Nella maggior parte dei casi, questo è un compito facile. Ad esempio, il codice per recuperare le righe con un cursore forward-only è lo stesso per tutti i driver. In alcuni casi, questo può essere più difficile. Ad esempio, il codice per costruire gli identificatori da utilizzare nelle istruzioni SQL deve considerare le convenzioni di tipo identificatore, citazione e una parte, due parti e tre parti.  
  
 In generale, il codice interoperabile deve far fronte ai problemi di supporto delle funzionalità e variabilità delle funzionalità. *Il supporto delle funzionalità* si riferisce al fatto che una particolare funzionalità sia supportata o meno. Ad esempio, non tutti i DBDB supportano le transazioni e il codice interoperabile deve funzionare correttamente indipendentemente dal supporto delle transazioni. *La variabilità* delle funzionalità si riferisce alla variazione nel modo in cui è supportata una particolare funzionalità. Ad esempio, i nomi dei cataloghi vengono inseriti all'inizio degli identificatori in alcuni DBS e alla fine degli identificatori in altri.  
  
 Le applicazioni possono gestire il supporto delle funzionalità e la variabilità delle funzionalità in fase di progettazione o in fase di esecuzione. Per gestire il supporto delle funzionalità e la variabilità in fase di progettazione, uno sviluppatore esamina i DBSMO e i driver di destinazione e verifica che lo stesso codice sia interoperabile tra di essi. Questo è generalmente il modo in cui le applicazioni con interoperabilità bassa o limitata affrontano questi problemi.  
  
 Ad esempio, se lo sviluppatore garantisce che un'applicazione verticale funzionerà solo con quattro DBS specifici e se ognuno di questi DBMS supporta le transazioni, l'applicazione non necessita di codice per verificare il supporto delle transazioni in fase di esecuzione. Si può sempre supporre che le transazioni sono disponibili a causa della decisione in fase di progettazione di utilizzare solo quattro DBS, ognuno dei quali supporta le transazioni.  
  
 Per gestire il supporto delle funzionalità e la variabilità in fase di esecuzione, l'applicazione deve testare le diverse funzionalità in fase di esecuzione e agire di conseguenza. Questo è generalmente il modo in cui le applicazioni altamente interoperabili affrontano questi problemi. Per i problemi di supporto delle funzionalità, ciò significa scrivere codice che rende la funzionalità facoltativa o codice che emula la funzionalità quando non è disponibile. Per i problemi di variabilità delle funzionalità, ciò significa scrivere codice che supporti tutte le possibili variazioni.  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Controllo del supporto e della variabilità delle funzionalità](../../../odbc/reference/develop-app/checking-feature-support-and-variability.md)  
  
-   [Funzionalità da controllare](../../../odbc/reference/develop-app/features-to-watch-for.md)
