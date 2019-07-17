---
title: Funzione SQLInstallTranslator | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLInstallTranslator
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLInstallTranslator
helpviewer_keywords:
- SQLInstallTranslator function [ODBC]
ms.assetid: 453b21ff-3c2b-4069-8ff7-5c727f062d89
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e5b973332c2fe0fa541635d326a3a5adecf6ae91
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68076107"
---
# <a name="sqlinstalltranslator-function"></a>Funzione SQLInstallTranslator
**Conformità**  
 Versione introdotta: ODBC 2.5, deprecato  
  
 **Riepilogo**  
 In ODBC 3.0 **SQLInstallTranslator** è stata sostituita da [SQLInstallTranslatorEx](../../../odbc/reference/syntax/sqlinstalltranslatorex-function.md). Le chiamate a **SQLInstallTranslator** verrà mappato **SQLInstallTranslatorEx**. Per altre informazioni, vedere **SQLInstallTranslatorEx**.  
  
 **SQLInstallTranslator** restituisce FALSE se un'applicazione viene chiamata in ODBC *3.x* Driver Manager con il *lpszInfFile* argomento impostato su un valore diverso da NULL. Il file Odbc.inf utilizzato in ODBC *2.x* non è più supportata in ODBC *3.x*, anche per la compatibilità con le versioni precedenti.
