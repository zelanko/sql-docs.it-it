---
title: Lunghezza dei dati, lunghezza del Buffer e troncamento | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 8586157237db1158587e3c39f1320b78d8251fb5
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68081476"
---
# <a name="data-length-buffer-length-and-truncation"></a>Lunghezza dei dati, lunghezza del buffer e troncamento
Il *lunghezza dei dati* è la lunghezza in byte dei dati come verranno archiviati nel buffer di dati dell'applicazione, non quando vengono archiviato nell'origine dati. Questa distinzione è importante perché i dati vengono spesso archiviati in tipi diversi nel buffer di dati più nell'origine dati. Pertanto, per i dati inviati all'origine dati, questa è la lunghezza in byte dei dati prima della conversione al tipo dell'origine dati. Per i dati recuperati dall'origine dati, questa è la lunghezza in byte dei dati dopo la conversione al tipo di buffer di dati e prima che venga eseguita qualsiasi troncamento.  
  
 Per i dati a lunghezza fissa, ad esempio un numero intero o una struttura di data, la lunghezza in byte dei dati è sempre la dimensione del tipo di dati. In generale, le applicazioni allocare un buffer di dati che rappresenta la dimensione del tipo di dati. Se l'applicazione consente di allocare un buffer più piccolo, le conseguenze sono definite in quanto il driver presuppone che il buffer dei dati è la dimensione del tipo di dati e non tronca i dati per un buffer più piccoli. Se l'applicazione consente di allocare un buffer più grande, lo spazio aggiuntivo non viene mai usato.  
  
 Per i dati a lunghezza variabile, ad esempio carattere o dati binari, è importante tenere presente che la lunghezza in byte dei dati è separato dal e spesso diverso da quello la lunghezza in byte del buffer. La relazione di questi due lunghezze è descritta nel [buffer](../../../odbc/reference/develop-app/buffers.md) sezione. Se la lunghezza in byte dei dati è maggiore della lunghezza di byte del buffer, il driver causa il troncamento dei dati recuperati per la lunghezza in byte del buffer e viene restituito SQL_SUCCESS_WITH_INFO con SQLSTATE 01004 (dati troncati). Tuttavia, la lunghezza di byte restituita è la lunghezza dei dati non troncati.  
  
 Si supponga, ad esempio, che un'applicazione alloca 50 byte per un buffer di dati binari. Se il driver ha 10 byte di dati binari da restituire, restituisce li 10 byte nel buffer. La lunghezza in byte dei dati è 10 e la lunghezza in byte del buffer è 50. Se il driver ha 60 byte di dati binari da restituire, troncamento dei dati per 50 byte, restituisce i byte nel buffer e viene restituito SQL_SUCCESS_WITH_INFO. La lunghezza in byte dei dati è 60 (lunghezza della prima del troncamento) e la lunghezza in byte del buffer è ancora 50.  
  
 Per ogni colonna che viene troncato viene creato un record di diagnostica. Poiché occorre tempo per il driver creare questi record e per l'applicazione per l'elaborazione, il troncamento può influire negativamente sulle prestazioni. In genere, un'applicazione può evitare questo problema tramite l'allocazione di buffer di dimensioni sufficienti, anche se ciò potrebbe non essere possibile quando si lavora con dati di tipo long. Quando si verifica un troncamento dei dati, l'applicazione può talvolta allocare un buffer più grande e recupera di nuovo i dati. Ciò non vale in tutti i casi. Se si verifica un troncamento durante il recupero dei dati con le chiamate a **SQLGetData**, l'applicazione non è necessario chiamare **SQLGetData** per i dati che sono già stati restituiti; per altre informazioni, vedere [introduzione Dati di tipo long](../../../odbc/reference/develop-app/getting-long-data.md).
