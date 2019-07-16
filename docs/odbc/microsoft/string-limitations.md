---
title: Limitazioni di stringhe | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 7faab41bd52397ac0d352e04a9ec153571e93f1e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67948767"
---
# <a name="string-limitations"></a>Limitazioni delle stringhe
La lunghezza massima della stringa istruzione SQL è 65.000 caratteri.  
  
 Quando viene usato il driver Microsoft Access, sono supportate solo le costanti stringa SQL-92 (tra virgolette singole, virgolette doppie non).  
  
 Il carattere barra verticale (&#124;) non può essere usata in una stringa, se il carattere è racchiuso tra virgolette back o non.  
  
 Per garantire la massima interoperabilità, le applicazioni devono passare stringhe nei parametri, anziché il passaggio tra virgolette stringhe.
