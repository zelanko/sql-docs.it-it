---
title: SQLSetConnectAttr (libreria di cursori) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLSetConnectAttr function [ODBC], Cursor Library
ms.assetid: 6f70bbd0-a057-49ef-8b05-4c80b58fc6e6
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 73d1369a2bce0327ac3367d33f0894bdcfab8205
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68125576"
---
# <a name="sqlsetconnectattr-cursor-library"></a>SQLSetConnectAttr (libreria di cursori)
> [!IMPORTANT]  
>  Questa funzionalità verrà rimossa in una versione futura di Windows. Evitare di utilizzarla nelle nuove attività di sviluppo e pianificare la modifica delle applicazioni che utilizzano attualmente questa funzionalità. Microsoft consiglia di usare le funzionalità del driver del cursore.  
  
 In questo argomento viene illustrato l'utilizzo dei **SQLSetConnectAttr** funzione nella libreria di cursori. Per informazioni generali sul **SQLSetConnectAttr**, vedere [funzione SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md).  
  
 Un'applicazione chiama **SQLSetConnectAttr** con l'attributo SQL_ATTR_ODBC_CURSORS per specificare se la libreria di cursori viene sempre usata, utilizzata se il driver non supporta i cursori scorrevoli o mai utilizzata. La libreria di cursori si presuppone che un driver supporta cursori scorrevoli se per il tipo di informazioni SQL_STATIC_CURSOR_ATTRIBUTES1 in restituisce SQL_CA1_RELATIVE **SQLGetInfo**.  
  
 L'applicazione deve chiamare **SQLSetConnectAttr** per specificare l'utilizzo della libreria di cursori dopo aver chiamato **SQLAllocHandle** con un *HandleType* SQL_HANDLE_DBC per allocare la connessione e prima che si connette all'origine dati. Se un'applicazione chiama **SQLSetConnectAttr** con l'attributo SQL_ATTR_ODBC_CURSORS mentre la connessione è ancora attiva, la libreria di cursori restituisce un errore.  
  
 Per impostare un attributo di istruzione supportato dalla libreria di cursori per tutte le istruzioni associate a una connessione, un'applicazione deve chiamare **SQLSetConnectAttr** per tale attributo dell'istruzione dopo la connessione all'origine dati e prima di esso Apre il cursore. Se un'applicazione chiama **SQLSetConnectAttr** con un'istruzione di attributo e un cursore è aperto in un'istruzione associata alla connessione, l'attributo di istruzione non essere applicato a tale istruzione fino a quando il cursore viene chiuso e riaperto.
