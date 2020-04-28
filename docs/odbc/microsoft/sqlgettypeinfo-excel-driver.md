---
title: SQLGetTypeInfo (driver Excel) | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81295071"
---
# <a name="sqlgettypeinfo-excel-driver"></a>SQLGetTypeInfo (driver Excel)
> [!NOTE]  
>  In questo argomento vengono fornite informazioni specifiche del driver di Excel. Per informazioni generali su questa funzione, vedere l'argomento appropriato in informazioni di [riferimento sulle API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Il nome del tipo (TYPE_NAME) restituito nella tabella prodotta da **SQLGetTypeInfo** sarà il nome usato più di frequente dall'origine dati.  
  
 SQL_ALL_EXCEPT_LIKE verrà restituito nella colonna RICERCAbile per i tipi di dati byte, Counter, Double, Single, Long e short. Per ottenere la funzionalità LIKE, è possibile convertire il valore in un carattere usando le funzioni di conversione canoniche ODBC, quindi eseguire il confronto.  
  
 Quando si utilizza il driver Microsoft Excel, i nomi dei tipi ODBC vengono restituiti nella colonna TYPE_NAME restituita da **SQLGetTypeInfo**.
