---
title: Tipi di dati XPath (SQLXML)XPath Data Types (SQLXML)
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
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
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 089b2b006d0159c63e480c8627762ac37dec98b8
ms.sourcegitcommit: a3f5c3742d85d21f6bde7c6ae133060dcf1ddd44
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/15/2020
ms.locfileid: "75247093"
---
# <a name="xpath-data-types-sqlxml-40"></a>Tipi di dati XPath (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], XPath e XML Schema (XSD) hanno tipi di dati molto diversi. XPath, ad esempio, non include tipi di dati integer o di data, mentre [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e XSD ne includono diversi. XSD utilizza una precisione in nanosecondi per i valori di ora, mentre [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilizza al massimo una precisione di 1/300 secondi. Di conseguenza, il mapping di un tipo di dati a un altro non è sempre possibile. Per ulteriori informazioni [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sul mapping dei tipi di dati ai tipi di dati XSD, vedere Coercizioni dei tipi di dati e il tipo di [dati sql:datatype Annotation &#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/data-type-coercions-and-the-sql-datatype-annotation-sqlxml-4-0.md).  
  
 In XPath sono disponibili tre tipi di dati: **string**, **number**e **boolean**. Il tipo di dati **number** è sempre un'iEEE 754 a virgola mobile a precisione doppia. Il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]tipo di dati **float(53)** è il più vicino al **numero**XPath. Tuttavia, **float(53)** non è esattamente IEEE 754. Ad esempio, non viene utilizzato né un valore diverso da un numero (NaN, Not-a-Number) né un valore infinito. Se si tenta di convertire una stringa non numerica in **numero** e se si tenta di dividere per zero, viene generato un errore.  
  
## <a name="xpath-conversions"></a>Conversioni XPath  
 Quando si utilizza una query XPath, ad esempio `OrderDetail[@UnitPrice > "10.0"]`, le conversioni dei tipi di dati implicite ed esplicite possono modificare impercettibilmente il significato della query. È pertanto importante comprendere le modalità di implementazione dei tipi di dati XPath. La specifica del linguaggio XPath, XPath (XML Path Language) versione 1.0 W3C Proposed Recommendation 8 http://www.w3.org/TR/1999/PR-xpath-19991008.htmlottobre 1999, è disponibile nel sito Web W3C all'indirizzo .  
  
 Gli operatori XPath sono suddivisi in quattro categorie:  
  
-   Operatori booleani (and, or)  
  
-   Operatori relazionali\<( \<, , >, , >)  
  
-   Operatori di uguaglianza (=, !=)  
  
-   Operatori aritmetici: (+, -, *, div, mod)  
  
 Ogni categoria di operatore converte in modo diverso gli operandi. Se necessario, gli operatori XPath convertono gli operandi in modo implicito. Gli operatori aritmetici convertono i loro operandi in **numeri**e generano un valore numerico. Gli operatori booleani convertono i relativi operandi in **booleano**e generano un valore booleano. Gli operatori relazionali e gli operatori di uguaglianza restituiscono un valore booleano, ma utilizzano regole di conversione diverse a seconda dei tipi di dati originali degli operandi, come illustrato nella tabella seguente.  
  
|Operando|Operatore relazionale|Operatore di uguaglianza|  
|-------------|-------------------------|-----------------------|  
|Entrambi gli operandi sono set di nodi.|TRUESe e solo se è presente un nodo in un set e un nodo nel secondo set in modo che il confronto dei relativi valori **stringa** sia TRUE.|Idem|  
|Uno è un set di nodi, l'altro una **stringa**.|TRUESe e solo se è presente un nodo nel set di nodi in modo che quando viene convertito in **number**, il confronto con la **stringa** convertita in **number** è TRUE.|TRUESe e solo se è presente un nodo nel set di nodi in modo che quando viene convertito in **stringa**, il confronto di esso con la **stringa** è TRUE.|  
|Uno è un set di nodi, l'altro un **numero**.|TRUESe e solo se è presente un nodo nel set di nodi in modo che quando viene convertito in **number**, il confronto con il **numero** è TRUE.|Idem|  
|Uno è un set di nodi, l'altro un **valore booleano.**|TRUESe e solo se è presente un nodo nel set di nodi in modo che quando viene convertito **in booleano** e quindi in **number**, il confronto con il **valore booleano** convertito in **number** è TRUE.|TRUESe e solo se è presente un nodo nel set di nodi in modo che quando viene convertito **in booleano**, il confronto con il **valore booleano** è TRUE.|  
|Nessuno è un set di nodi.|Convertire entrambi gli operandi in **numeri** e quindi confrontare.|Convertire entrambi gli operandi in un tipo comune e quindi eseguire il confronto. Converti **in booleano** se uno dei due è **booleano**, **num** se uno dei due è **number**; in caso contrario, convertire in **stringa**.|  
  
> [!NOTE]  
>  Poiché gli operatori relazionali XPath convertono sempre i relativi operandi in **number**, i confronti **tra stringhe** non sono possibili. Per includere confronti di date, SQL Server 2000 offre questa variazione alla specifica XPath: quando un operatore relazionale confronta una **stringa** con una **stringa,** un set di nodi a una **stringa**o un set di nodi con valori di stringa su un set di nodi con valori di stringa, viene eseguito un confronto **tra stringhe** (non un confronto **numerico).**  
  
## <a name="node-set-conversions"></a>Conversioni dei set di nodi  
 Le conversioni dei set di nodi non sono sempre intuitive. Un set di nodi viene convertito in una **stringa** prendendo il valore stringa solo del primo nodo nel set. Un set di nodi viene convertito in **numero** convertendolo in **stringa**e quindi convertendo **la stringa** in **numero**. Un set di nodi viene convertito **in booleano** verificandone l'esistenza.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non esegue la selezione della posizione nei set di nodi: la query XPath `Customer[3]`, ad esempio, indica il terzo cliente. Questo tipo di selezione della posizione non è supportato in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Pertanto, le conversioni da nodo impostato su**stringa** o da nodo impostato a**numero** come descritto dalla specifica XPath non vengono implementate. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilizza le semantiche "any" dove la specifica XPath specifica la semantica "first". Ad esempio, in base alla specifica W3C `Order[OrderDetail/@UnitPrice > 10.0]` XPath, la query XPath seleziona gli ordini con il primo **OrderDetail** con un **UnitPrice** maggiore di 10.0. In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], questa query XPath seleziona gli ordini con qualsiasi **OrderDetail** con un **UnitPrice** maggiore di 10.0.  
  
 La conversione in **booleano** genera un test di esistenza; pertanto, la `Products[@Discontinued=true()]` query XPath è equivalente all'espressione SQL "Products.Discontinued is not null", non all'espressione SQL "Products.Discontinued s 1". Per rendere la query equivalente a quest'ultima espressione SQL, convertire innanzitutto il set di nodi in un tipo non**booleano,** ad esempio **numero**. Ad esempio: `Products[number(@Discontinued) = true()]`.  
  
 Poiché la maggior parte degli operatori viene definita come TRUE se gli operatori sono TRUE per tutti i nodi nel set di nodi o per uno di essi, queste operazioni restituiscono sempre FALSE se il set di nodi è vuoto. In questo modo, se A è vuoto, sia `A = B` sia `A != B` sono FALSE e `not(A=B)` e `not(A!=B)` sono TRUE.  
  
 In genere, un attributo o un elemento che esegue il mapping a una colonna esiste se il valore di tale colonna nel database non è **null.** Sono presenti elementi di cui è stato eseguito il mapping a righe se è presente uno qualunque dei figli.  
  
> [!NOTE]  
>  Gli elementi annotati con **is-constant** esistono sempre. Di conseguenza, i predicati XPath non possono essere utilizzati su elementi **is-constant.**  
  
 Quando un set di nodi viene convertito in **stringa** o **numero**, il relativo tipo XDR (se presente) viene controllato nello schema annotato e tale tipo viene utilizzato per determinare la conversione necessaria.  
  
## <a name="mapping-xdr-data-types-to-xpath-data-types"></a>Mapping di tipi di dati XDR a tipi di dati XPath  
 Il tipo di dati XPath di un nodo è derivato dal tipo di dati XDR nello schema, come illustrato nella tabella seguente (il nodo **EmployeeID** viene utilizzato a scopo illustrativo).  
  
|Tipo di dati XDR|Equivalente<br /><br /> Tipo di dati XPath|Conversione SQL Server utilizzata|  
|-------------------|------------------------------------|--------------------------------|  
|Nonebin.base64bin.hex|N/D|NoneEmployeeID|  
|boolean|boolean|CONVERT(bit, EmployeeID)|  
|number, int, float, i1, i2, i4, i8,r4, r8ui1, ui2, ui4, ui8|d'acquisto|CONVERT(float(53), EmployeeID)|  
|id, idref, idrefsentity, entities, enumerationnotation, nmtoken, nmtokens, chardate, Timedate, Time.tz, string, uri, uuid|string|CONVERT(nvarchar(4000), EmployeeID, 126)|  
|fixed14.4|N/D (in XPath non è disponibile alcun tipo di dati equivalente al tipo di dati XDR fixed14.4).|CONVERT(money, EmployeeID)|  
|Data|string|LEFT(CONVERT(nvarchar(4000), EmployeeID, 126), 10)|  
|time<br /><br /> time.tz|string|SUBSTRING(CONVERT(nvarchar(4000), EmployeeID, 126), 1 + CHARINDEX(N'T', CONVERT(nvarchar(4000), EmployeeID, 126)), 24)|  
  
 Le conversioni di data e ora sono progettate per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]funzionare se il valore viene archiviato nel database utilizzando il tipo di dati **datetime** o una **stringa**. Si [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]noti che il tipo di dati **datetime** non utilizza il fuso **orario** e ha una precisione inferiore rispetto al tipo di dati **ora** XML. Per includere il tipo di dati del fuso [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **orario** o una precisione aggiuntiva, archiviare i dati utilizzando un tipo **stringa.**  
  
 Quando un nodo viene convertito dal relativo tipo di dati XDR al tipo di dati XPath, è talvolta necessaria un'ulteriore conversione (da un tipo di dati XPath a un altro tipo di dati XPath). Si consideri, ad esempio, la query XPath seguente:  
  
```  
(@m + 3) = 4  
```  
  
 Se @m è del tipo di dati XDR **fixed14.4,** la conversione dal tipo di dati XDR al tipo di dati XPath viene eseguita utilizzando:  
  
```  
CONVERT(money, m)  
```  
  
 In questa conversione, il nodo `m` viene convertito da **fixed14.4** a **money**. Per aggiungere il valore 3, tuttavia, è necessaria un'ulteriore conversione:  
  
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
||X non è noto|X è **stringa**|X è **il numero**|X è **booleano**|  
|string(X)|CONVERT (nvarchar(4000), X, 126)|-|CONVERT (nvarchar(4000), X, 126)|CASE WHEN X THEN N'true' ELSE N'false' END|  
|number(X)|CONVERT (float(53), X)|CONVERT (float(53), X)|-|CASE WHEN X THEN 1 ELSE 0 END|  
|boolean(X)|-|LEN(X) > 0|X != 0|-|  
  
## <a name="examples"></a>Esempi  
  
### <a name="a-convert-a-data-type-in-an-xpath-query"></a>R. Convertire un tipo di dati in una query XPath  
 Nella query XPath seguente specificata rispetto a uno schema XSD con annotazioni, la query seleziona tutti i nodi **Employee** con il valore dell'attributo **EmployeeID** E-1, dove "E-" è il prefisso specificato utilizzando l'annotazione **sql:id-prefix.**  
  
 `Employee[@EmployeeID="E-1"]`  
  
 Il predicato nella query equivale all'espressione SQL:  
  
 `N'E-' + CONVERT(nvarchar(4000), Employees.EmployeeID, 126) = N'E-1'`  
  
 Poiché **EmployeeID** è uno dei valori del tipo di dati **id** (**idref**, **idrefs**, **nmtoken** **, nmtokens**e così via) nello schema XSD, **EmployeeID** viene convertito **nel** tipo di dati XPath stringa utilizzando le regole di conversione descritte in precedenza.  
  
 `CONVERT(nvarchar(4000), Employees.EmployeeID, 126)`  
  
 Il prefisso "E-" viene aggiunto alla stringa, e il risultato viene quindi confrontato con `N'E-1'`.  
  
### <a name="b-perform-several-data-type-conversions-in-an-xpath-query"></a>B. Eseguire diverse conversioni dei tipi di dati in una query XPath  
 Considerare la seguente query XPath specificata su uno schema XSD con annotazioni: `OrderDetail[@UnitPrice * @OrderQty > 98]`  
  
 Questa query XPath restituisce tutti gli `@UnitPrice * @OrderQty > 98` ** \<** elementi OrderDetail>che soddisfano il predicato. Se il UnitPrice è annotato con un tipo di dati fixed14.4 nello schema annotato, questo predicato è equivalente all'espressione SQL:If the **UnitPrice** is annotated with a **fixed14.4** data type in the annotated schema, this predicate is equivalent to the SQL expression:  
  
 `CONVERT(float(53), CONVERT(money, OrderDetail.UnitPrice)) * CONVERT(float(53), OrderDetail.OrderQty) > CONVERT(float(53), 98)`  
  
 Nel convertire i valori nella query XPath, la prima operazione converte il tipo di dati XDR nel tipo di dati XPath. Poiché il tipo di dati XSD di **UnitPrice** è **fisso14.4**, come descritto nella tabella precedente, si tratta della prima conversione utilizzata:  
  
```  
CONVERT(money, OrderDetail.UnitPrice))   
```  
  
 Poiché gli operatori aritmetici convertono i relativi operandi nel tipo di dati **numero** XPath, viene applicata la seconda conversione (da un tipo di dati XPath a un altro tipo di dati XPath) in cui il valore viene convertito in **float(53)** (**float(53)** è vicino al tipo di dati **numero** XPath):  
  
```  
CONVERT(float(53), CONVERT(money, OrderDetail.UnitPrice))   
```  
  
 Supponendo che l'attributo **OrderQty** non abbia un tipo di dati XSD, **OrderQty** viene convertito in un tipo di dati XPath **numerico** in una singola conversione:  
  
```  
CONVERT(float(53), OrderDetail.OrderQty)  
```  
  
 Analogamente, il valore 98 viene convertito nel tipo di dati **numero** XPath:  
  
```  
CONVERT(float(53), 98)  
```  
  
> [!NOTE]  
>  Se il tipo di dati XSD utilizzato nello schema non è compatibile con il tipo di dati di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sottostante nel database o se viene eseguita una conversione del tipo di dati XPath non consentita, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] può restituire un errore. Ad esempio, se l'attributo **EmployeeID** è annotato con `Employee[@EmployeeID=1]` annotazione **id-prefix,** l'XPath genera un errore, perché **EmployeeID** ha l'annotazione **id-prefix** e non può essere convertito in **number**.  
  
  
