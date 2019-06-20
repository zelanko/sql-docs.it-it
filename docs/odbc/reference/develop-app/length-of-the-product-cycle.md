---
title: Lunghezza del ciclo del prodotto | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- interoperability [ODBC], product cycle
- length of the product cycle [ODBC]
ms.assetid: 4d08d886-6d8b-40fd-8544-13032f4bf6c7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2c8a5b88f3fdca03be7740ba086e7ff61edbf684
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63127220"
---
# <a name="length-of-the-product-cycle"></a>Lunghezza del ciclo del prodotto
La domanda sull'interoperabilità finale è ora. Sviluppa un'applicazione interoperativa in genere richiede più di sviluppare uno noninteroperable. Il motivo è che l'applicazione deve controllare le funzionalità DBMS, eseguire le stesse attività in modo diverso per i diversi DBMS, aggirare le funzionalità supportate da alcuni DBMS, ma non altri e così via.  
  
 Oltre a tempi di sviluppo, è necessario considerare ciclo di vita del prodotto. Se l'applicazione è progettata per essere usato una sola volta, ad esempio un'applicazione di trasferimento dei dati durante la migrazione da un DBMS a altro, è inutile in modo interoperativo. L'applicazione verrà usata una sola volta e rimossi.  
  
 Se l'applicazione verrà esiste per molto tempo, potrebbe essere più facile da gestire come un'applicazione interoperativa. Questo vale anche per le applicazioni personalizzate con un DBMS singolo come destinazione. Il motivo è che interoperabile codice Usa un sottoinsieme limitato delle funzionalità del database. Il driver è necessario per mantenere le funzionalità disponibili, anche in caso di modifiche al sistema DBMS sottostante. Di conseguenza, codice interoperativa può essere spostato il carico di lavoro di copia con le modifiche per il sistema DBMS dallo sviluppatore dell'applicazione per gli sviluppatori di driver.
