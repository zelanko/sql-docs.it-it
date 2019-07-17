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
ms.openlocfilehash: 6433df796c88abd7873915266d1a2ca4041a5c62
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68125732"
---
# <a name="sqlinstalltranslator-mapping"></a>Mapping di SQLInstallTranslator
Quando un'applicazione ODBC *2.x* applicazione chiama **SQLInstallTranslator** attraverso un ODBC *3.x* driver, Driver Manager viene eseguito il mapping della chiamata a  **SQLInstallTranslatorEx**. Un'applicazione non deve chiamare **SQLInstallTranslator** in ODBC *3.x* gestione Driver con il *lpszInfFile* argomento impostato su un valore diverso da NULL. ODBC. File INF usati in ODBC *2.x* non è più supportata in ODBC *3.x*, anche per la compatibilità con le versioni precedenti.
