---
title: Proprietà Unicode . Documenti Microsoft
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9824e76cebabb6f5f84505292801a0094e359f0f
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302446"
---
# <a name="unicode"></a>Unicode
Unicode definisce la codifica per i caratteri in molte lingue.  
  
 Per ulteriori informazioni sullo standard Unicode, vedere [Il consorzio Unicode](https://www.unicode.org).  
  
 Unicode definisce un set di caratteri universale. Una tabella codici ANSI di Windows definisce un set di caratteri, in genere contenente caratteri per una lingua. Potrebbe essere più difficile scrivere un'applicazione necessaria per utilizzare tabelle codici diverse.  
  
 Unicode non richiede una tabella codici. Ogni punto di codice viene mappato a un singolo carattere in una lingua.  
  
 Attualmente, l'unica codifica Unicode supportata da ODBC è UCS-2, che utilizza un numero intero a 16 bit (lunghezza fissa) per rappresentare un carattere. Unicode consente alle applicazioni di lavorare in lingue diverse.  
  
 Gestione Driver ODBC 3.5 (o versione successiva) è abilitato per Unicode. Ciò influisce su due aree principali: chiamate di funzione e tipi di dati stringa. Gestione Driver esegue il mapping di argomenti di stringa di funzione e dati di stringa come richiesto dall'applicazione e dal driver, entrambi i quali possono essere abilitati per Unicode o ANSI. Queste due aree vengono descritte in dettaglio nelle sezioni [Argomenti delle](../../../odbc/reference/develop-app/unicode-function-arguments.md) funzioni Unicode e [Dati Unicode](../../../odbc/reference/develop-app/unicode-data.md).  
  
 Gestione driver ODBC 3.5 (o versione successiva) supporta l'utilizzo di un driver Unicode con un'applicazione Unicode e un'applicazione ANSI. Supporta inoltre l'utilizzo di un driver ANSI con un'applicazione ANSI. Gestione Driver fornisce un mapping Unicode-ANSI limitato per un'applicazione Unicode che utilizza un driver ANSI.  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Argomenti funzione Unicode](../../../odbc/reference/develop-app/unicode-function-arguments.md)  
  
-   [Dati Unicode](../../../odbc/reference/develop-app/unicode-data.md)
