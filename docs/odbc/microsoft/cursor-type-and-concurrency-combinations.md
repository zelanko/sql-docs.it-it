---
title: Combinazioni di tipo di cursore e concorrenza | Microsoft Docs
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
ms.openlocfilehash: 2a29fc2d02cb46dda44fa22b2344cbab475443f2
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68096521"
---
# <a name="cursor-type-and-concurrency-combinations"></a>Combinazioni di tipo di cursore e concorrenza
> [!IMPORTANT]  
>  Questa funzionalità verrà rimossa in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. Utilizzare invece il driver ODBC fornito da Oracle.  
  
 I tipi di cursore controllano la funzionalità del cursore fornito all'utente. Le opzioni di concorrenza controllano il aggiornabilità e il comportamento di blocco di un set di risultati.  
  
|Tipo di cursore|Concorrenza (valori consentiti)|  
|-----------------|------------------------------------|  
|SQL_CURSOR_FORWARD_ONLY|SQL_CONCUR_READ_ONLY|  
|SQL_CURSOR_STATIC|SQL_CONCUR_READ_ONLY|  
|SQL_CURSOR_KEYSET_DRIVEN<sup>[1]</sup>|SQL_CONCUR_READ_ONLY SQL_CONCUR_LOCK<sup>[2]</sup> SQL_CONCUR_VALUES|  
  
 <sup>[1]</sup> vedere [limitazioni dell'utilizzo di cursori gestiti da keyset](../../odbc/microsoft/limitations-of-using-keyset-driven-cursors.md).  
  
 <sup>[2]</sup> SQL_CONCUR_LOCK è supportato solo quando l'opzione di connessione SQL_AUTOCOMMIT è impostata su SQL_AUTOCOMMIT_OFF.  
  
## <a name="see-also"></a>Vedere anche  
 [Opzioni di connessione](../../odbc/microsoft/connect-options.md)
