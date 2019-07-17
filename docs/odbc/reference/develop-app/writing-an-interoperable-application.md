---
title: La scrittura di un'applicazione interoperativa | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f24e50b7f6dd8b129a2777ce1132ec426b7ea182
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68078980"
---
# <a name="writing-an-interoperable-application"></a>Scrittura di un'applicazione interoperativa
Ogni volta che un'applicazione utilizza lo stesso codice rispetto a più di un driver, tale codice deve essere interoperabili tra i driver. Nella maggior parte dei casi, questo è un compito facile. Ad esempio, il codice per recuperare le righe con un cursore forward-only è lo stesso per tutti i driver. In alcuni casi, può essere più difficile. Ad esempio, il codice per costruire gli identificatori per l'uso nelle istruzioni SQL deve prendere in considerazione maiuscole/minuscole identificatore deve essere racchiuso tra e le convenzioni di denominazione di una sola parte, due parti e tre parti.  
  
 In generale, codice di interoperabilità deve far fronte con problemi di supporto delle funzionalità e della variabilità delle funzionalità. *Supporto alle funzionalità* fa riferimento a una caratteristica particolare o meno è supportata. Ad esempio, DBMS non tutte supportano le transazioni e interoperativa codice deve funzionare correttamente indipendentemente dal supporto delle transazioni. *Variabilità delle funzionalità* fa riferimento a variazione nel modo in cui una determinata funzionalità è supportata. Ad esempio, i nomi di catalogo vengono inseriti all'inizio di identificatori in alcune DBMS e alla fine di identificatori in altri casi.  
  
 Consente di gestire le applicazioni con supporto della funzionalità e della variabilità delle funzionalità in fase di progettazione o in fase di esecuzione. Per risolvere il supporto delle funzionalità e la variabilità in fase di progettazione, uno sviluppatore esamina il DBMS di destinazione e i driver e assicura che lo stesso codice sia interoperativo tra di essi. Questo è in genere il modo in cui le applicazioni a basso o limitato interoperability gestiscono questi problemi.  
  
 Ad esempio, se lo sviluppatore garantisce che un'applicazione verticale funzionerà solo con quattro specifico DBMS e ognuno di tali DBMS supporta le transazioni, l'applicazione non è necessario verificare il supporto delle transazioni in fase di esecuzione di codice. Può sempre presupporre che le transazioni sono disponibili a causa la decisione di progettazione da usare solo quattro DBMS, ognuno dei quali supporta le transazioni.  
  
 Per risolvere il supporto delle funzionalità e la variabilità in fase di esecuzione, l'applicazione deve testare per diverse funzionalità in fase di esecuzione e agire di conseguenza. Questo è in genere il modo in cui le applicazioni altamente interoperabile gestiscono questi problemi. Per i problemi di supporto di funzionalità, ciò significa che la scrittura di codice che rende facoltativo o la scrittura del codice della funzione che emula la funzionalità quando non è disponibile. Per problemi di variabilità di funzionalità, ciò significa la scrittura di codice che supporta tutte le possibili varianti.  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Controllo del supporto e della variabilità delle funzionalità](../../../odbc/reference/develop-app/checking-feature-support-and-variability.md)  
  
-   [Funzionalità da controllare](../../../odbc/reference/develop-app/features-to-watch-for.md)
