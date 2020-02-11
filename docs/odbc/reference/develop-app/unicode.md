---
title: Unicode | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Unicode [ODBC]
- Unicode [ODBC], about Unicode
ms.assetid: 113e1c9a-8333-4805-86f2-e4b57ab816a5
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 7e0044a2e2efbf0d8921a07ed4679806ba50bcd1
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68087558"
---
# <a name="unicode"></a>Unicode
Unicode definisce la codifica per i caratteri in molte lingue.  
  
 Per ulteriori informazioni sullo standard Unicode, vedere [il Consorzio Unicode](https://www.unicode.org).  
  
 Unicode definisce un set di caratteri universali. Una tabella codici ANSI di Windows definisce un set di caratteri che in genere contiene caratteri per una lingua. Potrebbe essere più difficile scrivere un'applicazione necessaria per utilizzare tabelle codici diverse.  
  
 Unicode non richiede una tabella codici. Ogni punto di codice viene mappato a un singolo carattere in una lingua.  
  
 Attualmente, l'unica codifica Unicode supportata da ODBC è UCS-2, che usa un Integer a 16 bit (a lunghezza fissa) per rappresentare un carattere. Unicode consente alle applicazioni di funzionare in linguaggi diversi.  
  
 La gestione driver ODBC 3,5 (o versione successiva) è abilitata per Unicode. Questo effetto riguarda due aree principali: le chiamate di funzione e i tipi di dati stringa. Gestione driver esegue il mapping degli argomenti della stringa di funzione e dei dati di tipo stringa come richiesto dall'applicazione e dal driver, che possono essere abilitati per Unicode o ANSI. Queste due aree sono descritte in dettaglio nelle sezioni argomenti della [funzione Unicode](../../../odbc/reference/develop-app/unicode-function-arguments.md) e [dati Unicode](../../../odbc/reference/develop-app/unicode-data.md).  
  
 Gestione driver ODBC 3,5 (o versione successiva) supporta l'utilizzo di un driver Unicode con un'applicazione Unicode e un'applicazione ANSI. Supporta inoltre l'utilizzo di un driver ANSI con un'applicazione ANSI. Gestione driver fornisce un mapping da Unicode a ANSI limitato per un'applicazione Unicode che utilizza un driver ANSI.  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Argomenti funzione Unicode](../../../odbc/reference/develop-app/unicode-function-arguments.md)  
  
-   [Dati Unicode](../../../odbc/reference/develop-app/unicode-data.md)
