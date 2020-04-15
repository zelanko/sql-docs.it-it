---
title: SQLParamOptions (Driver ODBC di Visual FoxPro) Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLParamOptions function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 7f94a6e2-9c34-405c-b2b0-304d94269715
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: dd714ce7774265a2afd00d42894d644a516bc402
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299471"
---
# <a name="sqlparamoptions-visual-foxpro-odbc-driver"></a>SQLParamOptions (driver ODBC Visual FoxPro)
> [!NOTE]  
>  In questo argomento sono contenute informazioni specifiche del driver ODBC di Visual FoxPro. Per informazioni generali su questa funzione, vedere l'argomento appropriato in [Riferimento all'API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Supporto: Completo  
  
 Conformità API ODBC: livello 1ODBC API Conformance: Level 1  
  
 Consente a un'applicazione di specificare più valori per il set di parametri assegnato da [SQLBindParameter.](../../odbc/microsoft/sqlbindparameter-visual-foxpro-odbc-driver.md) La possibilità di specificare più valori per un set di parametri è utile per gli inserimenti bulk e altre operazioni che richiedono all'origine dati di elaborare la stessa istruzione SQL più volte con valori di parametro diversi. Ad esempio, un'applicazione può specificare tre set di valori per il set di parametri associati a un'istruzione **INSERT** e quindi eseguire l'istruzione **INSERT** una sola volta per eseguire le tre operazioni di inserimento.  
  
 Per ulteriori informazioni, vedere [SQLParamOptions](../../odbc/reference/syntax/sqlparamoptions-function.md) in *ODBC Programmer's Reference*.
