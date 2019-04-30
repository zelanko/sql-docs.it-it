---
title: Limitazioni di nomi di colonna | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- desktop database drivers [ODBC], column names
- ODBC desktop database drivers [ODBC], column names
ms.assetid: 5a339f61-c52f-40ad-8deb-d785f72753d4
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8a80ed397ae494bc686ef76aaeeef10b61662f19
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63301806"
---
# <a name="column-name-limitations"></a>Limitazioni dei nomi di colonna
I nomi di colonna possono contenere qualsiasi carattere validi (ad esempio, spazi). Se i nomi di colonna contengono caratteri tranne lettere, numeri e caratteri di sottolineatura, il nome deve essere delimitato racchiudendolo tra virgolette back (').  
  
 Quando viene usato il driver Microsoft Access o Microsoft Excel, i nomi delle colonne sono limitate a 64 caratteri e i nomi lunghi generano un errore. Quando viene usato il driver Paradox, il nome di colonna massima è di 25 caratteri. Quando viene usato il driver di testo, il nome di colonna massima è di 64 caratteri e i nomi lunghi vengono troncati.  
  
 Quando viene usato il driver dBASE, con un valore ASCII maggiore di 127 caratteri vengono convertiti in caratteri di sottolineatura.  
  
 Quando viene usato il driver di Microsoft Excel, se i nomi di colonna sono presenti, devono essere nella prima riga. Un nome che, in Microsoft Excel, Usa il "!" carattere deve essere racchiuso tra virgolette back ('). Il "!" carattere viene convertito nel carattere "$", perché il "!" carattere non valido in un nome ODBC, anche quando il nome è racchiuso tra virgolette back. Tutti gli altri caratteri validi di Microsoft Excel (tranne il carattere barra verticale (&#124;)) può essere usato nei nomi di colonna, inclusi gli spazi. Un identificatore delimitato da utilizzare per il nome di una colonna di Microsoft Excel per includere uno spazio. I nomi di colonna specificato verranno sostituiti con nomi generati dal driver, ad esempio, "Col1" per la prima colonna.  
  
 Il carattere barra verticale (&#124;) non è possibile usare un nome di colonna, se il nome è racchiuso tra virgolette back o No.  
  
 Quando viene usato il driver di testo, il driver fornisce un nome predefinito se non viene specificato un nome di colonna. Ad esempio, il driver chiama la prima colonna F1, la seconda colonna F2 e così via.
