---
description: Funzioni numeriche (driver ODBC Visual FoxPro)
title: Funzioni numeriche (driver ODBC Visual FoxPro) | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c8728446decd8a0ad04f08d88475ae08a7c69c5f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88449373"
---
# <a name="numeric-functions-visual-foxpro-odbc-driver"></a>Funzioni numeriche (driver ODBC Visual FoxPro)
Nella tabella seguente vengono descritte le funzioni numeriche ODBC supportate dal driver ODBC Visual FoxPro. Quando la grammatica Visual FoxPro per la stessa funzione differisce dalla sintassi ODBC, viene elencato l'equivalente Visual FoxPro.  
  
|Grammatica ODBC|Grammatica Visual FoxPro|  
|------------------|---------------------------|  
|ABS *(numeric_exp)*||  
|ARccOS *(float_exp)*||  
|ASIN *(float_exp)*||  
|ATAN *(float_exp)*||  
|ATAN2 *(float_exp1, float_exp2)*|ATN2 (*float_exp1, float_exp2*)|  
|CEILING *(numeric_exp)*||  
|COS *(float_exp)*||  
|LETTIno *(float_exp)*||  
|GRADI *(numeric_exp)*|RTOD *(numeric_exp)*|  
|EXP *(float_exp)*||  
|PIANO *(numeric_exp)*||  
|LOG *(float_exp)*||  
|LOG10 *(float_exp)*||  
|MOD *(integer_exp1, integer_exp2)*||  
|PI *()*||  
|RADIAnti *(numeric_exp)*|DTOR *(numeric_exp)*|  
|RAND *([integer_exp])*||  
|ROUND *(numeric_exp, integer_exp)*||  
|FIRMA *(numeric_exp)*||  
|SIN *(float_exp)*||  
|SQRT *(float_exp)*||  
|TAN *(float_exp)*||  
  
 Le funzioni numeriche seguenti non sono supportate:  
  
 POTENZA *(numeric_exp, integer_exp)*  
  
 TRONCA *(numeric_exp, integer_exp)*
