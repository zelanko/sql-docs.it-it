---
description: Lunghezza dei dati, lunghezza del buffer e troncamento
title: Lunghezza dei dati, lunghezza del buffer e troncamento | Microsoft Docs
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
ms.openlocfilehash: c9a9651f39c1ff4d2c6dc9b691453fb5354c9e1a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88465833"
---
# <a name="data-length-buffer-length-and-truncation"></a>Lunghezza dei dati, lunghezza del buffer e troncamento
La *lunghezza dei dati* corrisponde alla lunghezza in byte dei dati, perché verrebbe archiviata nel buffer di dati dell'applicazione, non come viene archiviata nell'origine dati. Questa distinzione è importante perché i dati sono spesso archiviati in tipi diversi nel buffer dei dati rispetto all'origine dati. Pertanto, per l'invio dei dati all'origine dati, si tratta della lunghezza in byte dei dati prima della conversione al tipo dell'origine dati. Per i dati recuperati dall'origine dati, si tratta della lunghezza in byte dei dati dopo la conversione nel tipo di buffer di dati e prima che venga eseguito il troncamento.  
  
 Per i dati a lunghezza fissa, ad esempio un numero intero o una struttura di data, la lunghezza in byte dei dati corrisponde sempre alla dimensione del tipo di dati. In generale, le applicazioni allocano un buffer di dati che corrisponde alla dimensione del tipo di dati. Se l'applicazione alloca un buffer più piccolo, le conseguenze non sono definite perché il driver presuppone che il buffer dei dati corrisponda alla dimensione del tipo di dati e non tronca i dati in un buffer più piccolo. Se l'applicazione alloca un buffer più grande, lo spazio aggiuntivo non viene mai usato.  
  
 Per i dati a lunghezza variabile, ad esempio dati di tipo carattere o binario, è importante riconoscere che la lunghezza in byte dei dati è separata da e spesso diversa dalla lunghezza in byte del buffer. La relazione di queste due lunghezze è descritta nella sezione [buffer](../../../odbc/reference/develop-app/buffers.md) . Se la lunghezza in byte dei dati è maggiore della lunghezza in byte del buffer, il driver tronca i dati recuperati alla lunghezza in byte del buffer e restituisce SQL_SUCCESS_WITH_INFO con SQLSTATE 01004 (dati troncati). Tuttavia, la lunghezza in byte restituita è la lunghezza dei dati non troncati.  
  
 Si supponga, ad esempio, che un'applicazione allochi 50 byte per un buffer di dati binario. Se il driver ha 10 byte di dati binari da restituire, restituisce questi 10 byte nel buffer. La lunghezza in byte dei dati è 10 e la lunghezza in byte del buffer è 50. Se il driver ha 60 byte di dati binari da restituire, tronca i dati a 50 byte, restituisce tali byte nel buffer e restituisce SQL_SUCCESS_WITH_INFO. La lunghezza in byte dei dati è 60 (la lunghezza prima del troncamento) e la lunghezza in byte del buffer è ancora 50.  
  
 Viene creato un record di diagnostica per ogni colonna troncata. Poiché la creazione di questi record da parte del driver richiede tempo, il troncamento può influire negativamente sulle prestazioni dell'applicazione. In genere, un'applicazione può evitare questo problema allocando buffer sufficientemente grandi, sebbene questo potrebbe non essere possibile quando si utilizzano dati di lunga durata. Quando si verifica il troncamento dei dati, l'applicazione può talvolta allocare un buffer più grande e recuperare i dati. Questa operazione non è valida in tutti i casi. Se si verifica un troncamento durante il recupero dei dati con le chiamate a **SQLGetData**, l'applicazione non deve chiamare **SQLGetData** per i dati che sono già stati restituiti. Per ulteriori informazioni, vedere [recupero di dati Long](../../../odbc/reference/develop-app/getting-long-data.md).
