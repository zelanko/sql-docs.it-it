---
title: Interfacce a livello di chiamata | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81306542"
---
# <a name="call-level-interfaces"></a>Call Level Interface
La tecnica finale per l'invio di istruzioni SQL al sistema DBMS è tramite un'interfaccia CLI (Call-Level Interface). Un'interfaccia a livello di chiamata fornisce una libreria di funzioni DBMS che possono essere chiamate dal programma applicativo. Quindi, invece di provare a combinare SQL con un altro linguaggio di programmazione, un'interfaccia a livello di chiamata è simile alle librerie di routine che la maggior parte dei programmatori sono abituati a usare, ad esempio la stringa, le operazioni di I/O o le librerie matematiche in C. si noti che i DBMS che supportano SQL embedded hanno già un'interfaccia a livello di chiamata, le chiamate a Tuttavia, queste chiamate non sono documentate e sono soggette a modifiche senza preavviso.  
  
 Le interfacce a livello di chiamata sono comunemente usate nelle architetture client/server, in cui il programma dell'applicazione (il client) risiede in un computer e il sistema DBMS (il server) risiede in un computer diverso. L'applicazione chiama le funzioni dell'interfaccia della riga di comando nel sistema locale e tali chiamate vengono inviate attraverso la rete al sistema DBMS per l'elaborazione.  
  
 Un'interfaccia a livello di chiamata è simile a SQL dinamico, in quanto le istruzioni SQL vengono passate al sistema DBMS per l'elaborazione in fase di esecuzione, ma differisce da SQL embedded nel suo complesso perché non sono presenti istruzioni SQL incorporate e non è richiesto alcun precompilatore.  
  
 L'uso di un'interfaccia a livello di chiamata prevede in genere i passaggi seguenti:  
  
1.  L'applicazione chiama una funzione dell'interfaccia della riga di comando per connettersi al sistema DBMS.  
  
2.  L'applicazione compila un'istruzione SQL e la inserisce in un buffer. Chiama quindi una o più funzioni dell'interfaccia della riga di comando per inviare l'istruzione al sistema DBMS per la preparazione e l'esecuzione.  
  
3.  Se l'istruzione è un'istruzione SELECT, l'applicazione chiama una funzione CLI per restituire i risultati nei buffer dell'applicazione. In genere, questa funzione restituisce una riga o una colonna di dati alla volta.  
  
4.  L'applicazione chiama una funzione CLI per disconnettersi dal sistema DBMS.
