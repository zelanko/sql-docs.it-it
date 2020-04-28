---
title: Sintassi di valori letterali numerici | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC literals [ODBC], numeric
- numeric literals [ODBC]
- literals [ODBC], numeric
ms.assetid: fb17498d-4f1d-4b3d-b33d-1e62c7d3c32d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e035e3ec53c5b5494c029d6840b9f5c836821209
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81299861"
---
# <a name="numeric-literal-syntax"></a>Sintassi dei valori letterali numerici
Per i valori letterali numerici in ODBC viene utilizzata la sintassi seguente:  
  
 *numeric-Literal* :: = *signed-numeric-Literal &#124; unsigned-numeric-Literal*  
  
 *signed-numeric-Literal* :: = [*segno*] senza *segno-numeric-Literal*  
  
 *unsigned-numeric-Literal* :: = *exact-numeric-Literal &#124; approssimate-numeric-Literal*  
  
 *exact-numeric-Literal* :: = *unsigned-integer* [*periodo*[*senza segno-intero*]] *&#124;periodo senza segno-intero*  
  
 *Sign::* = *più-sign &#124; segno meno*  
  
 *approssimativo-numeric-Literal* :: = *mantissa ed esponente*  
  
 *mantissa* :: = *exact-numeric-Literal*  
  
 *esponente* :: = *Signed-Integer*  
  
 *Signed-Integer* :: = [*segno*] senza *segno-intero*  
  
 *unsigned-integer* :: = *digit...*  
  
 *segno più* :: =*+*  
  
 *segno meno* :: =-  
  
 *digit* :: = 1 &#124; 2 &#124; 3 &#124; 4 &#124; 5 &#124; 6 &#124; 7 &#124; 8 &#124; 9 &#124; 0  
  
 *periodo* :: =.
