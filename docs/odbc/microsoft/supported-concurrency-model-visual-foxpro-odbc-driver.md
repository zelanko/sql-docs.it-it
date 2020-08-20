---
description: Modello di concorrenza supportato (driver ODBC Visual FoxPro)
title: Modello di concorrenza supportato (driver ODBC Visual FoxPro) | Microsoft Docs
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
ms.openlocfilehash: 1be0a7e9ea3700941282f23956a8c304a1ef7f5e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88500104"
---
# <a name="supported-concurrency-model-visual-foxpro-odbc-driver"></a>Modello di concorrenza supportato (driver ODBC Visual FoxPro)
Il driver ODBC Visual FoxPro supporta la *concorrenza di sola lettura*. L'applicazione può chiamare [SQLSetStmtOption](../../odbc/microsoft/sqlsetstmtoption-visual-foxpro-odbc-driver.md) con un'opzione SQL_CONCURRENCY di SQL_CONCUR_READ_ONLY.  
  
 Per ulteriori informazioni, vedere [ODBC Programmer ' s Reference](../../odbc/reference/odbc-programmer-s-reference.md).  
  
## <a name="read-only-concurrency"></a>concorrenza di sola lettura  
 Impossibile aggiornare il cursore.  
  
## <a name="row-versioning"></a>controllo delle versioni delle righe  
 Essenzialmente il supporto del timestamp, in cui le versioni di riga vengono confrontate al momento dell'aggiornamento.
