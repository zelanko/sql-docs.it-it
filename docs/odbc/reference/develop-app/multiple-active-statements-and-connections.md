---
title: Più istruzioni attive e connessioni Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- interoperability [ODBC], multiple active statements and connections
- multiple active statements and connections [ODBC]
ms.assetid: a6571356-b23e-4f10-a17b-bce09460b71e
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8259967942f47b06c50a9043158f8b3b45c58d7a
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302430"
---
# <a name="multiple-active-statements-and-connections"></a>Istruzioni e connessioni attive multiple
Alcuni driver e DBDISPIACE limitano il numero di istruzioni e connessioni che possono essere attive contemporaneamente. Questi numeri possono essere piccoli come uno. Per ulteriori informazioni, vedere le opzioni SQL_MAX_CONCURRENT_ACTIVITIES e SQL_MAX_DRIVER_CONNECTIONS nella descrizione della funzione [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) e Handle di [istruzione](../../../odbc/reference/develop-app/statement-handles.md) e [di connessione](../../../odbc/reference/develop-app/connection-handles.md).
