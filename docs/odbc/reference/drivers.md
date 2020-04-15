---
title: Proprietà Drivers . Documenti Microsoft
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
ms.openlocfilehash: 7c8b40641be3db34fc6929edecdd5dd923700957
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81294184"
---
# <a name="drivers"></a>Driver
*I driver* sono librerie che implementano le funzioni nell'API ODBC. Ognuno è specifico di un particolare DBMS; ad esempio, un driver per Oracle non può accedere direttamente ai dati in un DBMS Informix. I driver espongono le funzionalità dei DBSMO sottostanti; non sono necessari per implementare funzionalità non supportate dal DBMS. Ad esempio, se il DBMS sottostante non supporta outer join, il driver non dovrebbe. L'unica eccezione principale è che i driver per DBSMO che non dispongono di motori di database autonomi, ad esempio Xbase, devono implementare un motore di database che supporta almeno una quantità minima di SQL.  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Attività dei driver](../../odbc/reference/driver-tasks.md)  
  
-   [Architettura dei driver](../../odbc/reference/driver-architecture.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Driver ODBC forniti da Microsoft](../../odbc/microsoft/microsoft-supplied-odbc-drivers.md)
