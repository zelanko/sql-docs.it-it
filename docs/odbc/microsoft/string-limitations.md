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
manager: craigg
ms.openlocfilehash: 003cd318d6db54c7547375219805c63cfc4ce249
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63269872"
---
# <a name="string-limitations"></a>Limitazioni delle stringhe
La lunghezza massima della stringa istruzione SQL è 65.000 caratteri.  
  
 Quando viene usato il driver Microsoft Access, sono supportate solo le costanti stringa SQL-92 (tra virgolette singole, virgolette doppie non).  
  
 Il carattere barra verticale (&#124;) non può essere usata in una stringa, se il carattere è racchiuso tra virgolette back o non.  
  
 Per garantire la massima interoperabilità, le applicazioni devono passare stringhe nei parametri, anziché il passaggio tra virgolette stringhe.
