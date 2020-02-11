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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 9daa81e2e0c2e927ee7407d4a00d5d48c333bd54
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "67990724"
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
