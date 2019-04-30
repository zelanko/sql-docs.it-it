---
title: Sintassi dei valori letterali intervallo | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d477dbc6b54d7ebd82b7e2ef8611f5f6dd807e83
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63188823"
---
# <a name="interval-literal-syntax"></a>Sintassi dei valori letterali intervallo
La sintassi seguente viene utilizzata per i valori letterali intervallo in ODBC.  
  
 *valore letterale di intervallo:: = intervallo* [+*&#124;*-] *intervallo-qualificatore della stringa di intervallo*  
  
 *interval-string* ::= *quote* { *year-month-literal* &#124; *day-time-literal* } *quote*  
  
 *year-month-literal* ::= *years-value* &#124; [*years-value* -] *months-value*  
  
 *day-time-literal* ::= *day-time-interval* &#124; *time-interval*  
  
 *day-time-interval* ::= *days-value* [*hours-value* [:*minutes-value*[:*seconds-value*]]]  
  
 *intervallo di tempo* :: = *-valore delle ore* [:*-valore dei minuti* [:*-valore dei secondi* ]]  
  
 &#124; *minutes-value* [:*seconds-value* ]  
  
 &#124; *seconds-value*  
  
 *valore dell'anno* :: = *valore datetime*  
  
 *months-value* ::= *datetime-value*  
  
 *valore di giorni* :: = *valore datetime*  
  
 *valore delle ore* :: = *valore datetime*  
  
 *valore dei minuti* :: = *valore datetime*  
  
 *seconds-value* ::= *seconds-integer-value* [.[*seconds-fraction*] ]  
  
 *seconds-integer-value* ::= *unsigned-integer*  
  
 *seconds-fraction* ::= *unsigned-integer*  
  
 *datetime-value* ::= *unsigned-integer*  
  
 *interval-qualifier* ::= *start-field* TO *end-field* &#124; *single-datetime-field*  
  
 *start-field* ::= *non-second-datetime-field* [(*interval-leading-field-precision* )]  
  
 *end-field* ::= *non-second-datetime-field* &#124; SECOND[(*interval-fractional-seconds-precision*)]  
  
 *campo datetime singolo* :: = *campo di data/ora secondo non* [(*intervallo leader-campo precisione*)] &#124; secondo [(*precisione-intervallo-leader-campo*  [, (*intervallo di--secondi-precisione frazionaria*)]  
  
 *datetime-field* ::= *non-second-datetime-field* &#124; SECOND  
  
 *campo di data/ora secondo non* :: = anno &#124; mese &#124; giorno &#124; ora &#124; minuti  
  
 *interval-fractional-seconds-precision* ::= *unsigned-integer*  
  
 *interval-leading-field-precision* ::= *unsigned-integer*  
  
 *quote* ::= '  
  
 *intero senza segno* :: = *cifra...*
