---
title: Proprietà Generic Applications Documenti Microsoft
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305552"
---
# <a name="generic-applications"></a>Applicazioni generiche
Le applicazioni generiche talvolta eseguono un'attività hardcoded, ad esempio un foglio di calcolo che recupera i dati da un database. Possono inoltre eseguire un'ampia gamma di attività definite dall'utente, ad esempio un'applicazione di query generica che consente all'utente di immettere ed eseguire un'istruzione SQL. Ciò che le applicazioni generiche hanno in comune è che devono lavorare con una varietà di DBS diversi e che lo sviluppatore non sa in anticipo quali saranno questi DBS.  
  
 Pertanto, le applicazioni generiche devono essere altamente interoperabili. Lo sviluppatore deve effettuare molte scelte, scambiando l'interoperabilità per le funzionalità e deve scrivere codice che prevede che i driver supportino un'ampia gamma di funzionalità. Mentre le applicazioni generiche potrebbero essere sintonizzati per funzionare con DBMS popolari, raramente contengono codice specifico del driver o DBMS.
