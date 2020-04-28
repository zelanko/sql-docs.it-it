---
title: Applicazioni generiche | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- interoperability [ODBC], generic applications
- interoperability [ODBC], levels
- generic applications [ODBC]
ms.assetid: dda2a3c4-76ef-40a6-b3a1-9e95bed61618
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 607676d5370f02ee1d39196bff9261bc897521ee
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81305552"
---
# <a name="generic-applications"></a>Applicazioni generiche
Le applicazioni generiche a volte eseguono un'attività hardcoded, ad esempio un foglio di calcolo che recupera i dati da un database. Potrebbero inoltre eseguire un'ampia gamma di attività definite dall'utente, ad esempio un'applicazione di query generica che consente all'utente di immettere ed eseguire un'istruzione SQL. Per quanto riguarda le applicazioni generiche, è necessario che funzionino con un'ampia gamma di sistemi DBMS diversi e che lo sviluppatore non conosca in anticipo quali saranno i DBMS.  
  
 Pertanto, le applicazioni generiche devono essere altamente interoperative. Lo sviluppatore deve effettuare molte scelte, effettuare il trading di interoperabilità per le funzionalità e deve scrivere codice che prevede che i driver supportino una vasta gamma di funzionalità. Sebbene sia possibile ottimizzare le applicazioni generiche in modo che funzionino con DBMS diffusi, raramente contengono codice specifico del driver o DBMS.
