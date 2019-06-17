---
title: SQLGetTypeInfo (Driver Paradox) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLGetTypeInfo function [ODBC], Paradox Driver
- Paradox driver [ODBC], SQLGetTypeInfo
ms.assetid: e65063c7-ba9e-4cf0-ac13-4bb5bd2937db
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 20b5776b5b0e1490ef31ff07d1876afef326db9b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63284983"
---
# <a name="sqlgettypeinfo-paradox-driver"></a>SQLGetTypeInfo (driver Paradox)
> [!NOTE]  
>  In questo argomento fornisce informazioni specifiche del Driver Paradox. Per informazioni generali su questa funzione, vedere l'argomento appropriato nel [riferimento all'API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Il nome del tipo (TYPE_NAME) restituita nella tabella prodotta dalle **SQLGetTypeInfo** corrisponderà al nome più comunemente utilizzato dall'origine dei dati.  
  
 SQL_ALL_EXCEPT_LIKE verrà restituito nella colonna di ricerca per Byte, del contatore, Double, i tipi di dati singolo, lunghi e brevi. (La funzionalità simile può essere ottenuta convertendo il valore in un carattere utilizzando le funzioni di conversione canonica ODBC e quindi eseguire il confronto.)
