---
title: Sequenze di escape GUID | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a74ed9d4dfe0afb8bf59abb11220a0677d000bfb
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "67947588"
---
# <a name="guid-escape-sequences"></a>Sequenze di escape GUID
ODBC utilizza sequenze di escape per i valori letterali GUID. La sintassi di questa sequenza di escape è la seguente:  
  
```  
{guid 'nnnnnnnn-nnnn-nnnn-nnnn-nnnnnnnnnnnn'}  
```  
  
## <a name="remarks"></a>Osservazioni  
 Nella notazione BNF la sintassi è la seguente:  
  
 *ODBC-GUID-Escape* :: =  
     *ODBC-ESC-initiator GUID* '*Guid-value*' *ODBC-ESC-Terminator*  
  
 *ODBC-ESC-initiator* :: = {  
  
 *ODBC-ESC-Terminator* :: =}  
  
 *GUID-valore* :: = clock-valore GUID-basso-valore-orologio separatore GUID-valore medio-orologio-separatore GUID-valore-valore di clock- *Seq-value GUID-valore-nodo-separatore*  
  
 *separatore GUID* :: =-  
  
 *Clock-low-value* :: = *hex_digit hex_digit hex_digit hex_digit* hex_digit hex_digit hex_digit hex_digit  
  
 *clock-valore medio* :: = *hex_digit hex_digit hex_digit hex_digit*  
  
 *Clock-High-Value* :: = *hex_digit hex_digit hex_digit hex_digit*  
  
 *clock-seq-value* :: = *hex_digit hex_digit hex_digit hex_digit*  
  
 *Clock-node-value* :: = *hex_digit hex_digit hex_digit hex_digit hex_digit* hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit  
  
 *hex_digit* :: = 0 &#124; 1 &#124; 2 &#124; 3 &#124; 4 &#124; 5 &#124; 6 &#124; 7 &#124; 8 &#124; 9 &#124; A &#124; B &#124; C &#124; D &#124; E &#124; F  
  
 La sequenza di escape dei valori letterali GUID è supportata se il tipo di dati GUID è supportato dall'origine dati. Un'applicazione deve chiamare **SQLGetTypeInfo** per determinare se questo tipo di dati è supportato.
