---
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 6460410488186c94713d859bf2912f2844ca2736
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "67915435"
---
# <a name="drivers"></a>Driver
I *driver* sono librerie che implementano le funzioni nell'API ODBC. Ogni è specifico di un determinato sistema DBMS; un driver per Oracle, ad esempio, non può accedere direttamente ai dati in un DBMS di Informix. I driver espongono le funzionalità dei DBMS sottostanti; non è necessario implementare funzionalità non supportate dal sistema DBMS. Se, ad esempio, il sistema DBMS sottostante non supporta outer join, il driver non sarà né. L'unica eccezione principale è che i driver per DBMS che non dispongono di motori di database autonomi, ad esempio Xbase, devono implementare un motore di database che supporta almeno una quantità minima di SQL.  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Attività dei driver](../../odbc/reference/driver-tasks.md)  
  
-   [Architettura dei driver](../../odbc/reference/driver-architecture.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Driver ODBC forniti da Microsoft](../../odbc/microsoft/microsoft-supplied-odbc-drivers.md)
