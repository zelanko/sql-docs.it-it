---
title: Sequenze di escape GUID - Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC escape sequences [ODBC], GUID
- escape sequences [ODBC], guid
- guid escape sequence [ODBC]
ms.assetid: 71d43ef9-4a31-493e-b9e0-f864e9ef3ce6
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 44907bfbd884bf361ce5f2ab8b3f6d8a247aba44
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306972"
---
# <a name="guid-escape-sequences"></a>Sequenze di escape GUID
ODBC utilizza sequenze di escape per i valori letterali GUID. La sintassi di questa sequenza di escape è la seguente:The syntax of this escape sequence is as follows:  
  
```  
{guid 'nnnnnnnn-nnnn-nnnn-nnnn-nnnnnnnnnnnn'}  
```  
  
## <a name="remarks"></a>Osservazioni  
 Nella notazione BNF, la sintassi è la seguente:  
  
 *ODBC-guid-escape* ::  
     *GUID dell'intestatore ODBC-esc* '*guid-value*' *ODBC-esc-terminator*  
  
 *ODBC-esc-initiator* ::  
  
 *Carattere di terminazione ODBC-esc::: *  
  
 *guid-valore* :: *clock-basso-valore guid-separatore clock-medio-valore guid-separator clock-alto-valore guid-separatore clock-seq-valore valore nodo-separatore*  
  
 *separatore guid* ::  
  
 *c'era il valore di hex_digit* hex_digit hex_digit hex_digit hex_digit hex_digit *hex_digit* hex_digit hex_digit  
  
 *clock-middle-value* :: *: hex_digit hex_digit hex_digit hex_digit*  
  
 *c'è un valore alto* :: hex_digit *hex_digit hex_digit hex_digit hex_digit*  
  
 *clock-seq-value* :: *hex_digit hex_digit hex_digit hex_digit hex_digit*  
  
 *clock-node-value* :: hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit *hex_digit hex_digit* hex_digit  
  
 *hex_digit* :: 0 &#124; 1 &#124; 2 &#124; 3 &#124; &#124; 5 &#124; 6 &#124; &#124; 7 &#124; &#124; 9 &#124; a &#124; B &#124; C &#124; D &#124; &#124; F  
  
 La sequenza di escape del valore letterale GUID è supportata se il tipo di dati GUID è supportato dall'origine dati. Un'applicazione deve chiamare **SQLGetTypeInfo** per determinare se questo tipo di dati è supportato.
