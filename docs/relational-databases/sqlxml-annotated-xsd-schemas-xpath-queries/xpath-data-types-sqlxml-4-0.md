---
title: Tipi di dati XPath (SQLXML)
description: Informazioni sui tipi di dati XPath in SQLXML 4,0 e sul relativo confronto con Microsoft SQL Server e i tipi di dati XML Schema (XSD).
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
ms.openlocfilehash: 17ad196110a68a83618e5048f53bfa84fb7e0f51
ms.sourcegitcommit: 6593b3b6365283bb76c31102743cdccc175622fe
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/02/2020
ms.locfileid: "84306020"
---
# <a name="xpath-data-types-sqlxml-40"></a>Tipi di dati XPath (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], XPath e XML Schema (XSD) hanno tipi di dati molto diversi. XPath, ad esempio, non include tipi di dati integer o di data, mentre [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e XSD ne includono diversi. XSD utilizza una precisione in nanosecondi per i valori di ora, mentre [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilizza al massimo una precisione di 1/300 secondi. Di conseguenza, il mapping di un tipo di dati a un altro non è sempre possibile. Per ulteriori informazioni sul mapping [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dei tipi di dati ai tipi di dati XSD, vedere [coercizione del tipo di dati e l'annotazione sql: DataType &#40;SQLXML 4,0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/data-type-coercions-and-the-sql-datatype-annotation-sqlxml-4-0.md).  
  
 XPath è costituito da tre tipi di dati: **String**, **Number**e **Boolean**. Il tipo di dati **Number** è sempre un valore a virgola mobile a precisione doppia IEEE 754. Il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo di dati **float (53)** corrisponde al **numero**XPath più vicino. Tuttavia, **float (53)** non è esattamente IEEE 754. Ad esempio, non viene utilizzato né un valore diverso da un numero (NaN, Not-a-Number) né un valore infinito. Se si tenta di convertire una stringa non numerica in un **numero** e si tenta di dividere per zero, viene restituito un errore.  
  
## <a name="xpath-conversions"></a>Conversioni XPath  
 Quando si utilizza una query XPath, ad esempio `OrderDetail[@UnitPrice > "10.0"]`, le conversioni dei tipi di dati implicite ed esplicite possono modificare impercettibilmente il significato della query. È pertanto importante comprendere le modalità di implementazione dei tipi di dati XPath. Le specifiche del linguaggio XPath, XML Path Language (XPath) versione 1,0 W3C proposed Recommendation 8 ottobre 1999, sono reperibili nel sito Web W3C all'indirizzo http://www.w3.org/TR/1999/PR-xpath-19991008.html .  
  
 Gli operatori XPath sono suddivisi in quattro categorie:  
  
-   Operatori booleani (and, or)  
  
-   Operatori relazionali ( \<, > , \<=, > =)  
  
-   Operatori di uguaglianza (=, !=)  
  
-   Operatori aritmetici: (+, -, *, div, mod)  
  
 Ogni categoria di operatore converte in modo diverso gli operandi. Se necessario, gli operatori XPath convertono gli operandi in modo implicito. Gli operatori aritmetici convertono gli operandi in **numero**e restituiscono un valore numerico. Gli operatori booleani convertono gli operandi in un valore **booleano**e restituiscono un valore booleano. Gli operatori relazionali e gli operatori di uguaglianza restituiscono un valore booleano, ma utilizzano regole di conversione diverse a seconda dei tipi di dati originali degli operandi, come illustrato nella tabella seguente.  
  
|Operando|Operatore relazionale|Operatore di uguaglianza|  
|-------------|-------------------------|-----------------------|  
|Entrambi gli operandi sono set di nodi.|TRUE se e solo se è presente un nodo in un set e un nodo nel secondo set in modo tale che il confronto dei valori **stringa** sia true.|Idem|  
|Uno è un set di nodi, l'altro una **stringa**.|TRUE se e solo se è presente un nodo nel set di nodi in modo tale che, se convertito in **numero**, il confronto con la **stringa** convertita in **numero** è true.|TRUE se e solo se è presente un nodo nel set di nodi in modo tale che, se convertito in **stringa**, il confronto con la **stringa** è true.|  
|Uno è un set di nodi, l'altro un **numero**.|TRUE se e solo se è presente un nodo nel set di nodi in modo tale che, se convertito in **numero**, il confronto con il **numero** è true.|Idem|  
|Uno è un set di nodi, l'altro un **valore booleano**.|TRUE se e solo se è presente un nodo nel set di nodi in modo tale che, se convertito in **valore booleano** e quindi in **numero**, il confronto con il **valore booleano** convertito in **numero** è true.|TRUE se e solo se è presente un nodo nel set di nodi in modo tale che, se convertito in un **valore booleano**, il confronto con il **valore booleano** è true.|  
|Nessuno è un set di nodi.|Convertire entrambi gli operandi in **numero** , quindi confrontare.|Convertire entrambi gli operandi in un tipo comune e quindi eseguire il confronto. Converte in **Boolean** se una delle due è **booleana**, **numero** se è un **numero**; in caso contrario, convertire in **stringa**.|  
  
> [!NOTE]  
>  Poiché gli operatori relazionali XPath convertono sempre gli operandi in **numero**, i confronti tra **stringhe** non sono possibili. Per includere i confronti di data, SQL Server 2000 offre questa variazione alla specifica XPath: quando un operatore relazionale confronta una **stringa** con una **stringa**, un set di nodi a una **stringa**o un set di nodi con valori di stringa in un set di nodi con valori di stringa, viene eseguito un confronto di **stringhe** (non un confronto **numerico** ).  
  
## <a name="node-set-conversions"></a>Conversioni dei set di nodi  
 Le conversioni dei set di nodi non sono sempre intuitive. Un set di nodi viene convertito in una **stringa** accettando il valore stringa solo del primo nodo nel set. Un set di nodi viene convertito in **numero** eseguendo la conversione in **stringa**e quindi convertendo una **stringa** in un **numero**. Un set di nodi viene convertito in un **valore booleano** verificando la relativa esistenza.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non esegue la selezione della posizione nei set di nodi: la query XPath `Customer[3]`, ad esempio, indica il terzo cliente. Questo tipo di selezione della posizione non è supportato in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Pertanto, le conversioni node-set-to-**String** o node-set-to-**Number** descritte dalla specifica XPath non sono implementate. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilizza le semantiche "any" dove la specifica XPath specifica la semantica "first". Ad esempio, in base alla specifica XPath W3C, la query XPath `Order[OrderDetail/@UnitPrice > 10.0]` Seleziona gli ordini con il primo **OrderDetail** con un **PrezzoUnitario** maggiore di 10,0. In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] questa query XPath seleziona gli ordini con qualsiasi **OrderDetail** con un **PrezzoUnitario** maggiore di 10,0.  
  
 La conversione in un **valore booleano** genera un test di esistenza; Pertanto, la query XPath `Products[@Discontinued=true()]` equivale all'espressione SQL "Products. Discontinued is not null", non all'espressione SQL "Products. Discontinued = 1". Per rendere la query equivalente all'ultima espressione SQL, convertire innanzitutto il set di nodi in un tipo non**booleano** , ad esempio **Number**. Ad esempio, `Products[number(@Discontinued) = true()]`  
  
 Poiché la maggior parte degli operatori viene definita come TRUE se gli operatori sono TRUE per tutti i nodi nel set di nodi o per uno di essi, queste operazioni restituiscono sempre FALSE se il set di nodi è vuoto. In questo modo, se A è vuoto, sia `A = B` sia `A != B` sono FALSE e `not(A=B)` e `not(A!=B)` sono TRUE.  
  
 In genere, un attributo o un elemento che esegue il mapping a una colonna esiste se il valore della colonna nel database non è **null**. Sono presenti elementi di cui è stato eseguito il mapping a righe se è presente uno qualunque dei figli.  
  
> [!NOTE]  
>  Gli elementi annotati con **is-Constant sono** sempre presenti. Di conseguenza, non è possibile utilizzare predicati XPath in elementi **is-constant** .  
  
 Quando un set di nodi viene convertito in una **stringa** o in un **numero**, il relativo tipo XDR (se presente) viene controllato nello schema con annotazioni e tale tipo viene utilizzato per determinare la conversione richiesta.  
  
## <a name="mapping-xdr-data-types-to-xpath-data-types"></a>Mapping di tipi di dati XDR a tipi di dati XPath  
 Il tipo di dati XPath di un nodo viene derivato dal tipo di dati XDR nello schema, come illustrato nella tabella seguente (il nodo **EmployeeID** viene utilizzato a scopo illustrativo).  
  
|Tipo di dati XDR|Equivalente<br /><br /> Tipo di dati XPath|Conversione SQL Server utilizzata|  
|-------------------|------------------------------------|--------------------------------|  
|Nonebin.base64bin.hex|N/D|NoneEmployeeID|  
|boolean|boolean|CONVERT(bit, EmployeeID)|  
|number, int, float, i1, i2, i4, i8,r4, r8ui1, ui2, ui4, ui8|d'acquisto|CONVERT(float(53), EmployeeID)|  
|id, idref, idrefsentity, entities, enumerationnotation, nmtoken, nmtokens, chardate, Timedate, Time.tz, string, uri, uuid|string|CONVERT(nvarchar(4000), EmployeeID, 126)|  
|fixed14.4|N/D (in XPath non è disponibile alcun tipo di dati equivalente al tipo di dati XDR fixed14.4).|CONVERT(money, EmployeeID)|  
|Data|string|LEFT(CONVERT(nvarchar(4000), EmployeeID, 126), 10)|  
|time<br /><br /> time.tz|string|SUBSTRING(CONVERT(nvarchar(4000), EmployeeID, 126), 1 + CHARINDEX(N'T', CONVERT(nvarchar(4000), EmployeeID, 126)), 24)|  
  
 Le conversioni di data e ora sono progettate per funzionare se il valore viene archiviato nel database utilizzando il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo di dati **DateTime** o una **stringa**. Si noti che il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo di dati **DateTime** non utilizza il **fuso orario** e ha una precisione inferiore rispetto al tipo di dati **Time** XML. Per includere il tipo di dati **TimeZone** o la precisione aggiuntiva, archiviare i dati in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando un tipo **stringa** .  
  
 Quando un nodo viene convertito dal relativo tipo di dati XDR al tipo di dati XPath, è talvolta necessaria un'ulteriore conversione (da un tipo di dati XPath a un altro tipo di dati XPath). Si consideri, ad esempio, la query XPath seguente:  
  
```  
(@m + 3) = 4  
```  
  
 Se @m è del tipo di dati XDR **fixed 14.4** , la conversione dal tipo di dati XDR al tipo di dati XPath viene eseguita utilizzando:  
  
```  
CONVERT(money, m)  
```  
  
 In questa conversione, il nodo `m` viene convertito da un **14.4 fisso** a un **denaro**. Per aggiungere il valore 3, tuttavia, è necessaria un'ulteriore conversione:  
  
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
||X non è noto|X è una **stringa**|X è un **numero**|X è un **valore booleano**|  
|string(X)|CONVERT (nvarchar(4000), X, 126)|-|CONVERT (nvarchar(4000), X, 126)|CASE WHEN X THEN N'true' ELSE N'false' END|  
|number(X)|CONVERT (float(53), X)|CONVERT (float(53), X)|-|CASE WHEN X THEN 1 ELSE 0 END|  
|boolean(X)|-|LEN (X) > 0|X != 0|-|  
  
## <a name="examples"></a>Esempi  
  
### <a name="a-convert-a-data-type-in-an-xpath-query"></a>R. Convertire un tipo di dati in una query XPath  
 Nella query XPath seguente specificata su uno schema XSD con annotazioni, la query seleziona tutti i nodi **Employee** con il valore dell'attributo **EmployeeID** di E-1, dove "E-" è il prefisso specificato utilizzando l'annotazione **SQL: id-prefix** .  
  
 `Employee[@EmployeeID="E-1"]`  
  
 Il predicato nella query equivale all'espressione SQL:  
  
 `N'E-' + CONVERT(nvarchar(4000), Employees.EmployeeID, 126) = N'E-1'`  
  
 Poiché **EmployeeID** è uno dei valori del tipo di dati **ID** (**IDREF**, **IDREFS**, **NMTOKEN**, **NMTOKENS**e così via) nello schema XSD, **EmployeeID** viene convertito nel tipo di dati XPath **stringa** utilizzando le regole di conversione descritte in precedenza.  
  
 `CONVERT(nvarchar(4000), Employees.EmployeeID, 126)`  
  
 Il prefisso "E-" viene aggiunto alla stringa, e il risultato viene quindi confrontato con `N'E-1'`.  
  
### <a name="b-perform-several-data-type-conversions-in-an-xpath-query"></a>B. Eseguire diverse conversioni dei tipi di dati in una query XPath  
 Considerare la seguente query XPath specificata su uno schema XSD con annotazioni: `OrderDetail[@UnitPrice * @OrderQty > 98]`  
  
 Questa query XPath restituisce tutti gli **\<OrderDetail>** elementi che soddisfano il predicato `@UnitPrice * @OrderQty > 98` . Se **PrezzoUnitario** viene annotato con un tipo di dati **14.4 fisso** nello schema con annotazioni, questo predicato è equivalente all'espressione SQL:  
  
 `CONVERT(float(53), CONVERT(money, OrderDetail.UnitPrice)) * CONVERT(float(53), OrderDetail.OrderQty) > CONVERT(float(53), 98)`  
  
 Nel convertire i valori nella query XPath, la prima operazione converte il tipo di dati XDR nel tipo di dati XPath. Poiché il tipo di dati XSD di **PrezzoUnitario** è **fixed 14.4**, come descritto nella tabella precedente, si tratta della prima conversione utilizzata:  
  
```  
CONVERT(money, OrderDetail.UnitPrice))   
```  
  
 Poiché gli operatori aritmetici convertono gli operandi nel tipo di dati **Number** XPath, viene applicata la seconda conversione (da un tipo di dati XPath a un altro tipo di dati XPath) in cui il valore viene convertito in **float (53)** (**float (53)** si avvicina al tipo di dati **Number** XPath):  
  
```  
CONVERT(float(53), CONVERT(money, OrderDetail.UnitPrice))   
```  
  
 Supponendo che l'attributo **OrderQty** non disponga di un tipo di dati XSD, **OrderQty** viene convertito in un tipo di dati **Number** XPath in un'unica conversione:  
  
```  
CONVERT(float(53), OrderDetail.OrderQty)  
```  
  
 Analogamente, il valore 98 viene convertito nel tipo di dati **Number** XPath:  
  
```  
CONVERT(float(53), 98)  
```  
  
> [!NOTE]  
>  Se il tipo di dati XSD utilizzato nello schema non è compatibile con il tipo di dati di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sottostante nel database o se viene eseguita una conversione del tipo di dati XPath non consentita, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] può restituire un errore. Se, ad esempio, l'attributo **EmployeeID** viene annotato con l'annotazione **id-prefix** , XPath `Employee[@EmployeeID=1]` genera un errore, perché **EmployeeID** presenta l'annotazione **id-prefix** e non può essere convertito in **Number**.  
  
  
