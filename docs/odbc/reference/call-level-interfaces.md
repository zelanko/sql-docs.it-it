---
title: Interfacce a livello di chiamata Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], CLI
- CLI [ODBC], using CLI
- sending SQL statements to DBMS [ODBC]
- SQL [ODBC], CLI
- call-level interface [ODBC], using call-level interface
ms.assetid: 42257bb6-0bf1-4533-a4ef-4a6dd2aecb18
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4288a278f745d533c92d3d45892753ef1a74c2b3
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306542"
---
# <a name="call-level-interfaces"></a>Call Level Interface
La tecnica finale per l'invio di istruzioni SQL al DBMS è tramite un'interfaccia a livello di chiamata (CLI). Un'interfaccia a livello di chiamata fornisce una libreria di funzioni DBMS che possono essere chiamate dal programma applicativo. Pertanto, anziché tentare di fondere SQL con un altro linguaggio di programmazione, un'interfaccia a livello di chiamata è simile alle librerie di routine a cui la maggior parte dei programmatori è abituata a usare, ad esempio le librerie di stringhe, I/O o matematiche in C. Si noti che i DBS che supportano SQL incorporato dispongono già di un'interfaccia a livello di chiamata, le cui chiamate vengono generate dal precompilatore. Tuttavia, queste chiamate sono prive di documenti e soggette a modifiche senza preavviso.  
  
 Le interfacce a livello di chiamata vengono comunemente utilizzate nelle architetture client/server, in cui il programma applicativo (il client) risiede in un computer e il DBMS (il server) risiede in un computer diverso. L'applicazione chiama le funzioni CLI nel sistema locale e tali chiamate vengono inviate attraverso la rete al DBMS per l'elaborazione.  
  
 Un'interfaccia a livello di chiamata è simile a SQL dinamico, in quanto le istruzioni SQL vengono passate al dbMS per l'elaborazione in fase di esecuzione, ma differisce da SQL incorporato nel suo complesso in quanto non sono presenti istruzioni SQL incorporate e non è necessario alcun precompilatore.  
  
 L'utilizzo di un'interfaccia a livello di chiamata prevede in genere i passaggi seguenti:Using a call-level interface typically involves the following steps:  
  
1.  L'applicazione chiama una funzione CLI per connettersi al DBMS.  
  
2.  L'applicazione compila un'istruzione SQL e la inserisce in un buffer. Chiama quindi una o più funzioni CLI per inviare l'istruzione al DBMS per la preparazione e l'esecuzione.  
  
3.  Se l'istruzione è un'istruzione SELECT, l'applicazione chiama una funzione CLI per restituire i risultati nei buffer dell'applicazione. In genere, questa funzione restituisce una riga o una colonna di dati alla volta.  
  
4.  L'applicazione chiama una funzione CLI per disconnettersi dal DBMS.
