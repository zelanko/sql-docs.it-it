---
description: Limitazioni delle stringhe
title: Limitazioni di stringa | Microsoft Docs
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
ms.openlocfilehash: c21d86a3c626ced52c6b7915d3cfbd9322fb596e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88449133"
---
# <a name="string-limitations"></a>Limitazioni delle stringhe
La lunghezza massima di una stringa di istruzione SQL è di 65.000 caratteri.  
  
 Quando si utilizza il driver Microsoft Access, sono supportate solo le costanti di stringa SQL-92 (con virgolette singole, non virgolette doppie).  
  
 Il carattere barra verticale (&#124;) non può essere usato in una stringa, indipendentemente dal fatto che il carattere sia racchiuso tra virgolette.  
  
 Per garantire la massima interoperabilità, le applicazioni devono passare stringhe nei parametri, anziché passare stringhe tra virgolette.
