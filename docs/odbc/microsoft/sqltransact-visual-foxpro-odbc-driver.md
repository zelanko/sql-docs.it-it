---
title: SQLTransact (driver ODBC Visual FoxPro) | Microsoft Docs
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "67948863"
---
# <a name="sqltransact-visual-foxpro-odbc-driver"></a>SQLTransact (driver ODBC Visual FoxPro)
> [!NOTE]  
>  Questo argomento contiene informazioni specifiche del driver ODBC Visual FoxPro. Per informazioni generali su questa funzione, vedere l'argomento appropriato in informazioni di [riferimento sulle API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Supporto: completo  
  
 Conformità API ODBC: livello principale  
  
 Richiede un'operazione di commit o di rollback per tutte le operazioni attive in tutti gli handle di istruzione (*HSTMT*) associati a una connessione o per tutte le connessioni associate all'handle di ambiente, *HENV*. **SQLTransact** funziona solo per le origini dati che sono [database](../../odbc/microsoft/visual-foxpro-terminology.md)di.  
  
 Se un commit ha esito negativo in modalità manuale, la transazione rimane attiva. è possibile scegliere di eseguire il rollback della transazione o di ripetere l'operazione di commit. Se un'operazione di commit ha esito negativo in modalità di transazione automatica, viene eseguito il rollback automatico della transazione. la transazione non può essere inattiva.  
  
 Per ulteriori informazioni, vedere [SQLTransact](../../odbc/reference/syntax/sqltransact-function.md) in *ODBC Programmer ' s Reference*.
