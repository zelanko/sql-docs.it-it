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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68085518"
---
# <a name="insert-statement-limitations"></a>Limitazioni dell'istruzione INSERT
I dati inseriti viene troncati a destra senza visualizzare alcun avviso se è troppo lunga per rientrare nella colonna.  
  
 Tentativo di inserire un valore non compreso nell'intervallo del tipo di dati di una colonna che fa sì che un valore NULL da inserire nella colonna.  
  
 Quando viene utilizzato un file dBASE, Microsoft Excel, Paradox o Textdriver, inserire una stringa di lunghezza zero in una colonna effettivamente inserisce un valore NULL invece.  
  
 Quando viene utilizzato il driver di Microsoft Excel, se una stringa vuota viene inserita in una colonna, una stringa vuota verrà convertita in un valore NULL. un'istruzione SELECT di ricerca che viene eseguita con una stringa vuota nella clausola WHERE non riuscirà per tale colonna.  
  
 Una tabella non è aggiornabile dal driver Paradox in due condizioni:  
  
-   Quando un indice univoco non è definito sulla tabella. Ciò non vale per una tabella vuota, che può essere aggiornata con una sola riga, anche se un indice univoco non è definito sulla tabella. Se in una tabella vuota che non dispone di un indice univoco viene inserita una riga singola, un'applicazione non è possibile creare un indice univoco o inserire dati aggiuntivi dopo aver inserita la singola riga.  
  
-   Se il motore di Database Borland non è implementato, solo di lettura e aggiungere le istruzioni sono consentite nella tabella Paradox.  
  
 Quando viene usato il driver di testo, i valori NULL sono rappresentati da una stringa con degli zero nei file di lunghezza fissa, ma sono rappresentati da non includere spazi nei file delimitato da virgole. Nella riga seguente che contiene tre campi, ad esempio, il secondo campo è un valore NULL:  
  
```  
"Smith:,, 123  
```  
  
 Quando viene usato il driver di testo, tutti i valori di colonna possono essere riempiti con spazi iniziali. La lunghezza di qualsiasi riga deve essere minore o uguale a 65,543 byte.
