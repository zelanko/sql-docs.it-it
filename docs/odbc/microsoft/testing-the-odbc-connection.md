---
description: Test della connessione ODBC
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 61a471af3c5681ca58ca3268ad4512ee80abb9cb
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88421545"
---
# <a name="testing-the-odbc-connection"></a>Test della connessione ODBC
> [!IMPORTANT]  
>  Questa funzionalità verrà rimossa in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. Utilizzare invece il driver ODBC fornito da Oracle.  
  
 Quando si risolvono i problemi di accesso ODBC ai server Oracle 7. x e Oracle8 RDBMS, potrebbe essere necessario verificare che gli adapter di protocollo SQL * NET e Oracle sottostanti siano installati correttamente. A tale scopo, usare l'utilità fornita da Oracle Nettest.exe nella directory Orawin\Bin  
  
 Netta è una semplice utilità che tenta di accedere al server selezionato utilizzando solo il software SQL * NET installato che fa parte del client Oracle. L'utilità richiederà un nome di account di accesso, una password e una stringa TNS Connect. Se il client Oracle è installato correttamente, l'utilità visualizzerà semplicemente "Ping riuscito". Se l'accesso non riesce, sarà necessario rivolgersi a un amministratore di database.
