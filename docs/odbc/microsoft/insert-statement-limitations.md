---
title: Limitazioni dell'istruzione INSERT Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC SQL grammar, INSERT statement limitations
- INSERT statement limitations [ODBC]
- truncation of data [ODBC]
ms.assetid: dea05698-527a-41ab-8729-bbed85556185
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f903f15ec13baa28a789891c1527dc742daa68ac
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300006"
---
# <a name="insert-statement-limitations"></a>Limitazioni dell'istruzione INSERT
I dati inseriti vengono troncati a destra senza alcun avviso se sono troppo lunghi per essere inseriti nella colonna.  
  
 Se si tenta di inserire un valore non compreso nell'intervallo del tipo di dati di una colonna, nella colonna verrà inserito un valore NULL.  
  
 Quando si utilizza un dBASE, Microsoft Excel, Paradox o Textdriver, l'inserimento di una stringa di lunghezza zero in una colonna inserisce effettivamente un valore NULL.  
  
 Quando viene utilizzato il driver di Microsoft Excel, se una stringa vuota viene inserita in una colonna, la stringa vuota viene convertita in un valore NULL; un'istruzione SELECT eseguita con una stringa vuota nella clausola WHERE non avrà esito positivo in tale colonna.  
  
 Una tabella non è aggiornabile dal driver Paradox in due condizioni:  
  
-   Quando un indice univoco non è definito nella tabella. Ciò non vale per una tabella vuota, che può essere aggiornata con una singola riga anche se nella tabella non è definito un indice univoco. Se una singola riga viene inserita in una tabella vuota che non dispone di un indice univoco, un'applicazione non può creare un indice univoco o inserire dati aggiuntivi dopo l'inserimento della singola riga.  
  
-   Se il Motore di database Borland non è implementato, nella tabella Paradox sono consentite solo istruzioni read e append.  
  
 Quando viene utilizzato il driver di testo, valori NULL sono rappresentati da una stringa con spaziatura vuota nei file a lunghezza fissa, ma non sono rappresentati da spazi nei file delimitati. Ad esempio, nella riga seguente contenente tre campi, il secondo campo è un valore NULL:  
  
```  
"Smith:,, 123  
```  
  
 Quando si utilizza il driver di testo, tutti i valori di colonna possono essere riempiti con spazi iniziali. La lunghezza di qualsiasi riga deve essere minore o uguale a 65.543 byte.
