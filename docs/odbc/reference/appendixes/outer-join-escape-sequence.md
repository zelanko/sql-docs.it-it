---
title: Sequenza di fuga Outer Join Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- outer join escape sequence [ODBC]
- escape sequences [ODBC], outer join
- ODBC escape sequences [ODBC], outer join
ms.assetid: 2cfd1525-6677-4d36-9b9e-730496853750
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 37ce446328d263f492cdfd369f6e8f9f64fe6dfc
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303612"
---
# <a name="outer-join-escape-sequence"></a>Sequenza di escape outer join
ODBC utilizza sequenze di escape per outer join. La sintassi di questa sequenza di escape è la seguente:The syntax of this escape sequence is as follows:  
  
```  
{oj outer-join}  
```  
  
## <a name="remarks"></a>Osservazioni  
 Nella notazione BNF, la sintassi è la seguente:  
  
 *ODBC-outer-join-escape* ::  
  
 *ODBC-esc-initiator* oj *outer-join ODBC-esc-terminator*  
  
 *outer-join* :: : *nome-tabella* [*nome-correlazione*] - SINISTRA &#124; DESTRA &#124; FULL  
  
 OUTER JOIN :*nome-tabella* [*nome-correlazione*] &#124; *outer-join*- ON  
  
 *ricerca-*  
  
 *Condizione*  
  
 *nome-correlazione* :: : *nome definito dall'utente*  
  
 *ODBC-esc-initiator* ::  
  
 *Carattere di terminazione ODBC-esc::: *  
  
 Per determinare quali parti di questa istruzione sono supportate, un'applicazione chiama **SQLGetInfo** con il tipo di informazioni SQL_OJ_CAPABILITIES. Per gli outer join, *search-condition* deve contenere solo la condizione di join tra i *nomi di tabella*specificati.
