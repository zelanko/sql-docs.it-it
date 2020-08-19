---
description: Scrittura di un'applicazione interoperativa
title: Scrittura di un'applicazione interoperativa | Microsoft Docs
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
ms.openlocfilehash: 0d8bff1848e20705ab64b8284ed42331c80fb23a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88421365"
---
# <a name="writing-an-interoperable-application"></a>Scrittura di un'applicazione interoperativa
Ogni volta che un'applicazione utilizza lo stesso codice per più di un driver, il codice deve essere interoperativo tra i driver. Nella maggior parte dei casi, si tratta di un'attività semplice. Ad esempio, il codice per recuperare le righe con un cursore di sola trasmissione è lo stesso per tutti i driver. In alcuni casi può essere più difficile. Ad esempio, il codice per costruire identificatori da utilizzare nelle istruzioni SQL deve prendere in considerazione le convenzioni tra maiuscole e minuscole dell'identificatore, le virgolette e le convenzioni di denominazione in tre parti.  
  
 In generale, il codice interoperativo deve far fronte ai problemi di supporto delle funzionalità e della variabilità delle funzionalità. Il *supporto delle funzionalità* indica se una particolare funzionalità è o meno supportata. Ad esempio, non tutti i DBMS supportano le transazioni e il codice interoperativo deve funzionare correttamente indipendentemente dal supporto delle transazioni. La *variabilità delle caratteristiche* si riferisce alla variazione del modo in cui è supportata una determinata funzionalità. I nomi dei cataloghi, ad esempio, vengono posizionati all'inizio degli identificatori in alcuni DBMS e alla fine degli identificatori in altri.  
  
 Le applicazioni possono gestire il supporto delle funzionalità e la variabilità delle caratteristiche in fase di progettazione o in fase di esecuzione. Per gestire il supporto e la variabilità della funzionalità in fase di progettazione, uno sviluppatore esamina i sistemi DBMS e i driver di destinazione e assicura che lo stesso codice sia interoperativo tra di essi. Questo è in genere il modo in cui le applicazioni con interoperabilità bassa o limitata gestiscono questi problemi.  
  
 Se, ad esempio, lo sviluppatore garantisce che un'applicazione verticale funzionerà solo con quattro DBMS specifici e se ognuno di questi DBMS supporta le transazioni, l'applicazione non necessita di codice per verificare il supporto delle transazioni in fase di esecuzione. Può sempre presupporre che le transazioni siano disponibili a causa della decisione della fase di progettazione di usare solo quattro DBMS, ognuno dei quali supporta le transazioni.  
  
 Per gestire il supporto della funzionalità e la variabilità in fase di esecuzione, l'applicazione deve testare funzionalità diverse in fase di esecuzione e agire di conseguenza. Questo è in genere il modo in cui le applicazioni altamente interoperative gestiscono questi problemi. Per i problemi di supporto delle funzionalità, significa scrivere codice che rende la funzionalità facoltativa o scrivere codice che emula la funzionalità quando non è disponibile. Per i problemi di variabilità delle funzionalità, significa scrivere codice che supporta tutte le possibili varianti.  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Controllo del supporto e della variabilità delle funzionalità](../../../odbc/reference/develop-app/checking-feature-support-and-variability.md)  
  
-   [Funzionalità da controllare](../../../odbc/reference/develop-app/features-to-watch-for.md)
