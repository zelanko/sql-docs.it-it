---
title: Limitazioni dell'istruzione INSERT | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 1676af6216ac703e9a8976951ec2888b9e940b67
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68085518"
---
# <a name="insert-statement-limitations"></a>Limitazioni dell'istruzione INSERT
I dati inseriti vengono troncati a destra senza preavviso se sono troppo lunghi per essere inseriti nella colonna.  
  
 Il tentativo di inserire un valore non compreso nell'intervallo del tipo di dati di una colonna comporta l'inserimento di un valore NULL nella colonna.  
  
 Quando si usa dBASE, Microsoft Excel, Paradox o Textdriver, l'inserimento di una stringa di lunghezza zero in una colonna inserisce effettivamente un valore NULL.  
  
 Quando si utilizza il driver Microsoft Excel, se in una colonna viene inserita una stringa vuota, la stringa vuota viene convertita in un valore NULL. un'istruzione SELECT con ricerca eseguita con una stringa vuota nella clausola WHERE non riuscirà in tale colonna.  
  
 Una tabella non può essere aggiornata dal driver Paradox in due condizioni:  
  
-   Se nella tabella non è definito un indice univoco. Questa operazione non è valida per una tabella vuota, che può essere aggiornata con una singola riga anche se nella tabella non è definito un indice univoco. Se in una tabella vuota viene inserita una singola riga che non dispone di un indice univoco, un'applicazione non è in grado di creare un indice univoco o di inserire dati aggiuntivi dopo l'inserimento di una singola riga.  
  
-   Se la motore di database Borland non è implementata, nella tabella Paradox sono consentite solo istruzioni Read e Append.  
  
 Quando si usa il driver di testo, i valori NULL sono rappresentati da una stringa con riempimento vuoto nei file a lunghezza fissa, ma sono rappresentati da nessun spazio nei file delimitati. Ad esempio, nella riga seguente che contiene tre campi, il secondo campo è un valore NULL:  
  
```  
"Smith:,, 123  
```  
  
 Quando si usa il driver di testo, tutti i valori di colonna possono essere riempiti con spazi iniziali. La lunghezza di una riga deve essere minore o uguale a 65.543 byte.
