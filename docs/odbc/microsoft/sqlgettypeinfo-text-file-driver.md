---
title: SQLGetTypeInfo (Driver per i file di testo) Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLGetTypeInfo function [ODBC], Text File Driver
- text file driver [ODBC], SQLGetTypeInfo
ms.assetid: 05a58975-093c-4bd9-bd72-b5f0026a6e36
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7b70b58e4760959db102450b5f8b7beed042df95
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81295001"
---
# <a name="sqlgettypeinfo-text-file-driver"></a>SQLGetTypeInfo (driver file di testo)
> [!NOTE]  
>  In questo argomento vengono fornite informazioni specifiche del driver di file di testo. Per informazioni generali su questa funzione, vedere l'argomento appropriato in [Riferimento all'API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Il nome del tipo (TYPE_NAME) restituito nella tabella prodotta da **SQLGetTypeInfo** sarà il nome più comunemente utilizzato dall'origine dati.  
  
 SQL_ALL_EXCEPT_LIKE verrà restituita nella colonna SEARCHABLE per i tipi di dati Byte, Counter, Double, Single, Long e Short. (La funzionalità LIKE può essere ottenuta convertendo il valore in un carattere utilizzando le funzioni di conversione canonica ODBC, quindi eseguendo il confronto.)  
  
 Quando viene utilizzato il driver di testo, **SQLGetTypeInfo** restituisce un valore di CASE_SENSITIVE FALSE per i tipi di dati di testo (CHAR e LONGCHAR), quando i tipi di dati sono effettivamente tra maiuscole e minuscole.
