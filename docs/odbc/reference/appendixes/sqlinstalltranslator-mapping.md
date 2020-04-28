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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8ab5ebccaac7ccf6374971c1d21040ad15fb3e55
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81300583"
---
# <a name="sqlinstalltranslator-mapping"></a>Mapping di SQLInstallTranslator
Quando un'applicazione ODBC *2. x* chiama **SQLInstallTranslator** tramite un driver ODBC *3. x* , gestione driver esegue il mapping della chiamata a **SQLInstallTranslatorEx**. Un'applicazione non deve chiamare **SQLInstallTranslator** in Gestione driver ODBC *3. x* con l'argomento *lpszInfFile* impostato su un valore diverso da null. ODBC. Il file INF utilizzato in ODBC *2. x* non è più supportato in ODBC *3. x*, anche per compatibilità con le versioni precedenti.
