---
title: SQLFetch (libreria di cursori) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLFetch function [ODBC], Cursor Library
ms.assetid: 35a0d493-778b-4fb1-84ee-a13540e2fe0e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2cb829f065421a13d3c7df06c670808bc3d9d77c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68064429"
---
# <a name="sqlfetch-cursor-library"></a>SQLFetch (libreria di cursori)
> [!IMPORTANT]  
>  Questa funzionalità verrà rimossa in una versione futura di Windows. Evitare di utilizzarla nelle nuove attività di sviluppo e pianificare la modifica delle applicazioni che utilizzano attualmente questa funzionalità. Microsoft consiglia di usare le funzionalità del driver del cursore.  
  
 In questo argomento viene illustrato l'utilizzo dei **SQLFetch** funzione nella libreria di cursori. Per informazioni generali sul **SQLFetch**, vedere [SQLFetch-funzione](../../../odbc/reference/syntax/sqlfetch-function.md).  
  
 Quando viene usata la libreria di cursori, le chiamate a **SQLFetch** ReadContentAsBase64 e ReadContentAsBinHex con chiamate a uno **SQLFetchScroll** oppure **SQLExtendedFetch**.  
  
 Se **SQLFetch** viene chiamato con SQL_ATTR_ROW_ARRAY_SIZE impostata su un valore maggiore di 1, la libreria di cursori supererà la chiamata del driver. Se il driver è un'API ODBC 2. *x* driver, le dimensioni del set di righe verranno ignorata e la chiamata a **SQLFetch** restituirà una singola riga di dati.  
  
 Se la libreria di cursori viene usata con un ODBC 2. *x* driver, un binding di offset (come definito nell'attributo di istruzione SQL_ATTR_ROW_BIND_OFFSET_PTR) non è utilizzato quando **SQLFetch** viene chiamato.  
  
 Quando viene caricata la libreria di cursori, un'applicazione non è possibile chiamare **SQLFetch** recuperare colonne di segnalibri. La libreria di cursori passa la chiamata a **SQLFetch** tramite il driver, ma la funzione vengono intercettate chiamate per abilitare i segnalibri e associare la colonna del segnalibro dalla libreria di cursori.
