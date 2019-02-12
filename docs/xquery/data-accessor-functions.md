---
title: Funzioni di accesso dati | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- data-accessor functions [XQuery]
ms.assetid: 31bad04f-7c74-4773-9f83-612704fdd21c
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 1c28f61a39e45ea101f2e999d5787dfa23cb29c2
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/11/2019
ms.locfileid: "56031792"
---
# <a name="data-accessor-functions"></a>Funzioni di accesso ai dati
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Negli argomenti di questa sezione vengono descritte le funzioni di accesso ai dati e viene fornito codice di esempio.  
  
## <a name="understanding-fndata-fnstring-and-text"></a>Informazioni su fn:data(), fn:string() e text()  
 XQuery include una funzione **fn:data()** per estrarre valori scalari tipizzati dai nodi, un test di nodo **Text ()** per restituire i nodi di testo e la funzione **fn:string()** che restituisce il valore di stringa di un nodo. L'utilizzo di tali funzioni non è tuttavia intuitivo. Di seguito vengono riportate le linee guida da seguire per il corretto utilizzo di tali funzioni in [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. L'istanza XML \<età > 12 \< /age > viene usato a scopo illustrativo.  
  
-   XML non tipizzati: /Age/Text () l'espressione di percorso restituisce il nodo di testo "12". La funzione fn:data(/age) restituisce il valore stringa "12", così come la funzione fn:string(/age).  
  
-   Dati XML tipizzati: L'espressione /Age/Text () restituisce un errore statico per qualsiasi tipizzata semplice \<età > elemento. La funzione fn:data(/age) restituisce invece il valore intero 12, mentre fn:string(/age) restituisce la stringa "12".  
  
## <a name="in-this-section"></a>In questa sezione  
  
-   [Funzione String &#40;XQuery&#41;](../xquery/data-accessor-functions-string-xquery.md)  
  
-   [Funzione data &#40;XQuery&#41;](../xquery/data-accessor-functions-data-xquery.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Espressioni di percorso &#40;XQuery&#41;](../xquery/path-expressions-xquery.md)  
  
  
