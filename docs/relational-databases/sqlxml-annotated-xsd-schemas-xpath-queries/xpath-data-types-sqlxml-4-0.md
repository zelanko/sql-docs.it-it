---
title: Tipi di dati XPath (SQLXML 4.0) | Documenti di Microsoft
ms.custom: ''
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
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 0c5cb588e96bcabad464339b7227ada3aef86221
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/11/2019
ms.locfileid: "56039922"
---
# <a name="xpath-data-types-sqlxml-40"></a>Tipi di dati XPath (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], XPath e gli elementi XML Schema (XSD) utilizzano tipi di dati molto diversi. XPath, ad esempio, non include tipi di dati integer o di data, mentre [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e XSD ne includono diversi. XSD utilizza una precisione in nanosecondi per i valori di ora, mentre [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilizza al massimo una precisione di 1/300 secondi. Di conseguenza, il mapping di un tipo di dati a un altro non è sempre possibile. Per ulteriori informazioni sul mapping [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] i tipi di dati ai tipi di dati XSD, vedere [coercizioni di tipi di dati e l'annotazione SQL: DataType &#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/data-type-coercions-and-the-sql-datatype-annotation-sqlxml-4-0.md).  
  
 XPath utilizza tre tipi di dati: **stringa**, **numero**, e **booleano**. Il **numero** tipo di dati è sempre una valore IEEE 754 a precisione doppia. Il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **float (53)** tipo di dati è il più vicino a XPath **numero**. Tuttavia **float (53)** è non esattamente IEEE 754. Ad esempio, non viene utilizzato né un valore diverso da un numero (NaN, Not-a-Number) né un valore infinito. Tenta di convertire una stringa in un valore numerico **numero** e tenta di dividere per zero restituiscono un errore.  
  
## <a name="xpath-conversions"></a>Conversioni XPath  
 Quando si utilizza una query XPath, ad esempio `OrderDetail[@UnitPrice > "10.0"]`, le conversioni dei tipi di dati implicite ed esplicite possono modificare impercettibilmente il significato della query. È pertanto importante comprendere le modalità di implementazione dei tipi di dati XPath. La specifica del linguaggio XPath, XML Path Language (XPath) version 1.0 W3C Proposed Recommendation 8 October 1999, visitare il sito Web W3C all'indirizzo http://www.w3.org/TR/1999/PR-xpath-19991008.html.  
  
 Gli operatori XPath sono suddivisi in quattro categorie:  
  
-   Operatori booleani (and, or)  
  
-   Operatori relazionali (\<, >, \<=, > =)  
  
-   Operatori di uguaglianza (=, !=)  
  
-   Operatori aritmetici: (+, -, *, div, mod)  
  
 Ogni categoria di operatore converte in modo diverso gli operandi. Se necessario, gli operatori XPath convertono gli operandi in modo implicito. Operatori aritmetici convertono gli operandi in **numero**e il risultato in un valore numerico. Gli operatori booleani convertono gli operandi in **booleana**e restituiscono un valore booleano. Gli operatori relazionali e gli operatori di uguaglianza restituiscono un valore booleano, ma utilizzano regole di conversione diverse a seconda dei tipi di dati originali degli operandi, come illustrato nella tabella seguente.  
  
|Operando|Operatore relazionale|Operatore di uguaglianza|  
|-------------|-------------------------|-----------------------|  
|Entrambi gli operandi sono set di nodi.|TRUE se e solo se è presente un nodo in un set e un nodo nel secondo set in modo tale che il confronto dei loro **stringa** valori è TRUE.|Idem|  
|Uno è un set di nodi, l'altro una **stringa**.|TRUE se e solo se è presente un nodo nel set di nodi in modo che quando convertito in **numero**, il confronto con la **stringa** convertito **numero** è TRUE.|TRUE se e solo se è presente un nodo nel set di nodi in modo che quando convertito in **stringa**, il confronto con la **stringa** è TRUE.|  
|Uno è un set di nodi, l'altro una **numero**.|TRUE se e solo se è presente un nodo nel set di nodi in modo che quando convertito in **numero**, il confronto con la **numero** è TRUE.|Idem|  
|Uno è un set di nodi, l'altro una **booleana**.|TRUE se e solo se è presente un nodo nel set di nodi in modo che quando convertito in **booleana** e quindi a **numero**, il confronto con il **booleano** convertito in **numero** è TRUE.|TRUE se e solo se è presente un nodo nel set di nodi in modo che quando convertito in **booleana**, il confronto con la **booleano** è TRUE.|  
|Nessuno è un set di nodi.|Convertire entrambi gli operandi al **numero** e quindi eseguire il confronto.|Convertire entrambi gli operandi in un tipo comune e quindi eseguire il confronto. Convertire **booleana** se si verifica una **booleano**, **numero** se si verifica una **numero**; in caso contrario, convertire in **stringa**.|  
  
> [!NOTE]  
>  Poiché gli operatori relazionali XPath convertono sempre gli operandi in **numero**, **stringa** confronti non sono possibili. Per includere confronti relativi alla data, SQL Server 2000 è disponibile una variazione alla specifica XPath: Quando un operatore relazionale Confronta un **stringa** a un **stringa**, un set di nodi un **stringa**, un con valori di stringa di set di nodi in un stringa con valori di set di nodi, o un  **stringa** confronto (non un **numero** confronto) viene eseguita.  
  
## <a name="node-set-conversions"></a>Conversioni dei set di nodi  
 Le conversioni dei set di nodi non sono sempre intuitive. Un set di nodi viene convertito in un **stringa** prendendo il valore stringa del solo il primo nodo nel set. Un set di nodi viene convertito in **numero** tramite la conversione a **stringa**e quindi riconvertendo **stringa** al **numero**. Un set di nodi viene convertito in **booleana** eseguendo il test di esistenza.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non esegue la selezione della posizione nei set di nodi: la query XPath `Customer[3]`, ad esempio, indica il terzo cliente. Questo tipo di selezione della posizione non è supportato in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Di conseguenza, il nodo-impostare-a-**stringa** o nodo-set-a-**numero** conversioni come descritto dalla specifica XPath non sono implementate. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilizza le semantiche "any" dove la specifica XPath specifica la semantica "first". Ad esempio, basato sulla specifica W3C XPath, la query XPath `Order[OrderDetail/@UnitPrice > 10.0]` seleziona gli ordini con il primo **OrderDetail** con un **UnitPrice** maggiore di 10.0. Nelle [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], la query XPath seguente seleziona gli ordini con qualsiasi **OrderDetail** con un **UnitPrice** maggiore di 10.0.  
  
 La conversione a **booleana** genera un esistenza test; pertanto, la query XPath `Products[@Discontinued=true()]` è equivalente all'espressione SQL "Products. Discontinued non is null", non all'espressione SQL "Products. Discontinued = 1". Per rendere la query è equivalente all'espressione SQL successiva, convertire innanzitutto il set di nodi in un non -**booleana** digitare, ad esempio **numero**. Ad esempio `Products[number(@Discontinued) = true()]`.  
  
 Poiché la maggior parte degli operatori viene definita come TRUE se gli operatori sono TRUE per tutti i nodi nel set di nodi o per uno di essi, queste operazioni restituiscono sempre FALSE se il set di nodi è vuoto. In questo modo, se A è vuoto, sia `A = B` sia `A != B` sono FALSE e `not(A=B)` e `not(A!=B)` sono TRUE.  
  
 In genere, esiste un attributo o elemento che esegue il mapping a una colonna se il valore della colonna nel database non è **null**. Sono presenti elementi di cui è stato eseguito il mapping a righe se è presente uno qualunque dei figli.  
  
> [!NOTE]  
>  Gli elementi annotati con **costante è** sempre presente. Di conseguenza, non è possibile usare i predicati XPath sul **costante è** elementi.  
  
 Quando un set di nodi viene convertito in **stringa** oppure **numero**, il tipo XDR (se presente) viene controllato nello schema con annotazioni e tale tipo viene usato per determinare la conversione necessaria.  
  
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
  
 Le conversioni di data e ora sono progettate per funzionare se il valore viene archiviato nel database utilizzando la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **datetime** tipo di dati o un' **stringa**. Si noti che il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **datetime** tipo di dati non utilizza **fuso orario** e applica una precisione minore rispetto a XML **ora** tipo di dati. Per includere il **fuso orario** tipo di dati o aggiungere ulteriore precisione, archiviare i dati nella [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilizzando una **stringa** tipo.  
  
 Quando un nodo viene convertito dal relativo tipo di dati XDR al tipo di dati XPath, è talvolta necessaria un'ulteriore conversione (da un tipo di dati XPath a un altro tipo di dati XPath). Si consideri, ad esempio, la query XPath seguente:  
  
```  
(@m + 3) = 4  
```  
  
 Se @m è il **fixed14.4** tipo di dati XDR, la conversione dal tipo di dati XDR al tipo di dati viene eseguito con XPath:  
  
```  
CONVERT(money, m)  
```  
  
 In questa conversione, il nodo `m` viene convertito da **fixed14.4** al **denaro**. Per aggiungere il valore 3, tuttavia, è necessaria un'ulteriore conversione:  
  
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
||X non è noto|X è **stringa**|X è **numero**|X è **booleano**|  
|string(X)|CONVERT (nvarchar(4000), X, 126)|-|CONVERT (nvarchar(4000), X, 126)|CASE WHEN X THEN N'true' ELSE N'false' END|  
|number(X)|CONVERT (float(53), X)|CONVERT (float(53), X)|-|CASE WHEN X THEN 1 ELSE 0 END|  
|boolean(X)|-|LEN(X) > 0|X != 0|-|  
  
## <a name="examples"></a>Esempi  
  
### <a name="a-convert-a-data-type-in-an-xpath-query"></a>A. Convertire un tipo di dati in una query XPath  
 Nella query XPath seguente specificata su uno schema XSD con annotazione, la query Seleziona tutti i **dipendente** nodi con il **EmployeeID** attributo valore 1, dove "E-" è il prefisso specificato utilizzando il **SQL: ID-prefisso** annotazione.  
  
 `Employee[@EmployeeID="E-1"]`  
  
 Il predicato nella query equivale all'espressione SQL:  
  
 `N'E-' + CONVERT(nvarchar(4000), Employees.EmployeeID, 126) = N'E-1'`  
  
 Poiché **EmployeeID** è uno della **id** (**idref**, **idrefs**, **nmtoken**,  **NMTOKENS**e così via) i valori al tipo di dati dello schema XSD, **EmployeeID** viene convertito nel **stringa** tipo di dati XPath utilizzando le regole di conversione descritte in precedenza.  
  
 `CONVERT(nvarchar(4000), Employees.EmployeeID, 126)`  
  
 Il prefisso "E-" viene aggiunto alla stringa, e il risultato viene quindi confrontato con `N'E-1'`.  
  
### <a name="b-perform-several-data-type-conversions-in-an-xpath-query"></a>b. Eseguire diverse conversioni dei tipi di dati in una query XPath  
 Considerare la seguente query XPath specificata su uno schema XSD con annotazioni: `OrderDetail[@UnitPrice * @OrderQty > 98]`  
  
 Questa query XPath restituisce tutti i  **\<OrderDetail >** gli elementi che soddisfano il predicato `@UnitPrice * @OrderQty > 98`. Se il **UnitPrice** annotato con un **fixed14.4** tipo di dati nello schema con annotazione, questo predicato è equivalente all'espressione SQL:  
  
 `CONVERT(float(53), CONVERT(money, OrderDetail.UnitPrice)) * CONVERT(float(53), OrderDetail.OrderQty) > CONVERT(float(53), 98)`  
  
 Nel convertire i valori nella query XPath, la prima operazione converte il tipo di dati XDR nel tipo di dati XPath. Poiché il tipo di dati XSD del **UnitPrice** viene **fixed14.4**, come descritto nella tabella precedente, si tratta della prima conversione utilizzata:  
  
```  
CONVERT(money, OrderDetail.UnitPrice))   
```  
  
 Poiché gli operatori aritmetici convertono gli operandi per la **numero** tipo di dati XPath, la seconda conversione (da un tipo di dati XPath in un altro tipo di dati XPath) viene applicata in cui il valore viene convertito in **float (53)**  (**float (53)** sta per l'espressione XPath **numero** tipo di dati):  
  
```  
CONVERT(float(53), CONVERT(money, OrderDetail.UnitPrice))   
```  
  
 Supponendo che il **OrderQty** attributo non dispone di alcun tipo di dati XSD **OrderQty** viene convertito in un **numero** tipo di dati XPath in una singola conversione:  
  
```  
CONVERT(float(53), OrderDetail.OrderQty)  
```  
  
 Analogamente, il valore 98 viene convertito nel **numero** tipo di dati XPath:  
  
```  
CONVERT(float(53), 98)  
```  
  
> [!NOTE]  
>  Se il tipo di dati XSD utilizzato nello schema non è compatibile con il tipo di dati di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sottostante nel database o se viene eseguita una conversione del tipo di dati XPath non consentita, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] può restituire un errore. Ad esempio, se il **EmployeeID** attributo viene annotata con **id-prefix** annotazione, l'espressione XPath `Employee[@EmployeeID=1]` genera un errore, perché **EmployeeID** è il **id-prefix** annotazione e non può essere convertito in **numero**.  
  
  
