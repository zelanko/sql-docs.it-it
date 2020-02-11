---
title: Più istruzioni e connessioni attive | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 76b74ff748a62a401955e4ea4a995f507314124e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "67942821"
---
# <a name="multiple-active-statements-and-connections"></a>Istruzioni e connessioni attive multiple
Alcuni driver e DBMS limitano il numero di istruzioni e connessioni che possono essere attive alla volta. Questi numeri possono essere più piccoli di uno. Per ulteriori informazioni, vedere le opzioni SQL_MAX_CONCURRENT_ACTIVITIES e SQL_MAX_DRIVER_CONNECTIONS nella descrizione della funzione [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) , nonché gli handle di [istruzione](../../../odbc/reference/develop-app/statement-handles.md) e di [connessione](../../../odbc/reference/develop-app/connection-handles.md).
