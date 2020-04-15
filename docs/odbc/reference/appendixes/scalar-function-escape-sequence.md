---
title: Sequenza di escape della funzione scalare Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- escape sequences [ODBC], scalar function
- scalar functions [ODBC], escape sequences
- ODBC escape sequences [ODBC], scalar function
ms.assetid: aaf5d516-e090-445f-8839-9e39581c69c7
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8347b8e6f0fab6dffc5295fb3b8260a6a56ed123
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305074"
---
# <a name="scalar-function-escape-sequence"></a>Sequenza di escape per funzioni scalari
ODBC utilizza sequenze di escape per le funzioni scalari. La sintassi di questa sequenza di escape è la seguente:The syntax of this escape sequence is as follows:  
  
```  
{fn scalar-function}  
```  
  
## <a name="remarks"></a>Osservazioni  
 Nella notazione BNF, la sintassi è la seguente:  
  
 *ODBC-scalar-function-escape* ::  
  
 *ODBC-esc-initiator* fn *scalare-funzione ODBC-esc-terminator*  
  
 *funzione scalare* :: *: nome-funzione* (*elenco-argomenti*)  
  
 Le definizioni per il *nonterminals function-name* e *function-name* (*argument-list*) derivano dall'elenco di funzioni scalari [nell'Appendice E: Funzioni scalari](../../../odbc/reference/appendixes/appendix-e-scalar-functions.md).)  
  
 *ODBC-esc-initiator* ::  
  
 *Carattere di terminazione ODBC-esc::: *  
  
 Per determinare se l'origine dati supporta le procedure e il driver supporta la sintassi di chiamata della procedura ODBC, un'applicazione può chiamare **SQLGetInfo**. Per ulteriori informazioni, vedere [Appendice E: Funzioni scalari](../../../odbc/reference/appendixes/appendix-e-scalar-functions.md).
