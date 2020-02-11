---
title: Funzioni XQuery per il tipo di dati XML | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- XQuery, functions
- xml data type [SQL Server], XQuery
- functions [SQL Server], XQuery
ms.assetid: 8df0877d-a03f-4ca9-b84e-908c4bb42b5e
author: rothja
ms.author: jroth
ms.openlocfilehash: e885b537fbc86f3b70a8142c5513dbf16cb1c158
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "67945991"
---
# <a name="xquery-functions-against-the-xml-data-type"></a>Funzioni XQuery per il tipo di dati XML
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  In questo argomento e nei relativi argomenti secondari vengono descritte le funzioni che è possibile utilizzare quando si specifica XQuery sul tipo di dati **XML** . Per le specifiche W3C, vedere [http://www.w3.org/TR/2004/WD-xpath-functions-20040723](https://go.microsoft.com/fwlink/?LinkId=4873).  
  
 Le funzioni XQuery appartengono allo http://www.w3.org/2004/07/xpath-functions spazio dei nomi. Le specifiche W3C utilizzano il prefisso "fn:" dello spazio dei nomi per la descrizione di queste funzioni. Quando si utilizzano le funzioni non è necessario specificare esplicitamente il prefisso "fn:". Per questo motivo e per migliorare la leggibilità, in questa documentazione i prefissi dello spazio dei nomi sono in genere omessi.  
  
 Nella tabella seguente sono elencate le funzioni XQuery supportate per il tipo di dati **XML**.  
  
|Category|Nome funzione|  
|--------------|-------------------|  
|[Funzioni su valori numerici](https://msdn.microsoft.com/library/d5740a32-b174-43b9-b64d-1cc6edc50cff)|[Ceiling](../xquery/numeric-values-functions-ceiling.md)|  
||[Floor](../xquery/numeric-values-functions-floor.md)|  
||[turno](../xquery/numeric-values-functions-round.md)|  
|[Funzioni XQuery su valori stringa](https://msdn.microsoft.com/library/2dccefef-5d90-4f56-bda7-4c1954d8a730)|[Concat](../xquery/functions-on-string-values-concat.md)|  
||[contiene](../xquery/functions-on-string-values-contains.md)|  
||[sottostringa](../xquery/functions-on-string-values-substring.md)|  
||[Funzione lower-case &#40;XQuery&#41;](../xquery/functions-on-string-values-lower-case.md)|  
||[Lunghezza stringa](../xquery/functions-on-string-values-string-length.md)|  
||[Funzione Upper-Case &#40;XQuery&#41;](../xquery/functions-on-string-values-upper-case.md)|  
|Funzioni su valori booleani|[non](../xquery/functions-on-boolean-values-not-function.md)|  
|[Funzioni sui nodi](https://msdn.microsoft.com/library/09a8affa-3341-4f50-aebc-fdf529e00c08)|[number](../xquery/functions-on-nodes-number.md)|  
||[Funzione local-name (XQuery)](../xquery/functions-on-nodes-local-name.md)|  
||[Funzione namespace-uri (XQuery)](../xquery/functions-on-nodes-namespace-uri.md)|  
|[Funzioni di contesto](https://msdn.microsoft.com/library/f7d8af33-9de9-450c-a667-23dee3129b5f)|[Ultima](../xquery/context-functions-last-xquery.md)|  
||[posizione](../xquery/context-functions-position-xquery.md)|  
|[Funzioni per le sequenze](https://msdn.microsoft.com/library/672d2795-53ab-49c2-bf24-bc81a47ecd3f)|[vuoto](../xquery/functions-on-sequences-empty.md)|  
||[distinct-values](../xquery/functions-on-sequences-distinct-values.md)|  
||[Funzione id (XQuery)](../xquery/functions-on-sequences-id.md)|  
|[Funzioni di aggregazione &#40;XQuery&#41;](https://msdn.microsoft.com/library/be647ef1-291e-4a5d-ab18-07c759efe176)|[conteggio](../xquery/aggregate-functions-count.md)|  
||[AVG](../xquery/aggregate-functions-avg.md)|  
||[min](../xquery/aggregate-functions-min.md)|  
||[Max](../xquery/aggregate-functions-max.md)|  
||[somma](../xquery/aggregate-functions-sum.md)|  
|[Funzioni del costruttore &#40;XQuery&#41;](../xquery/constructor-functions-xquery.md)|[Funzioni costruttore](../xquery/constructor-functions-xquery.md)|  
|[Funzioni di accesso ai dati](../xquery/data-accessor-functions.md)|[stringa](../xquery/data-accessor-functions-string-xquery.md)|  
||[data](../xquery/data-accessor-functions-data-xquery.md)|  
|[Funzioni costruttore booleane &#40;XQuery&#41;](https://msdn.microsoft.com/library/fa907f39-d4b7-4495-b829-c788928e0f64)|[Funzione true (XQuery)](../xquery/boolean-constructor-functions-true-xquery.md)|  
||[Funzione false (XQuery)](../xquery/boolean-constructor-functions-false-xquery.md)|  
|[Funzioni correlate a QName &#40;XQuery&#41;](https://msdn.microsoft.com/library/7e07eb26-f551-4b63-ab77-861684faff71)|[expanded-QName (XQuery)](../xquery/functions-related-to-qnames-expanded-qname.md)|  
||[local-name-from-QName (XQuery)](../xquery/functions-related-to-qnames-local-name-from-qname.md)|  
||[namespace-uri-from-QName (XQuery)](../xquery/functions-related-to-qnames-namespace-uri-from-qname.md)|  
|[Funzioni per le estensioni XQuery di SQL Server](https://msdn.microsoft.com/library/4bc5d499-5fec-4c3f-b11e-5ab5ef9d8f97)|[Funzione sql:column() (XQuery)](../xquery/xquery-extension-functions-sql-column.md)|  
||[Funzione sql:variable() (XQuery)](../xquery/xquery-extension-functions-sql-variable.md)|  
  
## <a name="see-also"></a>Vedere anche  
 [metodi con tipo di dati XML](../t-sql/xml/xml-data-type-methods.md)   
 [Riferimento al linguaggio XQuery &#40;SQL Server&#41;](../xquery/xquery-language-reference-sql-server.md)   
 [Dati XML &#40;SQL Server&#41;](../relational-databases/xml/xml-data-sql-server.md)  
  
  
