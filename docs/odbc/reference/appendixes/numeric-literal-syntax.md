---
title: Sintassi dei valori letterali numerica | Microsoft Docs
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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67990724"
---
# <a name="numeric-literal-syntax"></a>Sintassi dei valori letterali numerici
La sintassi seguente viene usata per i valori letterali numerici in ODBC:  
  
 *valore letterale numerico* :: = *letterali numerici firmati &#124; letterale numerico senza segno*  
  
 *signed-numeric-literal* ::= [*sign*] *unsigned-numeric-literal*  
  
 *Unsigned-numerico-literal* :: = *letterale numerico esatto &#124; letterali numerici approssimati*  
  
 *exact-numeric-literal* ::= *unsigned-integer* [*period*[*unsigned-integer*]] *&#124;period unsigned-integer*  
  
 *Sign* :: = *segno &#124; segno di sottrazione*  
  
 *letterali numerici approssimati* :: = *esponente mantissa E*  
  
 *mantissa* ::= *exact-numeric-literal*  
  
 *esponente* :: = *integer firmato*  
  
 *signed-integer* ::= [*sign*] *unsigned-integer*  
  
 *intero senza segno* :: = *cifra...*  
  
 *segno di addizione* :: = *+*  
  
 *segno di sottrazione* :: = -  
  
 *digit* ::= 1 &#124; 2 &#124; 3 &#124; 4 &#124; 5 &#124; 6 &#124; 7 &#124; 8 &#124; 9 &#124; 0  
  
 *periodo* :: =.
