---
title: Il multithreading | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC drivers [ODBC], thread-safe
- thread-safe drivers [ODBC]
- multithreaded applications [ODBC]
ms.assetid: cdfebdf5-12ff-4e28-8055-41f49b77f664
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1a16262d562ca2088f38cd863a6f44e537e65d40
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63254213"
---
# <a name="multithreading"></a>Multithreading
Nei sistemi operativi con multithreading, i driver devono essere thread-safe. Vale a dire, deve essere possibile usare lo stesso handle su più thread delle applicazioni. Come si ottiene questo risultato è specifico del driver ed è probabile che i driver serializzerà qualsiasi tentativo di utilizzare contemporaneamente lo stesso handle su due thread diversi.  
  
 Le applicazioni usano in genere più thread anziché l'elaborazione asincrona. L'applicazione crea un thread separato, chiama una funzione ODBC su di esso e quindi continuata l'elaborazione sul thread principale. Anziché dover continuamente il polling di funzione asincrona, come avviene quando viene utilizzato l'attributo di istruzione SQL_ATTR_ASYNC_ENABLE, l'applicazione può lasciare il thread appena creato fine.  
  
 Le funzioni che accettano un handle di istruzione e sono in esecuzione in un unico thread possono essere annullate chiamando **SQLCancel** con la stessa istruzione gestire da un altro thread. Anche se i driver non dovrebbe essere serializzato il ricorso **SQLCancel** in questo modo, non c'è garanzia che la chiamata **SQLCancel** effettivamente annullerà la funzione in esecuzione in altri thread.
