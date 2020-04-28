---
title: Marcatori di parametro nelle chiamate di procedura | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], interoperability
- parameter markers [ODBC]
- interoperability of SQL statements [ODBC], parameter markers
ms.assetid: cda56f2b-6eec-4cbc-8dbb-36d8fa9f9216
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e1a0099e298b0326b5ccc19d6281fa3a091d57a2
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81282497"
---
# <a name="parameter-markers-in-procedure-calls"></a>Marcatori di parametro nelle chiamate di procedura
Quando si richiamano routine che accettano parametri, le applicazioni interoperative devono utilizzare marcatori di parametro anziché valori di parametri letterali. Alcune origini dati non supportano l'utilizzo di valori di parametro letterali nelle chiamate di procedura. Per ulteriori informazioni sui parametri, vedere [parametri di istruzione](../../../odbc/reference/develop-app/statement-parameters.md). Per ulteriori informazioni sulle procedure di chiamata, vedere [procedure calls](../../../odbc/reference/develop-app/procedure-calls.md), più avanti in questa sezione.
