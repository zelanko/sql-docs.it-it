---
title: Limitazioni del nome della colonna Documenti Microsoft
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 41d973afdac360af114da41620997cad23a2c740
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81281381"
---
# <a name="column-name-limitations"></a>Limitazioni dei nomi di colonna
I nomi di colonna possono contenere qualsiasi carattere valido (ad esempio, spazi). Se i nomi delle colonne contengono caratteri ad eccezione di lettere, numeri e caratteri di sottolineatura, il nome deve essere delimitato racchiudendolo tra virgolette rovesciate (').  
  
 Quando si utilizza il driver di Microsoft Access o Microsoft Excel, i nomi delle colonne sono limitati a 64 caratteri e i nomi più lunghi generano un errore. Quando viene utilizzato il driver Paradox, il nome massimo della colonna è 25 caratteri. Quando viene utilizzato il driver di testo, il nome massimo della colonna è 64 caratteri e i nomi più lunghi vengono troncati.  
  
 Quando si utilizza il driver dBASE, i caratteri con un valore ASCII maggiore di 127 vengono convertiti in caratteri di sottolineatura.  
  
 Quando viene utilizzato il driver di Microsoft Excel, se sono presenti nomi di colonna, devono essere nella prima riga. Un nome che in Microsoft Excel utilizzerebbe il carattere "!" deve essere racchiuso tra virgolette rovesciate ('). Il carattere "!" viene convertito nel carattere "" perché il carattere "!" non è valido in un nome ODBC, anche quando il nome è racchiuso tra virgolette. Tutti gli altri caratteri validi di Microsoft Excel (ad eccezione del carattere barra verticale (&#124;)) possono essere utilizzati in un nome di colonna, inclusi gli spazi. Per includere uno spazio, è necessario utilizzare un identificatore delimitato per un nome di colonna di Microsoft Excel. I nomi di colonna non specificati verranno sostituiti con nomi generati dal driver, ad esempio "Col1" per la prima colonna.  
  
 Il carattere barra verticale (&#124;) non può essere utilizzato in un nome di colonna, indipendentemente dal fatto che il nome sia racchiuso o meno tra virgolette rovesciate.  
  
 Quando viene utilizzato il driver di testo, il driver fornisce un nome predefinito se non viene specificato un nome di colonna. Ad esempio, il driver chiama la prima colonna F1, la seconda colonna F2 e così via.
