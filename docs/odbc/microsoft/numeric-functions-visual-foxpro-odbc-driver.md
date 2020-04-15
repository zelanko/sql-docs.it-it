---
title: Funzioni numeriche (Driver ODBC di Visual FoxPro) . Documenti Microsoft
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
ms.openlocfilehash: d3993a9a1b2412cb15229f2763c7c3b38f6b7862
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298161"
---
# <a name="numeric-functions-visual-foxpro-odbc-driver"></a>Funzioni numeriche (driver ODBC Visual FoxPro)
Nella tabella seguente vengono descritte le funzioni numeriche ODBC supportate dal driver ODBC di Visual FoxPro. Quando la grammatica di Visual FoxPro per la stessa funzione è diversa dalla sintassi ODBC, viene elencato l'equivalente di Visual FoxPro.  
  
|Grammatica ODBC|Grammatica di Visual FoxPro|  
|------------------|---------------------------|  
|ABS *(numeric_exp)*||  
|ACOS *(float_exp)*||  
|ASIN *(float_exp)*||  
|ATAN *(float_exp)*||  
|ATAN2 *(float_exp1, float_exp2)*|ATN2 (*float_exp1, float_exp2*)|  
|ARROTONDA *numeric_exp.*||  
|COS *(float_exp)*||  
|COT *(float_exp)*||  
|GRADI *(numeric_exp)*|RTOD *(numeric_exp)*|  
|EXP *(float_exp)*||  
|FLOOR *(numeric_exp)*||  
|LOG *(float_exp)*||  
|LOG10 *(float_exp)*||  
|MOD *(integer_exp1, integer_exp2)*||  
|PI *( )*||  
|RADIANTI *(numeric_exp)*|DTOR *(numeric_exp)*|  
|RAND *([integer_exp])*||  
|ARROTONDA *(numeric_exp, integer_exp)*||  
|SEGNO *(numeric_exp)*||  
|SIN *(float_exp)*||  
|RADQ *(float_exp)*||  
|TAN *(float_exp)*||  
  
 Le seguenti funzioni numeriche non sono supportate:  
  
 POWER *(numeric_exp, integer_exp)*  
  
 TRUNCATE *(numeric_exp, integer_exp)*
