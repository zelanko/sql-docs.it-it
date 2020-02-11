---
title: Limitazioni del nome di colonna | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- desktop database drivers [ODBC], column names
- ODBC desktop database drivers [ODBC], column names
ms.assetid: 5a339f61-c52f-40ad-8deb-d785f72753d4
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 14e62555db2e88c6573f3bdca0d4a1a2733d428b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68006244"
---
# <a name="column-name-limitations"></a>Limitazioni dei nomi di colonna
I nomi di colonna possono contenere qualsiasi carattere valido, ad esempio spazi. Se i nomi di colonna contengono caratteri eccetto lettere, numeri e caratteri di sottolineatura, il nome deve essere racchiuso tra virgolette (').  
  
 Quando si utilizza il driver Microsoft Access o Microsoft Excel, i nomi delle colonne sono limitati a 64 caratteri e i nomi più lunghi generano un errore. Quando si usa il driver Paradox, il nome di colonna massimo è 25 caratteri. Quando si utilizza il driver di testo, il nome di colonna massimo è 64 caratteri e i nomi più lunghi vengono troncati.  
  
 Quando si usa il driver dBASE, i caratteri con un valore ASCII maggiore di 127 vengono convertiti in caratteri di sottolineatura.  
  
 Quando si utilizza il driver Microsoft Excel, se sono presenti nomi di colonna, è necessario che si trovino nella prima riga. Un nome che in Microsoft Excel utilizzerebbe il carattere "!" deve essere racchiuso tra virgolette ('). Il carattere "!" viene convertito nel carattere "$", perché il carattere "!" non è valido in un nome ODBC, anche quando il nome è racchiuso tra virgolette. Tutti gli altri caratteri validi di Microsoft Excel, ad eccezione del carattere barra verticale (&#124;)), possono essere usati in un nome di colonna, inclusi gli spazi. Per includere uno spazio, è necessario utilizzare un identificatore delimitato per il nome di una colonna di Microsoft Excel. I nomi di colonna non specificati verranno sostituiti con nomi generati dal driver, ad esempio, "col1" per la prima colonna.  
  
 Il carattere barra verticale (&#124;) non può essere utilizzato in un nome di colonna, indipendentemente dal fatto che il nome sia racchiuso tra virgolette.  
  
 Quando si utilizza il driver di testo, il driver fornisce un nome predefinito se non si specifica un nome di colonna. Ad esempio, il driver chiama la prima colonna F1, la seconda colonna F2 e così via.
