---
title: SQLGetTypeInfo (Access Driver) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Access driver [ODBC], SQLGetTypeInfo
- SQLGetTypeInfo function [ODBC], Access Driver
ms.assetid: a28b16eb-ca36-4297-9297-ecd7c107a84e
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1a7c87c0dc81035d59e17db02a6e95c3b573523a
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63028694"
---
# <a name="sqlgettypeinfo-access-driver"></a>SQLGetTypeInfo (driver Access)
> [!NOTE]  
>  In questo argomento vengono fornite informazioni di accesso specifici del Driver. Per informazioni generali su questa funzione, vedere l'argomento appropriato nel [riferimento all'API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Il nome del tipo (TYPE_NAME) restituita nella tabella prodotta dalle **SQLGetTypeInfo** corrisponderà al nome più comunemente utilizzato dall'origine dei dati.  
  
 SQL_ALL_EXCEPT_LIKE verrà restituito nella colonna di ricerca per Byte, del contatore, Double, i tipi di dati singolo, lunghi e brevi. (La funzionalità simile può essere ottenuta convertendo il valore in un carattere utilizzando le funzioni di conversione canonica ODBC, quindi eseguire il confronto).
