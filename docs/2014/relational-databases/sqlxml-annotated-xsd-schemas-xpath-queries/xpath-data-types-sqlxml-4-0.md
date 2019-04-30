---
title: Tipi di dati XPath (SQLXML 4.0) | Documenti di Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- mapping XDR types to XPath types [SQLXML]
- data types [XPath]
- arithmetic operators
- mapping data types [SQLXML]
- relational operators [SQLXML]
- node-set [SQLXML]
- data types [SQLXML], XPath
- XPath operators [SQLXML]
- XDR data type [SQLXML]
- equality operators [SQLXML]
- XPath conversions [SQLXML]
- converting data types [SQLXML]
- Boolean operators
- XPath queries [SQLXML], data types
- XPath data types [SQLXML]
- operators [SQLXML]
ms.assetid: a90374bf-406f-4384-ba81-59478017db68
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: b490a0f4876f911923ed0429f33d332b96768792
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63131339"
---
# <a name="xpath-data-types-sqlxml-40"></a>Tipi di dati XPath (SQLXML 4.0)
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], XPath e gli elementi XML Schema (XSD) utilizzano tipi di dati molto diversi. XPath, ad esempio, non include tipi di dati integer o di data, mentre [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e XSD ne includono diversi. XSD utilizza una precisione in nanosecondi per i valori di ora, mentre [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilizza al massimo una precisione di 1/300 secondi. Di conseguenza, il mapping di un tipo di dati a un altro non è sempre possibile. Per ulteriori informazioni sul mapping [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] i tipi di dati ai tipi di dati XSD, vedere [coercizioni di tipi di dati e l'annotazione SQL: DataType &#40;SQLXML 4.0&#41;](../sqlxml-annotated-xsd-schemas-using/data-type-coercions-and-the-sql-datatype-annotation-sqlxml-4-0.md).  
  
 XPath utilizza tre tipi di dati: `string`, `number` e `boolean`. Il tipo di dati `number` corrisponde sempre a un valore IEEE 754 a virgola mobile con precisione doppia. Il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] `float(53)` tipo di dati è il più vicino a XPath `number`. `float(53)`, tuttavia, non è esattamente un valore IEEE 754. Ad esempio, non viene utilizzato né un valore diverso da un numero (NaN, Not-a-Number) né un valore infinito. Eventuali tentativi di convertire una stringa non numerica in `number` e di dividere per zero restituiscono un errore.  
  
## <a name="xpath-conversions"></a>Conversioni XPath  
 Quando si utilizza una query XPath, ad esempio `OrderDetail[@UnitPrice > "10.0"]`, le conversioni dei tipi di dati implicite ed esplicite possono modificare impercettibilmente il significato della query. È pertanto importante comprendere le modalità di implementazione dei tipi di dati XPath. La specifica del linguaggio XPath, XML Path Language (XPath) version 1.0 W3C Proposed Recommendation 8 October 1999, visitare il sito Web W3C all'indirizzo http://www.w3.org/TR/1999/PR-xpath-19991008.html.  
  
 Gli operatori XPath sono suddivisi in quattro categorie:  
  
-   Operatori booleani (and, or)  
  
-   Operatori relazionali (\<, >, \<=, > =)  
  
-   Operatori di uguaglianza (=, !=)  
  
-   Operatori aritmetici: (+, -, *, div, mod)  
  
 Ogni categoria di operatore converte in modo diverso gli operandi. Se necessario, gli operatori XPath convertono gli operandi in modo implicito. Gli operatori aritmetici convertono gli operandi in `number` e restituiscono un valore numerico. Gli operatori booleani convertono gli operandi in `boolean` e restituiscono un valore booleano. Gli operatori relazionali e gli operatori di uguaglianza restituiscono un valore booleano, ma utilizzano regole di conversione diverse a seconda dei tipi di dati originali degli operandi, come illustrato nella tabella seguente.  
  
|Operando|Operatore relazionale|Operatore di uguaglianza|  
|-------------|-------------------------|-----------------------|  
|Entrambi gli operandi sono set di nodi.|TRUE solo se è presente un nodo in un set e un nodo nel secondo set in modo tale che il confronto dei rispettivi valori `string` sia TRUE.|Idem|  
|Uno è un set di nodi, l'altro è un valore `string`.|TRUE solo se è presente un nodo nel set di nodi in modo tale che, se convertito in `number`, il confronto con il valore `string` convertito in `number` sia TRUE.|TRUE solo se è presente un nodo nel set di nodi in modo tale che, se convertito in `string`, il confronto con il valore `string` sia TRUE.|  
|Uno è un set di nodi, l'altro è un valore `number`.|TRUE solo se è presente un nodo nel set di nodi in modo tale che, se convertito in `number`, il confronto con il valore `number` sia TRUE.|Idem|  
|Uno è un set di nodi, l'altro è un valore `boolean`.|TRUE solo se è presente un nodo nel set di nodi in modo tale che, se convertito in `boolean` e quindi in `number`, il confronto con il valore `boolean` convertito in `number` sia TRUE.|TRUE solo se è presente un nodo nel set di nodi in modo tale che, se convertito in `boolean`, il confronto con il valore `boolean` sia TRUE.|  
|Nessuno è un set di nodi.|Convertire entrambi gli operandi in `number` e quindi eseguire il confronto.|Convertire entrambi gli operandi in un tipo comune e quindi eseguire il confronto. Convertire in `boolean` se uno degli operandi è `boolean`, in `number` se uno degli operandi è `number`; in caso contrario, convertire in `string`.|  
  
> [!NOTE]  
>  Poiché gli operatori relazionali XPath convertono sempre gli operandi in `number`, i confronti `string` non sono possibili. Per includere confronti relativi alla data, SQL Server 2000 è disponibile una variazione alla specifica XPath: Quando un operatore relazionale Confronta un `string` a un `string`, un set di nodi un `string`, un con valori di stringa di set di nodi in un stringa con valori di set di nodi, o un `string` confronto (non un `number` confronto) viene eseguita.  
  
## <a name="node-set-conversions"></a>Conversioni dei set di nodi  
 Le conversioni dei set di nodi non sono sempre intuitive. Un set di nodi viene convertito in un tipo `string` assumendo il valore stringa solo del primo nodo nel set. Un set di nodi viene convertito in `number` tramite la conversione in `string` e quindi convertendo `string` in `number`. Un set di nodi viene convertito in `boolean` verificandone l'esistenza.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non esegue la selezione della posizione nei set di nodi: la query XPath `Customer[3]`, ad esempio, indica il terzo cliente. Questo tipo di selezione della posizione non è supportato in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Pertanto, le conversioni node-set-to-`string` o node-set-to-`number` come descritto dalla specifica XPath non sono implementate. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilizza le semantiche "any" dove la specifica XPath specifica la semantica "first". Ad esempio, basato sulla specifica W3C XPath, la query XPath `Order[OrderDetail/@UnitPrice > 10.0]` seleziona gli ordini con il primo **OrderDetail** con un **UnitPrice** maggiore di 10.0. Nelle [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], la query XPath seguente seleziona gli ordini con qualsiasi **OrderDetail** con un **UnitPrice** maggiore di 10.0.  
  
 La conversione in `boolean` genera un test di esistenza e, pertanto, la query XPath `Products[@Discontinued=true()]` equivale all'espressione SQL "Products.Discontinued is not null", non all'espressione SQL "Products.Discontinued = 1". Per rendere la query equivalente all'espressione SQL successiva, convertire innanzitutto il set di nodi in un tipo non `boolean`, ad esempio `number`. Ad esempio `Products[number(@Discontinued) = true()]`.  
  
 Poiché la maggior parte degli operatori viene definita come TRUE se gli operatori sono TRUE per tutti i nodi nel set di nodi o per uno di essi, queste operazioni restituiscono sempre FALSE se il set di nodi è vuoto. In questo modo, se A è vuoto, sia `A = B` sia `A != B` sono FALSE e `not(A=B)` e `not(A!=B)` sono TRUE.  
  
 In genere è presente un attributo o un elemento con mapping a una colonna se il valore della colonna nel database non è `null`. Sono presenti elementi di cui è stato eseguito il mapping a righe se è presente uno qualunque dei figli.  
  
> [!NOTE]  
>  Gli elementi annotati con `is-constant` sono sempre presenti. Di conseguenza, i predicati XPath non possono essere utilizzati in elementi `is-constant`.  
  
 Quando un set di nodi viene convertito in `string` o `number`, il tipo XDR (se presente) viene controllato nello schema con annotazioni e viene utilizzato per determinare la conversione necessaria.  
  
## <a name="mapping-xdr-data-types-to-xpath-data-types"></a>Mapping di tipi di dati XDR a tipi di dati XPath  
 Il tipo di dati XPath di un nodo viene derivato dal tipo di dati XDR nello schema, come illustrato nella tabella seguente (il nodo **EmployeeID** viene usato a scopo illustrativo).  
  
|Tipo di dati XDR|Equivalente<br /><br /> Tipo di dati XPath|Conversione SQL Server utilizzata|  
|-------------------|------------------------------------|--------------------------------|  
|Nonebin.base64bin.hex|N/D|NoneEmployeeID|  
|boolean|boolean|CONVERT(bit, EmployeeID)|  
|number, int, float, i1, i2, i4, i8,r4, r8ui1, ui2, ui4, ui8|number|CONVERT(float(53), EmployeeID)|  
|id, idref, idrefsentity, entities, enumerationnotation, nmtoken, nmtokens, chardate, Timedate, Time.tz, string, uri, uuid|string|CONVERT(nvarchar(4000), EmployeeID, 126)|  
|fixed14.4|N/D (in XPath non è disponibile alcun tipo di dati equivalente al tipo di dati XDR fixed14.4).|CONVERT(money, EmployeeID)|  
|Data|string|LEFT(CONVERT(nvarchar(4000), EmployeeID, 126), 10)|  
|time<br /><br /> time.tz|string|SUBSTRING(CONVERT(nvarchar(4000), EmployeeID, 126), 1 + CHARINDEX(N'T', CONVERT(nvarchar(4000), EmployeeID, 126)), 24)|  
  
 Le conversioni di data e ora sono progettate per funzionare se il valore viene archiviato nel database utilizzando la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] `datetime` tipo di dati o un `string`. Si noti che il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] `datetime` tipo di dati non utilizza `timezone` e ha una precisione minore rispetto a XML `time` tipo di dati. Per includere il tipo di dati `timezone` o aggiungere ulteriore precisione, archiviare i dati in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilizzando un tipo `string`.  
  
 Quando un nodo viene convertito dal relativo tipo di dati XDR al tipo di dati XPath, è talvolta necessaria un'ulteriore conversione (da un tipo di dati XPath a un altro tipo di dati XPath). Si consideri, ad esempio, la query XPath seguente:  
  
```  
(@m + 3) = 4  
```  
  
 Se @m è del `fixed14.4` tipo di dati XDR, la conversione dal tipo di dati XDR al tipo di dati viene eseguito con XPath:  
  
```  
CONVERT(money, m)  
```  
  
 In questa conversione il nodo `m` viene convertito da `fixed14.4` a `money`. Per aggiungere il valore 3, tuttavia, è necessaria un'ulteriore conversione:  
  
```  
CONVERT(float(CONVERT(money, m))  
```  
  
 L'espressione XPath viene valutata nel modo seguente:  
  
```  
CONVERT(float(CONVERT(money, m)) + CONVERT(float(53), 3) = CONVERT(float(53), 3)  
```  
  
 Come illustrato nella tabella seguente, si tratta della stessa conversione applicata per altre espressioni XPath, ad esempio i valori letterali o le espressioni composte.  
  
||||||  
|-|-|-|-|-|  
||X non è noto|X è `string`|X è `number`|X è `boolean`|  
|string(X)|CONVERT (nvarchar(4000), X, 126)|-|CONVERT (nvarchar(4000), X, 126)|CASE WHEN X THEN N'true' ELSE N'false' END|  
|number(X)|CONVERT (float(53), X)|CONVERT (float(53), X)|-|CASE WHEN X THEN 1 ELSE 0 END|  
|boolean(X)|-|LEN(X) > 0|X != 0|-|  
  
## <a name="examples"></a>Esempi  
  
### <a name="a-convert-a-data-type-in-an-xpath-query"></a>A. Convertire un tipo di dati in una query XPath  
 Nella query XPath seguente specificata su uno schema XSD con annotazione, la query Seleziona tutti i **dipendente** nodi con il **EmployeeID** attributo valore 1, dove "E-" è il prefisso specificato utilizzando il `sql:id-prefix` annotazione.  
  
 `Employee[@EmployeeID="E-1"]`  
  
 Il predicato nella query equivale all'espressione SQL:  
  
 `N'E-' + CONVERT(nvarchar(4000), Employees.EmployeeID, 126) = N'E-1'`  
  
 Poiché **EmployeeID** è uno del `id` (`idref`, `idrefs`, `nmtoken`, `nmtokens`e così via) i valori tipo di dati nello schema XSD **EmployeeID** è convertito nel `string` tipo di dati XPath utilizzando le regole di conversione descritte in precedenza.  
  
 `CONVERT(nvarchar(4000), Employees.EmployeeID, 126)`  
  
 Il prefisso "E-" viene aggiunto alla stringa, e il risultato viene quindi confrontato con `N'E-1'`.  
  
### <a name="b-perform-several-data-type-conversions-in-an-xpath-query"></a>B. Eseguire diverse conversioni dei tipi di dati in una query XPath  
 Considerare la seguente query XPath specificata su uno schema XSD con annotazioni: `OrderDetail[@UnitPrice * @OrderQty > 98]`  
  
 Questa query XPath restituisce tutti i  **\<OrderDetail >** gli elementi che soddisfano il predicato `@UnitPrice * @OrderQty > 98`. Se il **UnitPrice** annotato con un `fixed14.4` tipo di dati nello schema con annotazione, questo predicato è equivalente all'espressione SQL:  
  
 `CONVERT(float(53), CONVERT(money, OrderDetail.UnitPrice)) * CONVERT(float(53), OrderDetail.OrderQty) > CONVERT(float(53), 98)`  
  
 Nel convertire i valori nella query XPath, la prima operazione converte il tipo di dati XDR nel tipo di dati XPath. Poiché il tipo di dati XSD del **UnitPrice** è `fixed14.4`, come descritto nella tabella precedente, si tratta della prima conversione utilizzata:  
  
```  
CONVERT(money, OrderDetail.UnitPrice))   
```  
  
 Poiché gli operatori aritmetici convertono gli operandi nel tipo di dati XPath `number`, viene applicata la seconda conversione (da un tipo di dati XPath a un altro tipo di dati XPath), in cui il valore viene convertito in `float(53)`. `float(53)` è simile al tipo di dati XPath `number`:  
  
```  
CONVERT(float(53), CONVERT(money, OrderDetail.UnitPrice))   
```  
  
 Supponendo che il **OrderQty** attributo non dispone di alcun tipo di dati XSD **OrderQty** viene convertito in un `number` tipo di dati XPath in una singola conversione:  
  
```  
CONVERT(float(53), OrderDetail.OrderQty)  
```  
  
 Analogamente, il valore 98 viene convertito nel tipo di dati XPath `number`:  
  
```  
CONVERT(float(53), 98)  
```  
  
> [!NOTE]  
>  Se il tipo di dati XSD utilizzato nello schema non è compatibile con il tipo di dati di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sottostante nel database o se viene eseguita una conversione del tipo di dati XPath non consentita, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] può restituire un errore. Ad esempio, se il **EmployeeID** attributo è annotato con `id-prefix` annotazione, l'espressione XPath `Employee[@EmployeeID=1]` genera un errore, in quanto **EmployeeID** ha il `id-prefix` annotazione e non può essere convertito in `number`.  
  
  
