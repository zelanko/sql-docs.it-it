---
title: Applicazioni personalizzate | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- interoperability [ODBC], custom applications
- custom applications [ODBC]
- interoperability [ODBC], levels
ms.assetid: f28178d9-ecd6-4e8c-9644-9bb624999dcb
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: df00a748ee4d5e3a63b32c95449417a1057b58e1
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81305282"
---
# <a name="custom-applications"></a>Applicazioni personalizzate
Nelle applicazioni personalizzate viene in genere eseguita un'attività specifica per alcuni DBMS. Ad esempio, un'applicazione potrebbe recuperare i dati da un singolo DBMS e generare un report oppure trasferire dati tra diversi DBMS. Ciò che queste applicazioni hanno in comune è che questi DBMS sono noti prima che l'applicazione venga scritta ed è improbabile che si modifichino per la durata dell'applicazione.  
  
 L'applicazione personalizzata richiede pertanto un'interoperabilità minima o nulla. Lo sviluppatore di applicazioni può scegliere un singolo driver per ogni DBMS e il codice direttamente a tali driver. L'applicazione può contenere in modo sicuro codice specifico del driver per sfruttare le funzionalità di tali driver e potrebbe anche effettuare chiamate all'API del database nativo per utilizzare la funzionalità non supportata da ODBC.  
  
 Il principale problema di interoperabilità della maggior parte delle applicazioni personalizzate consiste nel fatto che i sistemi DBMS di destinazione cambieranno in futuro. In tal caso, questo processo può essere semplificato scrivendo codice più interoperativo per iniziare. Tuttavia, la modifica di DBMS è rara e in genere comporta una grande quantità di lavoro. Per questo motivo, gli sviluppatori di applicazioni personalizzate scelgono raramente di aumentare l'interoperabilità a scapito della funzionalità. in genere scelgono di ricodificare tale funzionalità quando cambiano DBMS.
