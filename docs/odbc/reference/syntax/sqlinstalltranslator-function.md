---
title: Funzione SQLInstallTranslator . Documenti Microsoft
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b094aa730fff6db80b9addb63a92bee0f5f85b2a
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300321"
---
# <a name="sqlinstalltranslator-function"></a>Funzione SQLInstallTranslator
**Conformità**  
 Versione introdotta: ODBC 2.5, deprecato  
  
 **Riepilogo**  
 In ODBC 3.0 **SQLInstallTranslator** è stato sostituito da [SQLInstallTranslatorEx](../../../odbc/reference/syntax/sqlinstalltranslatorex-function.md). Le chiamate a **SQLInstallTranslator** verranno mappate a **SQLInstallTranslatorEx**. Per ulteriori informazioni, vedere **SQLInstallTranslatorEx**.  
  
 **SQLInstallTranslator** restituirà FALSE se un'applicazione lo chiama in Gestione Driver ODBC *3.x* con l'argomento *lpszInfFile* impostato su un valore diverso da NULL. Il file Odbc.inf utilizzato in ODBC *2.x* non è più supportato in ODBC *3.x*, anche per compatibilità con le versioni precedenti.
