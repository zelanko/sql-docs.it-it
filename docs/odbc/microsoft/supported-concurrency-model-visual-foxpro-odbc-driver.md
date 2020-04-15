---
title: Modello di concorrenza supportato (driver ODBC di Visual FoxPro) . Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Visual FoxPro ODBC driver [ODBC], concurrency
- concurrency models [ODBC]
- FoxPro ODBC driver [ODBC], concurrency
ms.assetid: c39ed963-3af1-4888-8631-6083692ddcd7
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 253a6dd86f6dc974d53dd151636bb8b8132e4d02
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307717"
---
# <a name="supported-concurrency-model-visual-foxpro-odbc-driver"></a>Modello di concorrenza supportato (driver ODBC Visual FoxPro)
Il driver ODBC di Visual FoxPro supporta la concorrenza di *sola lettura.* L'applicazione può chiamare [SQLSetStmtOption](../../odbc/microsoft/sqlsetstmtoption-visual-foxpro-odbc-driver.md) con un'opzione SQL_CONCURRENCY di SQL_CONCUR_READ_ONLY.  
  
 Per ulteriori informazioni, vedere [ODBC Programmer's Reference](../../odbc/reference/odbc-programmer-s-reference.md).  
  
## <a name="read-only-concurrency"></a>concorrenza di sola lettura  
 Impossibile aggiornare il cursore.  
  
## <a name="row-versioning"></a>controllo delle versioni delle righe  
 Essenzialmente il supporto timestamp, in cui le versioni di riga vengono confrontate in fase di aggiornamento.
