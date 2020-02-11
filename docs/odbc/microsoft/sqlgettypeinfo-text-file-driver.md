---
title: SQLGetTypeInfo (driver file di testo) | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2659b3251cf77882f3762ce5699c36441e6c8ebc
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "67898643"
---
# <a name="sqlgettypeinfo-text-file-driver"></a>SQLGetTypeInfo (driver file di testo)
> [!NOTE]  
>  In questo argomento vengono fornite informazioni specifiche del driver del file di testo. Per informazioni generali su questa funzione, vedere l'argomento appropriato in informazioni di [riferimento sulle API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Il nome del tipo (TYPE_NAME) restituito nella tabella prodotta da **SQLGetTypeInfo** sarà il nome usato più di frequente dall'origine dati.  
  
 SQL_ALL_EXCEPT_LIKE verrà restituito nella colonna RICERCAbile per i tipi di dati byte, Counter, Double, Single, Long e short. Per ottenere la funzionalità LIKE, è possibile convertire il valore in un carattere usando le funzioni di conversione canoniche ODBC, quindi eseguire il confronto.  
  
 Quando si usa il driver di testo, **SQLGetTypeInfo** restituisce un valore CASE_SENSITIVE false per i tipi di dati di testo (char e LongChar), quando i tipi di dati fanno distinzione tra maiuscole e minuscole.
