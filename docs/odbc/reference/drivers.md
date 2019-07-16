---
title: I driver | Microsoft Docs
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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67915435"
---
# <a name="drivers"></a>Driver
*I driver* sono librerie che implementano le funzioni dell'API ODBC. Ognuno è specifico per un determinato DBMS; ad esempio, un driver per Oracle non è possibile accedere direttamente ai dati in un DBMS Informix. I driver di espongono le funzionalità del DBMS sottostante; non sono necessarie per implementare funzionalità non supportate dal sistema DBMS. Ad esempio, se il sistema DBMS sottostante non supporta gli outer join, quindi non deve essere il driver. L'unico importante eccezione è che i driver per DBMS che non dispongono di motori di database autonomo, ad esempio Xbase, devono implementare un motore di database che supporti almeno una quantità minima di SQL.  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Attività dei driver](../../odbc/reference/driver-tasks.md)  
  
-   [Architettura dei driver](../../odbc/reference/driver-architecture.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Driver ODBC forniti da Microsoft](../../odbc/microsoft/microsoft-supplied-odbc-drivers.md)
