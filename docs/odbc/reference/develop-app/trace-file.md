---
title: 'File di traccia : Documenti Microsoft'
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
ms.openlocfilehash: ddd0ee24649592cf4a1a296a51404334145a3bab
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298058"
---
# <a name="trace-file"></a>File di traccia
Un'applicazione specifica il file di traccia impostando la parola chiave **TraceFile** nella voce del Registro di sistema Odbc.ini o chiamando **SQLSetConnectAttr** con l'attributo di connessione SQL_ATTR_TRACEFILE. Se il file non esiste quando la tracciatura è abilitata, Gestione Driver creerà il file. Ogni applicazione deve avere un proprio file di traccia dedicato per evitare conflitti. Un'applicazione può utilizzare più di un file di traccia; programma di installazione di un'applicazione in grado di fornire all'utente una scelta di file di traccia. Se la tracciatura è abilitata in modo dinamico, un'applicazione può anche visualizzare i risultati della traccia, anziché registrare nel file di traccia.  
  
 Il file di traccia fornisce un registro di ogni chiamata di funzione ODBC con i tipi di dati e i valori di tutti gli argomenti. Registra tutte le funzioni di input e registra tutte le funzioni restituite con codici restituiti e stati di errore.  
  
 In ODBC *3.x*, i parametri per le funzioni di connessione non vengono forniti alla DLL di traccia.
