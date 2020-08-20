---
description: Sequenza di escape outer join
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 22517e676f9f8ac80622d368edcdb5a0ce1b283f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88466093"
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
