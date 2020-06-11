---
title: namespace-URI-from-QName (XQuery) | Microsoft Docs
description: Informazioni su come usare la funzione namespace-URI-from-QName per recuperare l'URI dello spazio dei nomi di un QName.
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
ms.openlocfilehash: a0967e9dfd9392513da3925725930111a97da0c9
ms.sourcegitcommit: 5b7457c9d5302f84cc3baeaedeb515e8e69a8616
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/20/2020
ms.locfileid: "83689551"
---
# <a name="functions-related-to-qnames---namespace-uri-from-qname"></a>Funzioni correlate a elementi QName - namespace-uri-from-QName
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Restituisce una stringa che rappresenta l'URI dello spazio dei nomi del QName specificato da *$arg*. Se *$arg* è la sequenza vuota, il risultato è la sequenza vuota.  
  
## <a name="syntax"></a>Sintassi  
  
```  
namespace-uri-from-QName($arg as xs:QName?) as xs:string?  
```  
  
## <a name="arguments"></a>Argomenti  
 *$arg*  
 QName per il quale viene restituito l'URI dello spazio dei nomi.  
  
## <a name="examples"></a>Esempio  
 In questo argomento vengono forniti esempi di XQuery sulle istanze XML archiviate in diverse colonne di tipo **XML** nel database AdventureWorks.  
  
### <a name="a-retrieve-the-namespace-uri-from-a-qname"></a>A. Recuperare l'URI dello spazio dei nomi per un QName  
 Per un esempio funzionante, vedere [local-name-from-QName &#40;XQuery&#41;](../xquery/functions-related-to-qnames-local-name-from-qname.md).  
  
### <a name="implementation-limitations"></a>Limitazioni di implementazione  
 Limitazioni:  
  
-   La funzione **namespace-URI-from-QName ()** restituisce istanze di XS: String anziché di XS: anyURI.  
  
## <a name="see-also"></a>Vedere anche  
 [Funzioni correlate a QName &#40;XQuery&#41;](https://msdn.microsoft.com/library/7e07eb26-f551-4b63-ab77-861684faff71)  
  
  
