---
title: SQLSetScrollOptions (Driver ODBC Visual FoxPro) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLSetScrollOptions function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 693e6e28-a845-41b1-9622-5058b0d87229
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8c2d78e26309d5ea7dc5e6eed5a04e84a1651b33
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63305744"
---
# <a name="sqlsetscrolloptions-visual-foxpro-odbc-driver"></a>SQLSetScrollOptions (driver ODBC Visual FoxPro)
> [!NOTE]  
>  In questo argomento contiene informazioni specifiche del Driver ODBC Visual FoxPro. Per informazioni generali su questa funzione, vedere l'argomento appropriato nel [riferimento all'API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Supporto: Partial  
  
 Conformità di API ODBC: Livello 2  
  
 Imposta le opzioni che controllano il comportamento dei cursori associata a un handle di istruzione *hstmt*.  
  
 Il Driver ODBC Visual FoxPro supporta solo SQL_CONCUR_READ_ONLY; non supporta il *fConcurrency* valore SQL_CONCUR_ROWVER. Il driver converte SQL_KEYSET_SIZE SQL_CURSOR_DYNAMIC e SQL_CURSOR_KEYSET_DRIVEN SQL_SCROLL_STATIC con avviso ODBC_01S02.  
  
 Per altre informazioni, vedere [SQLSetScrollOptions](../../odbc/reference/syntax/sqlsetscrolloptions-function.md) nel *riferimento per programmatori ODBC*.
