---
title: SQLTransact (Driver di accesso) Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Access driver [ODBC], SQLTransact
- SQLTransact function [ODBC], Access Driver
ms.assetid: 892b79c7-9e20-4d1f-bc60-d4b25694ca25
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4f88d3154925ab589a8519cb9205da03e8c3dc08
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299265"
---
# <a name="sqltransact-access-driver"></a>SQLTransact (driver Access)
> [!NOTE]  
>  In questo argomento vengono fornite informazioni specifiche del driver di accesso. Per informazioni generali su questa funzione, vedere l'argomento appropriato in [Riferimento all'API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Quando viene utilizzato il driver di Microsoft Access, SQL_COMMIT e SQL_ROLLBACK sono supportati per l'argomento *fType* in una chiamata a **SQLTransact**.  
  
 Se si verifica un errore durante il processo di commit, il database interessato può essere ripristinato utilizzando l'opzione Ripristina database nell'installazione del driver di Microsoft Access o tramite l'utilizzo della parola chiave REPAIR_DB nella funzione **SQLConfigDataSource.**
