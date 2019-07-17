---
title: namespace-uri-from-QName (XQuery) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- fn:namespace-uri-from-QName function
- namespace-uri-from-QName function
ms.assetid: 4ab3f003-2a3b-4268-9e88-b615e35701b2
author: rothja
ms.author: jroth
ms.openlocfilehash: 96edefd5409520109e2b2155507dd8879ed4b0d3
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67946638"
---
# <a name="functions-related-to-qnames---namespace-uri-from-qname"></a>Funzioni correlate a elementi QName - namespace-uri-from-QName
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Restituisce una stringa che rappresenta l'uri dello spazio dei nomi dell'elemento QName specificato da *$arg*. Il risultato è una sequenza vuota se *$arg* è una sequenza vuota.  
  
## <a name="syntax"></a>Sintassi  
  
```  
namespace-uri-from-QName($arg as xs:QName?) as xs:string?  
```  
  
## <a name="arguments"></a>Argomenti  
 *$arg*  
 QName per il quale viene restituito l'URI dello spazio dei nomi.  
  
## <a name="examples"></a>Esempi  
 In questo argomento vengono forniti esempi di XQuery sulle istanze XML archiviate in diverse **xml** colonne di tipo nel database AdventureWorks.  
  
### <a name="a-retrieve-the-namespace-uri-from-a-qname"></a>R. Recuperare l'URI dello spazio dei nomi per un QName  
 Per un esempio funzionante, vedere [local-name-from-QName &#40;XQuery&#41;](../xquery/functions-related-to-qnames-local-name-from-qname.md).  
  
### <a name="implementation-limitations"></a>Limitazioni di implementazione  
 Limitazioni:  
  
-   Il **namespace-uri-from-QName()** funzione restituisce le istanze di xs: String anziché di xs: anyURI.  
  
## <a name="see-also"></a>Vedere anche  
 [Le funzioni correlate a elementi QName &#40;XQuery&#41;](https://msdn.microsoft.com/library/7e07eb26-f551-4b63-ab77-861684faff71)  
  
  
