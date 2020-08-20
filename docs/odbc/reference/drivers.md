---
description: Driver
title: Driver | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC architecture [ODBC], drivers
- drivers [ODBC]
- drivers [ODBC], about drivers
ms.assetid: d6795d92-877e-44e1-b7d5-2ff2fd3989bd
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 81e8989fc178728e687baa13b37e6055692d9413
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88494594"
---
# <a name="drivers"></a>Driver
I *driver* sono librerie che implementano le funzioni nell'API ODBC. Ogni è specifico di un determinato sistema DBMS; un driver per Oracle, ad esempio, non può accedere direttamente ai dati in un DBMS di Informix. I driver espongono le funzionalità dei DBMS sottostanti; non è necessario implementare funzionalità non supportate dal sistema DBMS. Se, ad esempio, il sistema DBMS sottostante non supporta outer join, il driver non sarà né. L'unica eccezione principale è che i driver per DBMS che non dispongono di motori di database autonomi, ad esempio Xbase, devono implementare un motore di database che supporta almeno una quantità minima di SQL.  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Attività dei driver](../../odbc/reference/driver-tasks.md)  
  
-   [Architettura dei driver](../../odbc/reference/driver-architecture.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Driver ODBC forniti da Microsoft](../../odbc/microsoft/microsoft-supplied-odbc-drivers.md)
