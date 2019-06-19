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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 59110f66c512845ff5ce1f2f246c05c63fa755b9
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63061499"
---
# <a name="generic-applications"></a>Applicazioni generiche
Applicazioni generiche, talvolta, eseguire un'attività a livello di codice, ad esempio un foglio di calcolo il recupero dei dati da un database. Utente che potrebbe eseguire anche un'ampia gamma di attività definite dall'utente, ad esempio un'applicazione di query standard che consente all'utente di immettere ed eseguire un'istruzione SQL. Quali applicazioni generiche hanno in comune è che devono interagire con un'ampia gamma di DBMS diverso e che lo sviluppatore non conosce in anticipo quali saranno questi DBMS.  
  
 Di conseguenza, le applicazioni generiche devono essere estremamente interoperativi. Lo sviluppatore deve apportare molte le scelte disponibili, commerciali off per le funzionalità di interoperabilità e necessario scrivere codice che prevede che i driver per supportare un'ampia gamma di funzionalità. Mentre le applicazioni generiche potrebbero essere ottimizzate per funzionare con DBMS comuni, raramente contengono codice specifico del driver o specifici del DBMS.
