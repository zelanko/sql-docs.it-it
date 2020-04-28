---
title: local-name-from-QName (XQuery) | Microsoft Docs
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
- fn:local-name-from-QName function
- local-name-from-QName function
ms.assetid: fafed718-8c3c-403f-93ee-ec51fc157a6e
author: rothja
ms.author: jroth
ms.openlocfilehash: 765d412b9f3f0395a9bca6fd52c74135ddde3ff4
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "68004566"
---
# <a name="functions-related-to-qnames---local-name-from-qname"></a>Funzioni correlate a elementi QName - local-name-from-QName
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Restituisce XS: NCNAME che rappresenta la parte locale di QName specificata da *$arg*. Se *$arg* è una sequenza vuota, il risultato è una sequenza vuota.  
  
## <a name="syntax"></a>Sintassi  
  
```  
fn:local-name-from-QName($arg as xs:QName?) as xs:NCName?  
```  
  
## <a name="arguments"></a>Argomenti  
 *$arg*  
 QName da cui deve essere estratto il nome locale.  
  
## <a name="examples"></a>Esempi  
 In questo argomento vengono forniti esempi di XQuery sulle istanze XML archiviate **xml** in diverse colonne di tipo [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] XML nel database.  
  
 Nell'esempio seguente viene usata la funzione **local-name-from-QName ()** per recuperare le parti del nome locale e dell'URI dello spazio dei nomi da un valore di tipo QName. Nell'esempio vengono eseguite le operazioni seguenti:  
  
-   Viene creata una raccolta di XML Schema.  
  
-   Viene creata una tabella con una colonna di tipo XML. Il tipo XML viene tipizzato tramite la raccolta di XML Schema.  
  
-   Viene archiviata un'istanza XML di esempio nella tabella. Utilizzando il metodo **query ()** del tipo di dati XML, viene eseguita l'espressione di query per recuperare la parte del nome locale del valore del tipo QName dall'istanza di.  
  
```sql
DROP TABLE T  
go  
DROP XML SCHEMA COLLECTION SC  
go  
CREATE XML SCHEMA COLLECTION SC AS '  
<schema xmlns="http://www.w3.org/2001/XMLSchema"  
targetNamespace="QNameXSD" >  
      <element name="root" type="QName" nillable="true"/>  
</schema>'  
go  
  
CREATE TABLE T (xmlCol XML(SC))  
go  
-- following OK  
insert into T values ('<root xmlns="QNameXSD" xmlns:a="https://someURI">a:someLocalName</root>')  
 go  
-- Retrieve the local name.   
SELECT xmlCol.query('declare default element namespace "QNameXSD"; local-name-from-QName(/root[1])')  
FROM T  
-- Result = someLocalName  
-- You can retrieve namespace URI part from the QName using the namespace-uri-from-QName() function  
SELECT xmlCol.query('declare default element namespace "QNameXSD"; namespace-uri-from-QName(/root[1])')  
FROM T  
-- Result = https://someURI  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Funzioni correlate a QName &#40;XQuery&#41;](https://msdn.microsoft.com/library/7e07eb26-f551-4b63-ab77-861684faff71)  
  
  
