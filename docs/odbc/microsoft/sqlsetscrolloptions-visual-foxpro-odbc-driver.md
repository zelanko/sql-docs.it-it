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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 19051fc83466bc40d72c029089cfe6ec45c20a08
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81299421"
---
# <a name="sqlsetscrolloptions-visual-foxpro-odbc-driver"></a>SQLSetScrollOptions (driver ODBC Visual FoxPro)
> [!NOTE]  
>  Questo argomento contiene informazioni specifiche del driver ODBC Visual FoxPro. Per informazioni generali su questa funzione, vedere l'argomento appropriato in informazioni di [riferimento sulle API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Supporto: parziale  
  
 Conformità API ODBC: livello 2  
  
 Imposta le opzioni che controllano il comportamento dei cursori associati a un handle di istruzione, *HSTMT*.  
  
 Il driver ODBC Visual FoxPro supporta solo SQL_CONCUR_READ_ONLY; non supporta il valore *fConcurrency* SQL_CONCUR_ROWVER. Il driver converte SQL_KEYSET_SIZE, SQL_CURSOR_DYNAMIC e SQL_CURSOR_KEYSET_DRIVEN in SQL_SCROLL_STATIC con ODBC_01S02 di avviso.  
  
 Per ulteriori informazioni, vedere [SQLSetScrollOptions](../../odbc/reference/syntax/sqlsetscrolloptions-function.md) in *ODBC Programmer ' s Reference*.
