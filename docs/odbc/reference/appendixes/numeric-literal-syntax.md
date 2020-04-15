---
title: Sintassi dei valori letterali numerici - Documenti Microsoft
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299861"
---
# <a name="numeric-literal-syntax"></a>Sintassi dei valori letterali numerici
La sintassi seguente viene utilizzata per i valori letterali numerici in ODBC:  
  
 *numerico-letterale* :: *: signed-numeric-literal &#124; unsigned-numeric-literal*  
  
 *signed-numeric-literal* :: [*segno*] *unsigned-numeric-literal*  
  
 *unsigned-numeric-literal* :: : *esatto-numerico-letterale &#124; approssimativo-numerico-letterale*  
  
 *exact-numeric-literal* :: *unsigned-integer* [*punto*[*unsigned-integer*]] *&#124;punto unsigned-integer*  
  
 *segno* :: : *segno più &#124; segno meno*  
  
 *approssimativo-numerico-letterale* :: : *mantissa E esponente*  
  
 *mantissa* :: *: esatto-numerico-letterale*  
  
 *esponente* :: *: intero con segno*  
  
 *signed-integer* :: [*segno*] *unsigned-integer*  
  
 *unsigned-integer* :: *cifra...*  
  
 *segno di addito* ::*+*  
  
 *segno meno* ::  
  
 *cifra* :: 1 &#124; 2 &#124; 3 &#124; 4 &#124; 5 &#124; 6 &#124; 7 &#124; 8 &#124; &#124; 9 &#124; 0  
  
 *periodo* :: .
