---
title: Stored Procedure Limitations parametro | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- stored procedures [ODBC], ODBC driver for Oracle
- ODBC driver for Oracle [ODBC], stored procedures
ms.assetid: 8b804bcf-4cce-4e6f-aa45-00bab9ef9921
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7dc74811bf6cead91850ebd3fcaa8cf64025c80d
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63270862"
---
# <a name="stored-procedure-parameter-limitations"></a>Limitazioni dei parametri delle stored procedure
> [!IMPORTANT]  
>  Questa funzionalità verrà rimossa in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. In alternativa, usare il driver ODBC fornito da Oracle.  
  
 Quando si esegue Oracle stored procedure che utilizzano 10 o più parametri di output, la chiamata alla stored procedure non riuscirà, generando un errore di violazione di accesso o gli oggetti ADO (ActiveX Data). Ciò può verificarsi quando si usa il Driver Microsoft ODBC per Oracle con le versioni 8.0.4.0.0 e 8.0.4.0.4 del software client Oracle.  
  
 Per correggere il problema, il software client Oracle deve essere aggiornato alla versione 8.0.4.2.0 o versione successiva. Contattare Oracle Corporation per altre informazioni sul [patch](../../odbc/microsoft/oracle-software-patches.md).  
  
> [!NOTE]  
>  Questo problema non viene eseguito con la versione preliminare del software client Oracle versione 8.0.3.0.0.
