---
title: Sintassi letterale intervallo Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- literals [ODBC], interval
- interval literals [ODBC]
- ODBC literals [ODBC], interval
ms.assetid: 2f2d22c1-51d6-4055-9f5a-53bc31e9fea0
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3387b07a8e769206a6a495addff4287000691fec
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81290571"
---
# <a name="interval-literal-syntax"></a>Sintassi dei valori letterali intervallo
La sintassi seguente viene utilizzata per i valori letterali di intervallo in ODBC.  
  
 *interval-literal :: INTERVAL* [sezione *&#124;*-] *interval-string interval-qualifier*  
  
 *interval-string* :: *, citazione* , *anno-mese-letterale* &#124; *giorno-ora-letterale,* *citazione*  
  
 *anno-mese-letterale* :: : *valore-anni* &#124; [*valore-anni* -] *valore-mesi*  
  
 *giorno-ora-letterale* :: : *intervallo di giorno* &#124; *intervallo di tempo*  
  
 *giorno-ora-intervallo* :: : *giorni-valore* [*ore-valore* [:*minuti-valore*[:*secondi-valore*]]]  
  
 *intervallo di tempo* :: *valore-ore* [:*valore-minuti* [:*secondi-valore* ]  
  
 &#124; *minutes-value* [:*seconds-value* ]  
  
 &#124; *secondi-valore*  
  
 *years-value* :: valore *datetime*  
  
 *months-value* :: *valore-datetime*  
  
 *days-valore* :: : *valore datetime*  
  
 *hours-value* :: valore *datetime*  
  
 *minuti-valore* :: valore *datetime*  
  
 *seconds-value* :: : *seconds-integer-value* [.[ *secondi-frazione*] ]  
  
 *seconds-integer-valore* :: *: Unsigned-integer*  
  
 *secondi-frazione* :: *: Unsigned-integer*  
  
 *valore_datetime* :: *: Unsigned-integer*  
  
 *interval-qualifier* :: : *campo di inizio* A campo *finale* &#124; *single-datetime-field*  
  
 *campo-inizio* :: : *campo non-second-datetime-field* [(*interval-leading-field-precision* )]  
  
 *end-field* :: : *campo non-second-datetime-&#124;* SECOND[(*intervallo-frazionario-secondi-precisione*)]  
  
 *single-datetime-field* :: : *campo non-second-datetime-field* [(*interval-leading-field-precision*)] &#124; SECOND[(*interval-leading-field-precision* [, (*intervallo-frazionario-secondi-precisione*)]  
  
 *datetime-field* :: *: campo non-second-datetime-field* &#124; SECOND  
  
 *non-secondo datetime-field* :: : ANNO &#124; MESE &#124; GIORNO &#124; ORA &#124; MINUTE  
  
 *intervallo frazionario-secondi-precisione* :: : *Unsigned-integer*  
  
 *interval-leading-field-precision* :: : *Unsigned-integer*  
  
 *citazione* ::  
  
 *unsigned-integer* :: *cifra...*
