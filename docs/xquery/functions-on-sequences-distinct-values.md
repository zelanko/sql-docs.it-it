---
title: Funzione DISTINCT-values (XQuery) | Microsoft Docs
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
- distinct-values function
- fn:distinct-values function
ms.assetid: f4c2bb53-2bec-4f1a-9c00-cf997fb7ae5b
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 48b338416b7bd464a69c424354f4029c719fef33
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62939094"
---
# <a name="functions-on-sequences---distinct-values"></a>Funzioni su sequenze - distinct-values
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Rimuove valori duplicati dalla sequenza specificata da *$arg*. Se *$arg* è una sequenza vuota, la funzione restituisce una sequenza vuota.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
fn:distinct-values($arg as xdt:anyAtomicType*) as xdt:anyAtomicType*  
```  
  
## <a name="arguments"></a>Argomenti  
 *$arg*  
 Sequenza di valori atomici.  
  
## <a name="remarks"></a>Note  
 Tutti i tipi di valori atomizzati passati a **distinct-values()** devono essere sottotipi dello stesso tipo di base. Tipi di base accettati sono i tipi che supportano il **eq** operazione. Tra questi tipi sono inclusi i tre tipi di base numerici predefiniti, ovvero i tipi di base di data/ora xs:string, xs:boolean e xdt:untypedAtomic. Per i valori di tipo xdt:untypedAtomic viene eseguito il cast a xs:string. In presenza di una combinazione di questi tipi o nel caso in cui vengano passati altri valori di altri tipi, viene restituito un errore statico.  
  
 Il risultato del **distinct-values()** riceve il tipo di base dei tipi passati, ad esempio xs: String nel caso di xdt: untypedAtomic, con la cardinalità originale. Se l'input è una sequenza vuota calcolata in modo statico, la sequenza vuota è implicita e viene restituito un errore statico.  
  
 I valori di tipo xs:string vengono confrontati con le regole di confronto dei punti di codice Unicode predefinite XQuery.  
  
## <a name="examples"></a>Esempi  
 In questo argomento vengono forniti esempi di XQuery sulle istanze XML archiviate in diverse **xml** colonne di tipo nel database AdventureWorks.  
  
### <a name="a-using-the-distinct-values-function-to-remove-duplicate-values-from-the-sequence"></a>A. Utilizzo della funzione distinct-values() per rimuovere valori duplicati dalla sequenza  
 In questo esempio, un'istanza XML che contiene i numeri di telefono viene assegnata a un **xml** variabile di tipo. La query XQuery specificata su tale variabile utilizza il **distinct-values()** funzione per compilare un elenco di numeri di telefono che non contengono duplicati.  
  
```  
declare @x xml  
set @x = '<PhoneNumbers>  
 <Number>111-111-1111</Number>  
 <Number>111-111-1111</Number>  
 <Number>222-222-2222</Number>  
</PhoneNumbers>'  
-- 1st select  
select @x.query('  
  distinct-values( data(/PhoneNumbers/Number) )  
') as result  
```  
  
 Questo è il risultato:  
  
```  
111-111-1111 222-222-2222    
```  
  
 Nella query seguente, una sequenza di numeri (1, 1, 2) viene passata per il **distinct-values()** (funzione). La funzione rimuove quindi il duplicato dalla sequenza e restituisce gli altri due.  
  
```  
declare @x xml  
set @x = ''  
select @x.query('  
  distinct-values((1, 1, 2))  
') as result  
```  
  
 La query restituisce 1 2.  
  
### <a name="implementation-limitations"></a>Limitazioni di implementazione  
 Limitazioni:  
  
-   Il **distinct-values()** funzione esegue il mapping di valori interi a xs: decimal.  
  
-   Il **distinct-values()** funzione solo supporta i tipi menzionati in precedenza e non supporta la combinazione di tipi di base.  
  
-   Il **distinct-values()** funzione su valori xs: Duration non è supportata.  
  
-   Non è supportata l'opzione sintattica che fornisce le regole di confronto.  
  
## <a name="see-also"></a>Vedere anche  
 [Funzioni XQuery per il tipo di dati XML](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
