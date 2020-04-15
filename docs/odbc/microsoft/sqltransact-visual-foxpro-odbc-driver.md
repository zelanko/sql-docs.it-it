---
title: SQLTransact (Driver ODBC di Visual FoxPro) Documenti Microsoft
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3910f24578bcbc409a84573e994c0680ed5949b2
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299221"
---
# <a name="sqltransact-visual-foxpro-odbc-driver"></a>SQLTransact (driver ODBC Visual FoxPro)
> [!NOTE]  
>  In questo argomento sono contenute informazioni specifiche del driver ODBC di Visual FoxPro. Per informazioni generali su questa funzione, vedere l'argomento appropriato in [Riferimento all'API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Supporto: Completo  
  
 Conformità API ODBC: livello di baseODBC API Conformance: Core Level  
  
 Richiede un'operazione di commit o rollback per tutte le operazioni attive su tutti gli handle di istruzione *(hstmt*s) associati a una connessione o per tutte le connessioni associate all'handle di ambiente, *henv*. **SQLTransact** funziona solo per le origini dati che sono [database](../../odbc/microsoft/visual-foxpro-terminology.md).  
  
 Se un commit ha esito negativo in modalità manuale, la transazione rimane attiva; è possibile scegliere di eseguire il rollback della transazione o ripetere l'operazione di commit. Se un'operazione di commit ha esito negativo in modalità di transazione automatica, viene eseguito automaticamente il rollback della transazione. la transazione non può essere inattiva.  
  
 Per ulteriori informazioni, vedere [SQLTransact](../../odbc/reference/syntax/sqltransact-function.md) in *ODBC Programmer's Reference*.
