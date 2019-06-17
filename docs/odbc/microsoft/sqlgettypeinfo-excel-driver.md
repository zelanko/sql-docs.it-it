---
title: SQLGetTypeInfo (Excel Driver) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLGetTypeInfo function [ODBC], Excel Driver
- Excel driver [ODBC], SQLGetTypeInfo
ms.assetid: 708845be-e6a1-4677-8113-c52819a43fa4
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ac7fe52ffdbb090e0b63a972e77c1a7f7a756446
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63034908"
---
# <a name="sqlgettypeinfo-excel-driver"></a>SQLGetTypeInfo (driver Excel)
> [!NOTE]  
>  In questo argomento fornisce informazioni specifiche del Driver Excel. Per informazioni generali su questa funzione, vedere l'argomento appropriato nel [riferimento all'API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Il nome del tipo (TYPE_NAME) restituita nella tabella prodotta dalle **SQLGetTypeInfo** corrisponderà al nome più comunemente utilizzato dall'origine dei dati.  
  
 SQL_ALL_EXCEPT_LIKE verrà restituito nella colonna di ricerca per Byte, del contatore, Double, i tipi di dati singolo, lunghi e brevi. (La funzionalità simile può essere ottenuta convertendo il valore in un carattere utilizzando le funzioni di conversione canonica ODBC, quindi eseguire il confronto).  
  
 Quando viene usato il driver di Microsoft Excel, i nomi di tipo ODBC vengono restituiti nella colonna TYPE_NAME restituito da **SQLGetTypeInfo**.
