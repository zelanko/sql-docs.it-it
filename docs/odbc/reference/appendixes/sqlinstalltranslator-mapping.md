---
title: Mapping di SQLInstallTranslator | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLInstallTranslator function [ODBC], mapping
- mapping deprecated functions [ODBC], SQLInstallTranslator
ms.assetid: bcd9ba4f-7834-4bc4-876e-c7478998e524
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9760bfad769e9508d58d1cd00f98376dbd13d877
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63298512"
---
# <a name="sqlinstalltranslator-mapping"></a>Mapping di SQLInstallTranslator
Quando un'applicazione ODBC 2. *x* applicazione chiama **SQLInstallTranslator** tramite un'applicazione ODBC 3*x* driver, Driver Manager viene eseguito il mapping della chiamata a **SQLInstallTranslatorEx**. Un'applicazione non deve chiamare **SQLInstallTranslator** in ODBC 3 *. x* gestione Driver con il *lpszInfFile* argomento impostato su un valore diverso da NULL. ODBC. File INF usati in ODBC 2. *x* non è più supportata in ODBC 3*x*, anche per la compatibilità con le versioni precedenti.
