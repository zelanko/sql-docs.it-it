---
title: SQLSetConnectAttr (Libreria cursore) Documenti Microsoft
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a87c85d727fb9eb2fc27613b9eecd3fe0ec51b58
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300541"
---
# <a name="sqlsetconnectattr-cursor-library"></a>SQLSetConnectAttr (libreria di cursori)
> [!IMPORTANT]  
>  Questa funzionalità verrà rimossa in una versione futura di Windows. Evitare di utilizzare questa funzionalità nelle nuove attività di sviluppo e pianificare la modifica delle applicazioni che attualmente utilizzano questa funzionalità. Microsoft consiglia di utilizzare la funzionalità del cursore del driver.  
  
 In questo argomento viene illustrato l'utilizzo della funzione **SQLSetConnectAttr** nella libreria di cursori. Per informazioni generali su **SQLSetConnectAttr**, vedere [Funzione SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md).  
  
 Un'applicazione chiama **SQLSetConnectAttr** con il SQL_ATTR_ODBC_CURSORS attributo per specificare se la libreria di cursori viene sempre utilizzata, utilizzata se il driver non supporta cursori scorrevoli o mai utilizzato. La libreria di cursori presuppone che un driver supporti i cursori scorrevoli se restituisce SQL_CA1_RELATIVE per il tipo di informazioni SQL_STATIC_CURSOR_ATTRIBUTES1 in **SQLGetInfo**.  
  
 L'applicazione deve chiamare **SQLSetConnectAttr** per specificare l'utilizzo della libreria di cursori dopo aver chiamato **SQLAllocHandle** con un *HandleType* di SQL_HANDLE_DBC per allocare la connessione e prima che si connetta all'origine dati. Se un'applicazione chiama **SQLSetConnectAttr** con l'attributo SQL_ATTR_ODBC_CURSORS mentre la connessione è ancora attiva, la libreria di cursori restituisce un errore.  
  
 Per impostare un attributo di istruzione supportato dalla libreria di cursori per tutte le istruzioni associate a una connessione, un'applicazione deve chiamare **SQLSetConnectAttr** per tale attributo di istruzione dopo la connessione all'origine dati e prima di aprire il cursore. Se un'applicazione chiama **SQLSetConnectAttr** con un attributo di istruzione e un cursore è aperto su un'istruzione associata alla connessione, l'attributo di istruzione non verrà applicato a tale istruzione fino a quando il cursore non viene chiuso e riaperto.
