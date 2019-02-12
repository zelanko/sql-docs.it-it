---
title: Metodo nodes() (tipo di dati xml) | Microsoft Docs
ms.custom: ''
ms.date: 07/26/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- nodes() method
- nodes method
ms.assetid: 7267fe1b-2e34-4213-8bbf-1c953822446c
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 58a2a76cd79f7dded8fca3ded72dcaeaf4572482
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/11/2019
ms.locfileid: "56034152"
---
# <a name="nodes-method-xml-data-type"></a>Metodo nodes() (tipo di dati xml)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  È possibile usare il metodo **nodes()** per suddividere un'istanza del tipo di dati **xml** in un insieme di dati relazionali. Tale metodo consente di identificare i nodi sui quali verrà eseguito il mapping a una nuova riga.  
  
 Per ogni istanza del tipo di dati **xml** esiste un nodo di contesto fornito implicitamente. Nel caso di un'istanza XML archiviata in una colonna o variabile, si tratta del nodo del documento, che costituisce il nodo implicito di livello più alto per ogni istanza del tipo di dati **xml**.  
  
 Il metodo **nodes()** restituisce un set di righe che contiene copie logiche delle istanze XML originali. In tali copie logiche il nodo di contesto di ogni istanza di riga viene impostato su uno dei nodi identificati tramite l'espressione della query, di modo che le query successive possano eseguire spostamenti relativi rispetto ai nodi di contesto.  
  
 Dal set di righe è possibile recuperare più valori. È ad esempio possibile applicare il metodo **value()** al set di righe restituito dal metodo **nodes()** e recuperare più valori dall'istanza XML originale. Quando viene applicato a un'istanza XML, il metodo **value()** restituisce un solo valore.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
nodes (XQuery) as Table(Column)  
```  
  
## <a name="arguments"></a>Argomenti  
 *XQuery*  
 Valore letterale stringa costituito da un'espressione XQuery. Se l'espressione della query costruisce nodi, questi ultimi verranno esposti nel set di righe risultante. Se l'espressione della query restituisce una sequenza vuota, il set di righe sarà vuoto. Se l'espressione della query restituisce staticamente una sequenza che contiene valori atomici, anziché nodi, verrà generato un errore statico.  
  
 *Table*(*Column*)  
 Nome della tabella e della colonna per il set di righe risultante.  
  
## <a name="remarks"></a>Remarks  
 Si consideri ad esempio la tabella seguente:  
  
```  
T (ProductModelID int, Instructions xml)  
```  
  
 In tale tabella è archiviato il seguente documento di istruzioni per la produzione, di cui è illustrato solo un frammento. Si noti che nel documento sono indicati tre centri di produzione.  
  
```  
<root>  
  <Location LocationID="10"...>  
     <step>...</step>  
     <step>...</step>  
      ...  
  </Location>  
  <Location LocationID="20" ...>  
       ...  
  </Location>  
  <Location LocationID="30" ...>  
       ...  
  </Location>  
</root>  
```  
  
 Una chiamata al metodo `nodes()` con l'espressione di query `/root/Location` restituirebbe un set di righe con tre righe, ognuna contenente una copia logica del documento XML originale e con l'elemento di contesto impostato su uno dei nodi `<Location>`:  
  
```  
Product  
ModelID      Instructions  
----------------------------------  
1       <root>  
             <Location LocationID="20" ... />  
             <Location LocationID="30" .../></root>  
1      <root><Location LocationID="10" ... />  
  
             <Location LocationID="30" .../></root>  
1      <root><Location LocationID="10" ... />  
             <Location LocationID="20" ... />  
             </root>  
```  
  
 Per eseguire query su tale set di righe, è possibile usare i metodi con tipo di dati **xml**. La query seguente estrae il sottoalbero dell'elemento di contesto per ogni riga generata:  
  
```  
SELECT T2.Loc.query('.')  
FROM   T  
CROSS APPLY Instructions.nodes('/root/Location') as T2(Loc)   
```  
  
 Risultato:  
  
```  
ProductModelID  Instructions  
----------------------------------  
1        <Location LocationID="10" ... />  
1        <Location LocationID="20" ... />  
1        <Location LocationID="30" .../>  
```  
  
 Nel set di righe restituito sono state mantenute le informazioni sul tipo. È possibile applicare metodi con tipo di dati **xml**, ad esempio **query()**, **value()**, **exist()** e **nodes()** al risultato di un metodo **nodes()**. Non è tuttavia possibile applicare il metodo **modify()** per modificare l'istanza XML.  
  
 Inoltre, il nodo di contesto nel set di righe non può essere materializzato, ovvero non può essere utilizzato in un'istruzione SELECT. Può essere tuttavia utilizzato nelle istruzioni IS NULL e COUNT(*).  
  
 Gli scenari d'uso del metodo **nodes()** sono gli stessi dell'uso di [OPENXML &#40;Transact-SQL&#41;](../../t-sql/functions/openxml-transact-sql.md), che visualizza un'istanza XML come set di righe. Non è tuttavia possibile usare cursori quando si usa il metodo **nodes()** su una tabella che contiene più righe di documenti XML.  
  
 Si noti che, poiché il set di righe restituito dal metodo **nodes()** è senza nome, deve essere denominato in modo esplicito tramite alias.  
  
 La funzione **nodes()** non può essere applicata direttamente ai risultati di una funzione definita dall'utente. Per usare la funzione **nodes()** con il risultato di una funzione scalare definita dall'utente, è possibile assegnare il risultato della funzione definita dall'utente a una variabile o usare una tabella derivata per assegnare un alias di colonna al valore restituito dalla funzione definita dall'utente e quindi usare CROSS APPLY per eseguire la selezione dall'alias.  
  
 Nell'esempio seguente viene illustrato un modo per utilizzare `CROSS APPLY` per selezionare il risultato di una funzione definita dall'utente.  
  
```  
USE AdventureWorks;  
GO  
  
CREATE FUNCTION XTest()  
RETURNS xml  
AS  
BEGIN  
RETURN '<document/>';  
END;  
GO  
  
SELECT A2.B.query('.')  
FROM  
(SELECT dbo.XTest()) AS A1(X)   
CROSS APPLY X.nodes('.') A2(B);  
GO  
  
DROP FUNCTION XTest;  
GO  
```  
  
## <a name="examples"></a>Esempi  
  
### <a name="using-nodes-method-against-a-variable-of-xml-type"></a>Utilizzo del metodo nodes() su una variabile di tipo xml  
 Nell'esempio seguente viene utilizzato un documento XML con un elemento di livello principale <`Root`>e tre elementi figlio <`row`>. La query utilizza il metodo `nodes()` per impostare nodi di contesto separati, uno per ogni elemento<`row`>. Il metodo `nodes()` restituisce un set di righe con tre righe. Ogni riga contiene una copia logica dell'istanza XML originale e ogni nodo di contesto identifica un diverso elemento <`row`> nel documento originale.  
  
 La query restituisce quindi il nodo di contesto di ogni riga:  
  
```  
DECLARE @x xml   
SET @x='<Root>  
    <row id="1"><name>Larry</name><oflw>some text</oflw></row>  
    <row id="2"><name>moe</name></row>  
    <row id="3" />  
</Root>'  
SELECT T.c.query('.') AS result  
FROM   @x.nodes('/Root/row') T(c)  
GO  
```  
  
 Di seguito è riportato il risultato. In questo esempio il metodo della query restituisce l'elemento di contesto e il relativo contenuto:  
  
```  
<row id="1"><name>Larry</name><oflw>some text</oflw></row>  
<row id="2"><name>moe</name></row>  
<row id="3"/>  
```  
  
 Se si applica la funzione di accesso padre ai nodi di contesto, viene restituito l'elemento <`Root`> di ognuna delle tre righe:  
  
```  
SELECT T.c.query('..') AS result  
FROM   @x.nodes('/Root/row') T(c)  
go  
```  
  
 Risultato:  
  
```  
<Root>  
    <row id="1"><name>Larry</name><oflw>some text</oflw></row>  
    <row id="2"><name>moe</name></row>  
    <row id="3" />  
</Root>  
<Root>  
    <row id="1"><name>Larry</name><oflw>some text</oflw></row>  
    <row id="2"><name>moe</name></row>  
    <row id="3" />  
</Root>  
<Root>  
    <row id="1"><name>Larry</name><oflw>some text</oflw></row>  
    <row id="2"><name>moe</name></row>  
    <row id="3" />  
</Root>  
```  
  
### <a name="specifying-the-nodes-method-against-a-column-of-xml-type"></a>Utilizzo del metodo nodes() in una colonna di tipo xml  
 In questo esempio vengono usati documenti di istruzioni per la produzione di biciclette, archiviati nella colonna di tipo **xml** Instructions della tabella **ProductModel**.  
  
 Nell'esempio seguente il metodo `nodes()` viene eseguito sulla colonna `Instructions` di tipo **xml** della tabella `ProductModel`.  
  
 Il metodo `nodes()` imposta gli elementi <`Location`> come nodi di contesto specificando il percorso `/MI:root/MI:Location`. Il set di righe risultante include copie logiche del documento originale, una per ogni nodo <`Location`> del documento, con il nodo di contesto impostato sull'elemento <`Location`>. Il metodo `nodes()` restituisce pertanto un set di nodi di contesto <`Location`>.  
  
 Il metodo `query()` su questo set di righe richiede `self::node` e pertanto restituisce l'elemento `<Location>` di ogni riga.  
  
 In questo esempio la query imposta ogni elemento <`Location`> come nodo di contesto nel documento di istruzioni per la produzione di uno specifico modello di prodotto. È possibile utilizzare tali nodi di contesto per recuperare valori quali i seguenti:  
  
-   Trovare ID dei centri di produzione in ogni elemento <`Location`>  
  
-   Recuperare i passaggi di produzione (gli elementi figlio <`step`>) in ogni elemento <`Location`>  
  
 La query seguente restituisce l'elemento di contesto. Nel metodo `'.'` viene specificata la sintassi abbreviata per `self::node()`, ovvero `query()`.  
  
 Si noti quanto segue:  
  
-   Il metodo `nodes()` viene applicato alla colonna Instructions e restituisce il set di righe `T (C)`, il quale contiene copie logiche del documento originale di istruzioni per la produzione con `/root/Location` come elemento di contesto.  
  
-   CROSS APPLY applica `nodes()` a ogni riga nella colonna `Instructions` e restituisce solo le righe che producono un set di risultati.  
  
    ```  
    SELECT C.query('.') as result  
    FROM Production.ProductModel  
    CROSS APPLY Instructions.nodes('  
    declare namespace MI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
    /MI:root/MI:Location') as T(C)  
    WHERE ProductModelID=7  
    ```  
  
     Risultato parziale:  
  
    ```  
    <MI:Location LocationID="10"  ...>  
       <MI:step ... />  
          ...  
    </MI:Location>  
    <MI:Location LocationID="20"  ... >  
        <MI:step ... />  
          ...  
    </MI:Location>  
    ...  
    ```  
  
### <a name="applying-nodes-to-the-rowset-returned-by-another-nodes-method"></a>Applicazione del metodo nodes() al set di righe restituito da un altro metodo nodes()  
 Il codice seguente esegue una query sui documenti XML con le istruzioni per la produzione archiviati nella colonna `Instructions` della tabella `ProductModel`. La query restituisce un set di righe che contiene l'ID del modello di prodotto, i centri di produzione e i passaggi di produzione.  
  
 Si noti quanto segue:  
  
-   Il metodo `nodes()` viene applicato alla colonna `Instructions` e restituisce il set di righe `T1 (Locations)`, il quale contiene copie logiche del documento originale di istruzioni per la produzione con `/root/Location` come elemento di contesto.  
  
-   Il metodo `nodes()` viene applicato al set di righe `T1 (Locations)` e restituisce il set di righe `T2 (steps)`, il quale contiene copie logiche del documento originale di istruzioni per la produzione con `/root/Location/step` come elemento di contesto.  
  
```  
SELECT ProductModelID, Locations.value('./@LocationID','int') as LocID,  
steps.query('.') as Step         
FROM Production.ProductModel         
CROSS APPLY Instructions.nodes('         
declare namespace MI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";         
/MI:root/MI:Location') as T1(Locations)         
CROSS APPLY T1.Locations.nodes('         
declare namespace MI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";         
./MI:step ') as T2(steps)         
WHERE ProductModelID=7         
GO         
```  
  
 Risultato:  
  
```  
ProductModelID LocID Step         
----------------------------         
7      10   <step ... />         
7      10   <step ... />         
...         
7      20   <step ... />         
7      20   <step ... />         
7      20   <step ... />         
...         
```  
  
 Nella query il prefisso `MI` viene dichiarato due volte. In alternativa, è possibile utilizzare `WITH XMLNAMESPACES` per dichiarare il prefisso una volta sola e utilizzarlo nella query:  
  
```  
WITH XMLNAMESPACES (  
   'https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions'  AS MI)  
  
SELECT ProductModelID, Locations.value('./@LocationID','int') as LocID,  
steps.query('.') as Step         
FROM Production.ProductModel         
CROSS APPLY Instructions.nodes('         
/MI:root/MI:Location') as T1(Locations)         
CROSS APPLY T1.Locations.nodes('         
./MI:step ') as T2(steps)         
WHERE ProductModelID=7         
GO    
```  
  
## <a name="see-also"></a>Vedere anche  
 [Aggiungere spazi dei nomi alle query con WITH XMLNAMESPACES](../../relational-databases/xml/add-namespaces-to-queries-with-with-xmlnamespaces.md)   
 [Creare istanze di dati XML](../../relational-databases/xml/create-instances-of-xml-data.md)   
 [metodi con tipo di dati xml](../../t-sql/xml/xml-data-type-methods.md)  
  
  
