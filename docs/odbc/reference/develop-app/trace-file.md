---
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8138a0cef3a28d31242a74162f0024e28e8b8fe9
ms.sourcegitcommit: 56b963446965f3a4bb0fa1446f49578dbff382e0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2019
ms.locfileid: "67793934"
---
# <a name="trace-file"></a>File di traccia
Un'applicazione specifica nel file di traccia impostando il **TraceFile** parola chiave nella voce del Registro di sistema ODBC. ini o chiamando **SQLSetConnectAttr** con l'attributo di connessione SQL_ATTR_TRACEFILE. Se il file non esiste quando la traccia è abilitata, gestione Driver creerà il file. Ogni applicazione deve avere un proprio file di traccia dedicato per evitare conflitti. Un'applicazione può utilizzare più di un file di traccia. programma di installazione di un'applicazione può fornire all'utente con una scelta dei file di traccia. Se la traccia è abilitata in modo dinamico, un'applicazione può anche visualizzare i risultati della traccia, piuttosto che la registrazione nel file di traccia.  
  
 Il file di traccia fornisce i valori di tutti gli argomenti e un log di ogni chiamata di funzione ODBC con i tipi di dati. Registra le funzioni di tutti gli input e registra tutte le funzioni restituite con i codici restituiti e gli stati di errore.  
  
 In ODBC *3.x*, parametri alle funzioni di connessione non disponibili per la DLL di traccia.
