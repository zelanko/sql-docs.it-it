---
title: Test della connessione ODBC | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- testing connections [ODBC]
- ODBC driver for Oracle [ODBC], testing connections
ms.assetid: 5e671665-2aba-49a7-8871-70784d8b3cc9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 543ab436ac7dca5e0d5965220cd90a798afb5ccf
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62633176"
---
# <a name="testing-the-odbc-connection"></a>Test della connessione ODBC
> [!IMPORTANT]  
>  Questa funzionalità verrà rimossa in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. In alternativa, usare il driver ODBC fornito da Oracle.  
  
 La risoluzione dei problemi di accesso ODBC per Oracle 7.x e i server Oracle8 RDBMS, potrebbe essere necessario verificare che il codice sottostante SQL * Net e adattatori del protocollo Oracle siano installati correttamente. A tale scopo, utilizzare l'utilità Oracle forniti Nettest.exe nella directory Orawin\Bin.  
  
 Nettest è una semplice utilità che tenta di accedere al server selezionato utilizzando solo l'installati SQL * Net software che fa parte del client Oracle. L'utilità chiede un nome di account di accesso, la password e TNS stringa di connessione. Se il client Oracle è stato installato correttamente, l'utilità visualizzerà semplicemente "Ping riuscito". Se l'account di accesso non è riuscita, è necessario contattare l'amministratore del database.
