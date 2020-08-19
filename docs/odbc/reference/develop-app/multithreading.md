---
description: Multithreading
title: Multithreading | Microsoft Docs
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
ms.openlocfilehash: 470a3d3a4d76ae038e3c80b9aa9b93dfd1d0ed79
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429243"
---
# <a name="multithreading"></a>Multithreading
Nei sistemi operativi multithread i driver devono essere thread-safe. Ovvero, è necessario che le applicazioni usino lo stesso handle in più di un thread. Il modo in cui viene eseguita questa operazione è specifico del driver ed è probabile che i driver serializzano tutti i tentativi di usare simultaneamente lo stesso handle su due thread diversi.  
  
 Le applicazioni utilizzano in genere più thread anziché l'elaborazione asincrona. L'applicazione crea un thread separato, chiama una funzione ODBC su di essa e quindi continua l'elaborazione nel thread principale. Anziché dover eseguire continuamente il polling della funzione asincrona, come nel caso in cui venga utilizzato l'attributo SQL_ATTR_ASYNC_ENABLE Statement, l'applicazione può semplicemente consentire il completamento del thread appena creato.  
  
 Le funzioni che accettano un handle di istruzione e sono in esecuzione in un thread possono essere annullate chiamando **SQLCancel** con lo stesso handle di istruzione da un altro thread. Sebbene i driver non debbano serializzare l'utilizzo di **SQLCancel** in questo modo, non esiste alcuna garanzia che la chiamata di **SQLCancel** elimini effettivamente la funzione in esecuzione sull'altro thread.
