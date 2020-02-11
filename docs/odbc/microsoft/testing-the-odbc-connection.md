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
ms.openlocfilehash: 02509ddb6a986ebb7796d80aca10c6f18cde6e69
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "67939702"
---
# <a name="testing-the-odbc-connection"></a>Test della connessione ODBC
> [!IMPORTANT]  
>  Questa funzionalità verrà rimossa in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. Utilizzare invece il driver ODBC fornito da Oracle.  
  
 Quando si risolvono i problemi di accesso ODBC ai server Oracle 7. x e Oracle8 RDBMS, potrebbe essere necessario verificare che gli adapter di protocollo SQL * NET e Oracle sottostanti siano installati correttamente. A tale scopo, utilizzare l'utilità fornita da Oracle. exe nella directory Orawin\Bin  
  
 Netta è una semplice utilità che tenta di accedere al server selezionato utilizzando solo il software SQL * NET installato che fa parte del client Oracle. L'utilità richiederà un nome di account di accesso, una password e una stringa TNS Connect. Se il client Oracle è installato correttamente, l'utilità visualizzerà semplicemente "Ping riuscito". Se l'accesso non riesce, sarà necessario rivolgersi a un amministratore di database.
