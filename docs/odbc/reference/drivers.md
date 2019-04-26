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
manager: craigg
ms.openlocfilehash: 2e3996aafa0e4f5b389e4f46d5df3b22632daad9
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62628766"
---
# <a name="drivers"></a>Driver
*I driver* sono librerie che implementano le funzioni dell'API ODBC. Ognuno è specifico per un determinato DBMS; ad esempio, un driver per Oracle non è possibile accedere direttamente ai dati in un DBMS Informix. I driver di espongono le funzionalità del DBMS sottostante; non sono necessarie per implementare funzionalità non supportate dal sistema DBMS. Ad esempio, se il sistema DBMS sottostante non supporta gli outer join, quindi non deve essere il driver. L'unico importante eccezione è che i driver per DBMS che non dispongono di motori di database autonomo, ad esempio Xbase, devono implementare un motore di database che supporti almeno una quantità minima di SQL.  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Attività dei driver](../../odbc/reference/driver-tasks.md)  
  
-   [Architettura dei driver](../../odbc/reference/driver-architecture.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Driver ODBC forniti da Microsoft](../../odbc/microsoft/microsoft-supplied-odbc-drivers.md)
