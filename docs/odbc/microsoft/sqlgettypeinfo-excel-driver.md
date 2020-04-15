---
title: SQLGetTypeInfo (driver di Excel) Documenti Microsoft
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 64befe30be9ed7988e0c9348e9335eb632dd975c
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81295071"
---
# <a name="sqlgettypeinfo-excel-driver"></a>SQLGetTypeInfo (driver Excel)
> [!NOTE]  
>  In questo argomento vengono fornite informazioni specifiche del driver di Excel.This topic provides Excel Driver-specific information. Per informazioni generali su questa funzione, vedere l'argomento appropriato in [Riferimento all'API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Il nome del tipo (TYPE_NAME) restituito nella tabella prodotta da **SQLGetTypeInfo** sarà il nome più comunemente utilizzato dall'origine dati.  
  
 SQL_ALL_EXCEPT_LIKE verrà restituita nella colonna SEARCHABLE per i tipi di dati Byte, Counter, Double, Single, Long e Short. (La funzionalità LIKE può essere ottenuta convertendo il valore in un carattere utilizzando le funzioni di conversione canonica ODBC, quindi eseguendo il confronto.)  
  
 Quando viene utilizzato il driver di Microsoft Excel, i nomi dei tipi ODBC vengono restituiti nella colonna TYPE_NAME restituita da **SQLGetTypeInfo**.
