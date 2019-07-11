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
ms.openlocfilehash: 50bfa00f482110d3d0695ef249e8758b5db02c80
ms.sourcegitcommit: 56b963446965f3a4bb0fa1446f49578dbff382e0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2019
ms.locfileid: "67792809"
---
# <a name="sqlinstalltranslator-mapping"></a>Mapping di SQLInstallTranslator
Quando un'applicazione ODBC *2.x* applicazione chiama **SQLInstallTranslator** attraverso un ODBC *3.x* driver, Driver Manager viene eseguito il mapping della chiamata a  **SQLInstallTranslatorEx**. Un'applicazione non deve chiamare **SQLInstallTranslator** in ODBC *3.x* gestione Driver con il *lpszInfFile* argomento impostato su un valore diverso da NULL. ODBC. File INF usati in ODBC *2.x* non è più supportata in ODBC *3.x*, anche per la compatibilità con le versioni precedenti.
