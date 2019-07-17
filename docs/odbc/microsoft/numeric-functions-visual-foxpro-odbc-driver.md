---
title: Funzioni numeriche (Driver ODBC Visual FoxPro) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC numeric functions [ODBC]
- Visual FoxPro ODBC driver [ODBC], numeric functions
- numeric functions [ODBC]
- FoxPro ODBC driver [ODBC], numeric functions
ms.assetid: 7caab48e-cbb5-4bbc-a09b-5cf902e5bc45
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 34d2ceb19bce2e466ff5cae7647125e94fdb7c03
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68044991"
---
# <a name="numeric-functions-visual-foxpro-odbc-driver"></a>Funzioni numeriche (driver ODBC Visual FoxPro)
La tabella seguente descrive le funzioni numeriche ODBC supportate dal Driver ODBC Visual FoxPro; Quando la grammatica di Visual FoxPro per la stessa funzione differisce dalla sintassi ODBC, viene elencato l'equivalente di Visual FoxPro.  
  
|Grammatica ODBC|Grammatica di Visual FoxPro|  
|------------------|---------------------------|  
|ABS *(numeric_exp)*||  
|ACOS *(float_exp)*||  
|ASIN *(float_exp)*||  
|ATAN *(float_exp)*||  
|ATAN2 *(float_exp1, float_exp2)*|ATN2 (*float_exp1, float_exp2*)|  
|CEILING *(numeric_exp)*||  
|COS *(float_exp)*||  
|COT *(float_exp)*||  
|DEGREES *(numeric_exp)*|RTOD *(numeric_exp)*|  
|EXP *(float_exp)*||  
|FLOOR *(numeric_exp)*||  
|LOG *(float_exp)*||  
|LOG10 *(float_exp)*||  
|MOD *(integer_exp1, integer_exp2)*||  
|PI *( )*||  
|RADIANS *(numeric_exp)*|DTOR *(numeric_exp)*|  
|RAND *([integer_exp])*||  
|Funzione ROUND *(numeric_exp, integer_exp)*||  
|SIGN *(numeric_exp)*||  
|SIN *(float_exp)*||  
|SQRT *(float_exp)*||  
|TAN *(float_exp)*||  
  
 Non sono supportate le funzioni numeriche seguenti:  
  
 POWER *(numeric_exp, integer_exp)*  
  
 TRUNCATE *(numeric_exp, integer_exp)*
