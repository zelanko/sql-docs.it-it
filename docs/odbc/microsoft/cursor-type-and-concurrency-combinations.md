---
title: Tipo di cursore e concorrenza combinazioni | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC driver for Oracle [ODBC], concurrency options
- cursors [ODBC], ODBC driver for Oracle
- concurrency options [ODBC]
- ODBC driver for Oracle [ODBC], cursor options
ms.assetid: db63d610-f86f-4029-9d66-fed616c8a818
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3e83cb131f37dd2901b77e70d19f5ed95ef596bb
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63151297"
---
# <a name="cursor-type-and-concurrency-combinations"></a>Combinazioni di tipo di cursore e concorrenza
> [!IMPORTANT]  
>  Questa funzionalità verrà rimossa in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. In alternativa, usare il driver ODBC fornito da Oracle.  
  
 Tipi di cursore controllano le funzionalità del cursore fornito all'utente. Le opzioni di concorrenza controllano l'aggiornabilità e comportamento di blocco di un set di risultati.  
  
|Tipo di cursore|Concorrenza (i valori consentiti)|  
|-----------------|------------------------------------|  
|SQL_CURSOR_FORWARD_ONLY|SQL_CONCUR_READ_ONLY|  
|SQL_CURSOR_STATIC|SQL_CONCUR_READ_ONLY|  
|SQL_CURSOR_KEYSET_DRIVEN<sup>[1]</sup>|SQL_CONCUR_READ_ONLY SQL_CONCUR_LOCK<sup>[2]</sup> SQL_CONCUR_VALUES|  
  
 <sup>[1] </sup> Visualizzare [limitazioni dell'utilizzo di cursori](../../odbc/microsoft/limitations-of-using-keyset-driven-cursors.md).  
  
 <sup>[2] </sup> SQL_CONCUR_LOCK è supportata solo quando l'opzione di connessione SQL_AUTOCOMMIT è impostata su SQL_AUTOCOMMIT_OFF.  
  
## <a name="see-also"></a>Vedere anche  
 [Opzioni di connessione](../../odbc/microsoft/connect-options.md)
