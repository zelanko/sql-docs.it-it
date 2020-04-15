---
title: Limitazioni delle stringhe Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC desktop database drivers [ODBC]
- desktop database drivers [ODBC]
ms.assetid: ec1da65f-c69d-415d-bf75-8fda8aa2b39f
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 61f81ff3da882095a0a6c41bb5061addd497a5d2
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306062"
---
# <a name="string-limitations"></a>Limitazioni delle stringhe
La lunghezza massima di una stringa di istruzione SQL è 65.000 caratteri.  
  
 Quando viene utilizzato il driver di Microsoft Access, sono supportate solo le costanti di stringa SQL-92 (con virgolette singole, non virgolette doppie).  
  
 Il carattere barra verticale (&#124;) non può essere utilizzato in una stringa, indipendentemente dal fatto che il carattere sia racchiuso o meno tra virgolette rovesciate.  
  
 Per garantire la massima interoperabilità, le applicazioni devono passare stringhe nei parametri, anziché passare stringhe tra virgolette.
