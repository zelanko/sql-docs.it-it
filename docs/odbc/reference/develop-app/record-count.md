---
title: Conteggio record | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- record count [ODBC]
- descriptors [ODBC], record count
ms.assetid: 46eec3cc-0ecc-4980-9020-fb74a9af5730
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 28e503ae4602d87fc9138ed018ee1e95f135ec57
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81281817"
---
# <a name="record-count"></a>Conteggio record
Il SQL_DESC_COUNT campo di intestazione di un descrittore è l'indice in base uno del record con il numero più alto che contiene i dati. Questo campo non è un conteggio di tutte le colonne o i parametri associati. Quando si alloca un descrittore, il valore iniziale di SQL_DESC_COUNT è 0.  
  
 Il driver esegue qualsiasi azione necessaria per allocare e gestire qualsiasi spazio di archiviazione necessario per mantenere le informazioni sul descrittore. L'applicazione non specifica in modo esplicito le dimensioni di un descrittore né alloca i nuovi record. Quando l'applicazione fornisce informazioni per un record di descrittore il cui numero è maggiore del valore di SQL_DESC_COUNT, il driver aumenta automaticamente SQL_DESC_COUNT. Quando l'applicazione annulla il binding del record del descrittore con il numero più alto, il driver diminuisce automaticamente SQL_DESC_COUNT in modo da contenere il numero del record più alto rimanente associato.
