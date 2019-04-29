---
title: A livello di chiamata interfacce | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 99ec2d9a1995502a4bfd96dad02157ccc6574f6c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62735007"
---
# <a name="call-level-interfaces"></a>Call Level Interface
La tecnica finale per l'invio di istruzioni SQL per il sistema DBMS è tramite un'interfaccia a livello di chiamata (comando). Un'interfaccia a livello di chiamata fornisce una libreria di funzioni di sistema DBMS che può essere chiamato dal programma dell'applicazione. In questo modo, invece di tentare di blend SQL con un altro linguaggio di programmazione, un'interfaccia a livello di chiamata è simile alle librerie di routine maggior parte dei programmatori sono abituati a usare, ad esempio la stringa, i/o o delle librerie matematiche in C. si noti che DBMS che supportano SQL incorporato esiste già un'interfaccia a livello di chiamata, le chiamate a cui vengono generate dallo strumento di precompilazione. Tuttavia, queste chiamate sono soggette a modifiche senza preavviso e non documentate.  
  
 Call-level Interface vengono comunemente usati nelle architetture client/server, in cui il programma dell'applicazione (client) si trova in un unico computer e il sistema DBMS (server) si trova in un computer diverso. L'applicazione chiama le funzioni dell'interfaccia della riga nel sistema locale, e tali chiamate vengono inviate attraverso la rete per il sistema DBMS per l'elaborazione.  
  
 Un'interfaccia a livello di chiamata è simile a istruzioni SQL dinamiche, in quanto le istruzioni SQL vengono passate al sistema DBMS per l'elaborazione in fase di esecuzione, ma differisce da SQL incorporate nel suo complesso in quanto sono presenti istruzioni SQL incorporate e nessun precompilatore è obbligatorio.  
  
 Usa in genere un'interfaccia a livello di chiamata prevede i passaggi seguenti:  
  
1.  L'applicazione chiama una funzione della riga di comando per la connessione per il sistema DBMS.  
  
2.  L'applicazione si basa un'istruzione SQL e lo inserisce in un buffer. Chiama quindi uno o più funzioni dell'interfaccia della riga per inviare l'istruzione per il sistema DBMS per la preparazione e l'esecuzione.  
  
3.  Se l'istruzione è un'istruzione SELECT, l'applicazione chiama una funzione della riga di comando per restituire i risultati nel buffer dell'applicazione. In genere, questa funzione restituisce una riga o una colonna di dati alla volta.  
  
4.  L'applicazione chiama una funzione della riga di comando per disconnettersi dal sistema DBMS.
