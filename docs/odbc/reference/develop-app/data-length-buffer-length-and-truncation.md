---
title: Lunghezza dei dati, lunghezza del buffer e troncamento Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data buffers [ODBC], length
- data length [ODBC]
- truncating data [ODBC]
- length of data buffers [ODBC]
- buffers [ODBC], length
ms.assetid: 2825c6e7-b9ff-42fe-84fc-7fb39728ac5d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b2e7b8d1e60cd83594509c2ab5cbc24e04546eca
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305231"
---
# <a name="data-length-buffer-length-and-truncation"></a>Lunghezza dei dati, lunghezza del buffer e troncamento
La lunghezza dei *dati* è la lunghezza in byte dei dati come verrebbe archiviata nel buffer di dati dell'applicazione, non come viene archiviata nell'origine dati. Questa distinzione è importante perché i dati vengono spesso archiviati in tipi diversi nel buffer di dati rispetto all'origine dati. Pertanto, per i dati inviati all'origine dati, questa è la lunghezza in byte dei dati prima della conversione nel tipo dell'origine dati. Per i dati recuperati dall'origine dati, si tratta della lunghezza in byte dei dati dopo la conversione nel tipo del buffer di dati e prima che venga eseguito il troncamento.  
  
 Per i dati a lunghezza fissa, ad esempio un numero intero o una struttura di data, la lunghezza in byte dei dati è sempre la dimensione del tipo di dati. In generale, le applicazioni allocano un buffer di dati della dimensione del tipo di dati. Se l'applicazione alloca un buffer più piccolo, le conseguenze non sono definite perché il driver presuppone che il buffer di dati sia la dimensione del tipo di dati e non tronca i dati per adattarli a un buffer più piccolo. Se l'applicazione alloca un buffer più grande, lo spazio aggiuntivo non viene mai utilizzato.  
  
 Per i dati a lunghezza variabile, ad esempio i dati di tipo carattere o binario, è importante riconoscere che la lunghezza in byte dei dati è separata e spesso diversa dalla lunghezza in byte del buffer. La relazione di queste due lunghezze è descritta nella sezione [Buffer.](../../../odbc/reference/develop-app/buffers.md) Se la lunghezza in byte dei dati è maggiore della lunghezza in byte del buffer, il driver tronca i dati recuperati alla lunghezza in byte del buffer e restituisce SQL_SUCCESS_WITH_INFO con SQLSTATE 01004 (dati troncati). Tuttavia, la lunghezza dei byte restituiti è la lunghezza dei dati non troncati.  
  
 Si supponga, ad esempio, che un'applicazione allochi 50 byte per un buffer di dati binari. Se il driver dispone di 10 byte di dati binari da restituire, restituisce quei 10 byte nel buffer. La lunghezza in byte dei dati è 10 e la lunghezza in byte del buffer è 50. Se il driver dispone di 60 byte di dati binari da restituire, tronca i dati a 50 byte, restituisce tali byte nel buffer e restituisce SQL_SUCCESS_WITH_INFO. La lunghezza in byte dei dati è 60 (la lunghezza prima del troncamento) e la lunghezza in byte del buffer è ancora 50.  
  
 Viene creato un record di diagnostica per ogni colonna troncata. Poiché il driver richiede tempo per creare questi record e per l'applicazione per elaborarli, il troncamento può ridurre le prestazioni. In genere, un'applicazione può evitare questo problema allocando buffer di dimensioni sufficienti, anche se ciò potrebbe non essere possibile quando si lavora con dati lunghi. Quando si verifica il troncamento dei dati, l'applicazione può talvolta allocare un buffer più grande e recuperare nuovamente i dati; questo non è vero in tutti i casi. Se si verifica il troncamento durante il recupero dei dati con chiamate a **SQLGetData**, l'applicazione non deve chiamare **SQLGetData** per i dati già restituiti; Per ulteriori informazioni, vedere [Recupero di dati lunghi](../../../odbc/reference/develop-app/getting-long-data.md).
