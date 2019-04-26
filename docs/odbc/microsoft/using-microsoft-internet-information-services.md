---
title: Utilizzando Microsoft Internet Information Services | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC driver for Oracle [ODBC], IIS
- internet information services [ODBC]
- IIS [ODBC]
ms.assetid: 3328f2f1-b34a-472f-82cf-ad49768ff061
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 509979a38e6d7e71f979ce317b9e1626a85c5a54
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62633391"
---
# <a name="using-microsoft-internet-information-services"></a>Uso di Microsoft Internet Information Services
> [!IMPORTANT]  
>  Questa funzionalità verrà rimossa in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. In alternativa, usare il driver ODBC fornito da Oracle.  
  
 Se hai difficoltà connette dall'interno di uno script IIS (in particolare se si riceve un errore o un 12641), aggiungere la riga seguente al file SQLNET:  
  
```  
SQLNET.AUTHENTICATION_SERVICES = (none)  
```  
  
 I servizi di rete sicura verrà disabilitato in modo che sia possibile connettersi tramite l'autenticazione anonima.
