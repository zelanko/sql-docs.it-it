---
title: Sequenza di escape outer join | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 576fe7268ccf71a8c926f6b1124ebbf8a8c711b0
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68100646"
---
# <a name="outer-join-escape-sequence"></a>Sequenza di escape outer join
ODBC utilizza sequenze di escape per outer join. La sintassi di questa sequenza di escape è la seguente:  
  
```  
{oj outer-join}  
```  
  
## <a name="remarks"></a>Osservazioni  
 Nella notazione BNF la sintassi è la seguente:  
  
 *ODBC-outer join-Escape* :: =  
  
 *ODBC-ESC-initiator* GU *outer join ODBC-ESC-Terminator*  
  
 *outer join* :: = *nome-tabella* [*nome-correlazione*] {Left &#124; right &#124; Full}  
  
 OUTER JOIN {*nome-tabella* [*nome-correlazione*] &#124; *outer join*} in  
  
 *ricerca*  
  
 *condizione*  
  
 *Correlation-Name* :: = *nome-definito dall'utente*  
  
 *ODBC-ESC-initiator* :: = {  
  
 *ODBC-ESC-Terminator* :: =}  
  
 Per determinare quali parti dell'istruzione sono supportate, un'applicazione chiama **SQLGetInfo** con il tipo di informazioni SQL_OJ_CAPABILITIES. Per gli outer join, la *condizione di ricerca* deve contenere solo la condizione di join tra i nomi di *tabella*specificati.
