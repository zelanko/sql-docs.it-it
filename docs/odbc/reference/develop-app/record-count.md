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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8f8b0a6fc7aa5765d9373af33ab4fac0a4a07aac
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63151233"
---
# <a name="record-count"></a>Conteggio record
Il campo dell'intestazione di un descrittore SQL_DESC_COUNT è l'indice in base 1 del record con numero più alto che contiene i dati. Questo campo non è un conteggio di tutte le colonne o parametri associati. Quando si alloca un descrittore, il valore iniziale di SQL_DESC_COUNT è 0.  
  
 Il driver accetta qualsiasi azione necessaria per allocare e mantenere la risorsa di archiviazione necessarie per contenere le informazioni del descrittore. L'applicazione in modo non esplicito specificare le dimensioni di un descrittore né allocare nuovi record. Quando l'applicazione fornisce le informazioni per un record del descrittore il cui numero è superiore al valore di SQL_DESC_COUNT, il driver aumenta automaticamente SQL_DESC_COUNT. Quando l'applicazione viene disassociato il record del descrittore con numero più alto, il driver si ridotta automaticamente SQL_DESC_COUNT per contenere il numero del record rimanenti più alto associato.
