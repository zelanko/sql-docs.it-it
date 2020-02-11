---
title: SQLSetScrollOptions (driver ODBC Visual FoxPro) | Microsoft Docs
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
ms.openlocfilehash: b3746d9cea2ce5ffb7d03424d7cda4fa1889aabc
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "67905387"
---
# <a name="sqlsetscrolloptions-visual-foxpro-odbc-driver"></a>SQLSetScrollOptions (driver ODBC Visual FoxPro)
> [!NOTE]  
>  Questo argomento contiene informazioni specifiche del driver ODBC Visual FoxPro. Per informazioni generali su questa funzione, vedere l'argomento appropriato in informazioni di [riferimento sulle API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Supporto: parziale  
  
 Conformità API ODBC: livello 2  
  
 Imposta le opzioni che controllano il comportamento dei cursori associati a un handle di istruzione, *HSTMT*.  
  
 Il driver ODBC Visual FoxPro supporta solo SQL_CONCUR_READ_ONLY; non supporta il valore *fConcurrency* SQL_CONCUR_ROWVER. Il driver converte SQL_KEYSET_SIZE, SQL_CURSOR_DYNAMIC e SQL_CURSOR_KEYSET_DRIVEN in SQL_SCROLL_STATIC con ODBC_01S02 di avviso.  
  
 Per ulteriori informazioni, vedere [SQLSetScrollOptions](../../odbc/reference/syntax/sqlsetscrolloptions-function.md) in *ODBC Programmer ' s Reference*.
