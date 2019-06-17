---
title: SQLGetTypeInfo (dBASE Driver) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLGetTypeInfo function [ODBC], dBASE Driver
- DBase driver [ODBC], SQLGetTypeInfo
ms.assetid: 6e9ce02b-97c7-4c1a-91e0-829df7459c84
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 90bfbe29fd011f8b62527854f0ca5a179d8f63cc
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63224525"
---
# <a name="sqlgettypeinfo-dbase-driver"></a>SQLGetTypeInfo (driver dBASE)
> [!NOTE]  
>  In questo argomento fornisce informazioni specifiche del Driver dBASE. Per informazioni generali su questa funzione, vedere l'argomento appropriato nel [riferimento all'API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Il nome del tipo (TYPE_NAME) restituita nella tabella prodotta dalle **SQLGetTypeInfo** corrisponderà al nome più comunemente utilizzato dall'origine dei dati.  
  
 SQL_ALL_EXCEPT_LIKE verrà restituito nella colonna di ricerca per Byte, del contatore, Double, i tipi di dati singolo, lunghi e brevi. (La funzionalità simile può essere ottenuta convertendo il valore in un carattere utilizzando le funzioni di conversione canonica ODBC, quindi eseguire il confronto).
