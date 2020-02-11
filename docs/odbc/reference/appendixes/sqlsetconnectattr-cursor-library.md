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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68125576"
---
# <a name="sqlsetconnectattr-cursor-library"></a>SQLSetConnectAttr (libreria di cursori)
> [!IMPORTANT]  
>  Questa funzionalità verrà rimossa in una versione futura di Windows. Evitare di utilizzare questa funzionalità nelle nuove attività di sviluppo e pianificare la modifica delle applicazioni che attualmente utilizzano questa funzionalità. Microsoft consiglia di utilizzare la funzionalità di cursore del driver.  
  
 In questo argomento viene illustrato l'utilizzo della funzione **SQLSetConnectAttr** nella libreria di cursori. Per informazioni generali su **SQLSetConnectAttr**, vedere [funzione SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md).  
  
 Un'applicazione chiama **SQLSetConnectAttr** con l'attributo SQL_ATTR_ODBC_CURSORS per specificare se la libreria di cursori viene sempre utilizzata, utilizzata se il driver non supporta i cursori scorrevoli o mai utilizzato. La libreria di cursori presuppone che un driver supporti i cursori scorrevoli se restituisce SQL_CA1_RELATIVE per il tipo di informazioni SQL_STATIC_CURSOR_ATTRIBUTES1 in **SQLGetInfo**.  
  
 L'applicazione deve chiamare **SQLSetConnectAttr** per specificare l'utilizzo della libreria di cursori dopo aver chiamato **SQLAllocHandle** con un *HandleType* di SQL_HANDLE_DBC per allocare la connessione e prima di connettersi all'origine dati. Se un'applicazione chiama **SQLSetConnectAttr** con l'attributo SQL_ATTR_ODBC_CURSORS mentre la connessione è ancora attiva, la libreria di cursori restituisce un errore.  
  
 Per impostare un attributo di istruzione supportato dalla libreria di cursori per tutte le istruzioni associate a una connessione, un'applicazione deve chiamare **SQLSetConnectAttr** per l'attributo dell'istruzione dopo la connessione all'origine dati e prima dell'apertura del cursore. Se un'applicazione chiama **SQLSetConnectAttr** con un attributo di istruzione e un cursore è aperto in un'istruzione associata alla connessione, l'attributo dell'istruzione non verrà applicato a tale istruzione finché il cursore non viene chiuso e riaperto.
