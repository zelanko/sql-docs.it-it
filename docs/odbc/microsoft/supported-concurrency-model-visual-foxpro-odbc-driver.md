---
title: Modello di concorrenza (Driver ODBC Visual FoxPro) supportato | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f8528ecb2f34d3f0ef7120c7047865ab5f6c1a72
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63270094"
---
# <a name="supported-concurrency-model-visual-foxpro-odbc-driver"></a>Modello di concorrenza supportato (driver ODBC Visual FoxPro)
Supporta il Driver ODBC Visual FoxPro *concorrenza di sola lettura*. L'applicazione può chiamare [SQLSetStmtOption](../../odbc/microsoft/sqlsetstmtoption-visual-foxpro-odbc-driver.md) con un'opzione SQL_CONCURRENCY di SQL_CONCUR_READ_ONLY.  
  
 Per ulteriori informazioni, vedere la [di riferimento del programmatore di ODBC](../../odbc/reference/odbc-programmer-s-reference.md).  
  
## <a name="read-only-concurrency"></a>concorrenza di sola lettura  
 Il cursore non può essere aggiornato.  
  
## <a name="row-versioning"></a>controllo delle versioni delle righe  
 Essenzialmente timestamp supporto, in quale riga vengono confrontate le versioni in fase di aggiornamento.
