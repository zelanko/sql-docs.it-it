---
description: Uso di Microsoft Internet Information Services
title: Utilizzo di Microsoft Internet Information Services | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5e20a15aad4409f535d83e813fdfbd911ca80674
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88471333"
---
# <a name="using-microsoft-internet-information-services"></a>Uso di Microsoft Internet Information Services
> [!IMPORTANT]  
>  Questa funzionalità verrà rimossa in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. Utilizzare invece il driver ODBC fornito da Oracle.  
  
 Se si verificano problemi di connessione da uno script IIS (in particolare se si riceve un errore ORA-12641), aggiungere la riga seguente al file SQLNET. ora:  
  
```  
SQLNET.AUTHENTICATION_SERVICES = (none)  
```  
  
 Questa operazione consente di disabilitare i servizi di rete protetti per potersi connettere usando l'autenticazione anonima.
