---
title: Limitazioni del nome della tabella Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC SQL grammar, table name limitations
- table name limitations [ODBC]
- Excel driver [ODBC], table name limitations
ms.assetid: d9843e4b-1d05-4d5a-9dc3-ee9ec59edb97
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 738c563961eae56471f0238d9726a1ebb0bdc76e
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81289217"
---
# <a name="table-name-limitations"></a>Limitazioni dei nomi di tabella
I nomi di tabella possono contenere qualsiasi carattere valido (ad esempio, spazi). Se i nomi delle tabelle contengono caratteri ad eccezione di lettere, numeri e caratteri di sottolineatura, il nome deve essere delimitato racchiudendolo tra virgolette rovesciate (').  
  
 Quando viene utilizzato il driver di Microsoft Excel e un nome di tabella non è qualificato da un riferimento al database, il database predefinito è implicito. Se un nome in Microsoft Excel include il carattere "!", verrà convertito automaticamente nel carattere "".< .  
  
 Il nome della tabella \<di Microsoft Excel che fa riferimento a filename> è supportato per i file di Microsoft Excel 3.0 e 4.0. Il nome della tabella \<di Microsoft Excel che fa riferimento a> nome cartella di lavoro è supportato per i file di Microsoft Excel 5.0, 7.0 o 97.  
  
 Quando si utilizza il driver dBASE, i caratteri con un valore ASCII maggiore di 127 vengono convertiti in caratteri di sottolineatura.  
  
 Quando viene utilizzato il driver di Microsoft Access, il nome della tabella è limitato a 64 caratteri.  
  
 Quando si utilizza il driver dBASE, Microsoft Excel 3.0 o 4.0, Paradox o Text, le parole chiave speciali di MS-DOS CON, AUX, LPT1 e LPT2 non devono essere utilizzate come nomi di tabella.
