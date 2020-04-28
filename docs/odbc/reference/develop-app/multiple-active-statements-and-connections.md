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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8259967942f47b06c50a9043158f8b3b45c58d7a
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81302430"
---
# <a name="multiple-active-statements-and-connections"></a>Istruzioni e connessioni attive multiple
Alcuni driver e DBMS limitano il numero di istruzioni e connessioni che possono essere attive alla volta. Questi numeri possono essere più piccoli di uno. Per ulteriori informazioni, vedere le opzioni SQL_MAX_CONCURRENT_ACTIVITIES e SQL_MAX_DRIVER_CONNECTIONS nella descrizione della funzione [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) , nonché gli handle di [istruzione](../../../odbc/reference/develop-app/statement-handles.md) e di [connessione](../../../odbc/reference/develop-app/connection-handles.md).
