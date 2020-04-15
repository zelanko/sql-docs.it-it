---
title: Proprietà Multithreading . Documenti Microsoft
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c10d1b401ac780d24184c4c2337199e99973e916
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302416"
---
# <a name="multithreading"></a>Multithreading
Nei sistemi operativi multithread, i driver devono essere thread-safe. In altre parte, è possibile che le applicazioni utilizzino lo stesso handle su più thread. Il modo in cui questo viene ottenuto è specifico del driver ed è probabile che i driver serializzeranno tutti i tentativi di utilizzare contemporaneamente lo stesso handle su due thread diversi.  
  
 Le applicazioni usano in genere più thread anziché l'elaborazione asincrona. L'applicazione crea un thread separato, chiama una funzione ODBC su di esso e quindi continua l'elaborazione nel thread principale. Anziché dover eseguire continuamente il polling della funzione asincrona, come nel caso in cui viene utilizzato l'attributo di istruzione SQL_ATTR_ASYNC_ENABLE, l'applicazione può semplicemente consentire il completamento del thread appena creato.  
  
 Le funzioni che accettano un handle di istruzione e sono in esecuzione su un thread possono essere annullate chiamando **SQLCancel** con lo stesso handle di istruzione da un altro thread. Anche se i driver non devono serializzare l'utilizzo di **SQLCancel** in questo modo, non vi è alcuna garanzia che la chiamata **SQLCancel** effettivamente annullare la funzione in esecuzione sull'altro thread.
