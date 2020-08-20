---
description: File di traccia
title: File di traccia | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- trace files [ODBC]
- tracing options [ODBC], trace files
ms.assetid: ec97f949-126f-40a2-b67e-e74520a524cb
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ba45e44baaba68d1c203e83a25c9db305642e6d2
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88487494"
---
# <a name="trace-file"></a>File di traccia
Un'applicazione specifica il file di traccia impostando la parola chiave **TraceFile** nella voce del registro di sistema Odbc.ini o chiamando **SQLSetConnectAttr** con l'attributo di connessione SQL_ATTR_TRACEFILE. Se il file non esiste quando la traccia è abilitata, il file verrà creato da Gestione driver. Ogni applicazione deve disporre di un file di traccia dedicato per evitare conflitti. Un'applicazione può utilizzare più di un file di traccia. il programma di installazione di un'applicazione può fornire all'utente la possibilità di scegliere file di traccia. Se la traccia è abilitata in modo dinamico, un'applicazione può anche visualizzare i risultati della traccia, anziché eseguire la registrazione nel file di traccia.  
  
 Il file di traccia fornisce un log di ogni chiamata di funzione ODBC con i tipi di dati e i valori di tutti gli argomenti. Registra tutte le funzioni di input e registra tutte le funzioni restituite con i codici restituiti e gli Stati di errore.  
  
 In ODBC *3. x*, i parametri per le funzioni di connessione non vengono forniti alla DLL di traccia.
