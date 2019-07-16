---
title: SQLTransact (Driver ODBC Visual FoxPro) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLTransact function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 92cf86c0-f7a8-44d7-b59f-a1342677440b
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e554a8669b6e6e95e234a5b939477a8bb2f7b8cc
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67948863"
---
# <a name="sqltransact-visual-foxpro-odbc-driver"></a>SQLTransact (driver ODBC Visual FoxPro)
> [!NOTE]  
>  In questo argomento contiene informazioni specifiche del Driver ODBC Visual FoxPro. Per informazioni generali su questa funzione, vedere l'argomento appropriato nel [riferimento all'API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Supporto: Full  
  
 Conformità di API ODBC: A livello centrale  
  
 Richiede un'operazione di commit o rollback per tutte le operazioni attive in tutti gli handle di istruzione (*hstmt*s) con una connessione o per tutte le connessioni associate all'handle di ambiente, associati *henv*. **SQLTransact** funziona solo per le origini dati che vengono [database](../../odbc/microsoft/visual-foxpro-terminology.md).  
  
 Se un'operazione di commit ha esito negativo quando è in modalità manuale, la transazione rimane attiva; è possibile scegliere di rollback della transazione o ripetere l'operazione di commit. Se un'operazione di commit ha esito negativo quando è in modalità di transazione automatica, il rollback della transazione automaticamente. la transazione non può essere inattiva.  
  
 Per altre informazioni, vedere [SQLTransact](../../odbc/reference/syntax/sqltransact-function.md) nel *riferimento per programmatori ODBC*.
