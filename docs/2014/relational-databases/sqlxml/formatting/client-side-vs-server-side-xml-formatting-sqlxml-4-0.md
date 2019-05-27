---
title: Lato client e Programma di formattazione XML sul lato server (SQLXML 4.0) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- NESTED mode
- FOR XML clause, formatting
- client-side XML formatting
- server-side XPath
- server-side XML formatting
- AUTO mode
- client-side XPath
ms.assetid: f807ab7a-c5f8-4e61-9b00-23aebfabc47e
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4eaa4667db1e8b6ed789e2adb90bc8d72c1b02e6
ms.sourcegitcommit: 45a9d7ffc99502c73f08cb937cbe9e89d9412397
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/22/2019
ms.locfileid: "66012345"
---
# <a name="client-side-vs-server-side-xml-formatting-sqlxml-40"></a>Lato client e Formattazione XML sul lato server (SQLXML 4.0)
  In questo argomento vengono descritte le differenze generali tra la formattazione XML sul lato client e quella sul lato server in SQLXML.  
  
## <a name="multiple-rowset-queries-not-supported-in-client-side-formatting"></a>Query su più set di righe non supportate nella formattazione sul lato client  
 Le query che generano più set di righe non sono supportate quando si utilizza la formattazione XML sul lato client. Supporre, ad esempio, di disporre di una directory virtuale nella quale è stata specificata la formattazione sul lato client. Considerare questo modello di esempio, che dispone di due istruzioni SELECT in una  **\<sql:query >** blocco:  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <sql:query>  
     SELECT FirstName FROM Person.Contact FOR XML Nested;   
     SELECT LastName FROM Person.Contact FOR XML Nested    
  </sql:query>  
</ROOT>  
```  
  
 È possibile eseguire questo modello nel codice dell'applicazione ma viene restituito un errore, poiché la formattazione XML sul lato client non supporta la formattazione di più set di righe. Se si specifica la query in due separare  **\<sql:query >** blocchi, si otterranno i risultati desiderati.  
  
## <a name="timestamp-maps-differently-in-client--vs-server-side-formatting"></a>timestamp mappe in modo diverso in Client-Visual Studio. Formattazione sul lato server  
 Nella formattazione XML sul lato server la colonna di database del tipo `timestamp` esegue il mapping al tipo XDR i8, quando viene specificata l'opzione XMLDATA nella query.  
  
 Nella formattazione XML sul lato client la colonna di database del tipo `timestamp` esegue il mapping al tipo XDR `uri` o `bin.base64`, a seconda che venga specificata l'opzione binary base64 nella query. Il `bin.base64` tipo XDR è utile se si usano le funzionalità di updategram e caricamento bulk, perché questo tipo viene convertito nel [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] `timestamp` tipo. In questo modo, l'operazione di inserimento, aggiornamento o eliminazione viene eseguita correttamente.  
  
## <a name="deep-variants-are-used-in-server-side-formatting"></a>Tipi VARIANT completi utilizzati nella formattazione sul lato server  
 Nella formattazione XML sul lato server vengono utilizzati i tipi VARIANT completi. Se si utilizza la formattazione XML sul lato client, le varianti vengono convertite in una stringa Unicode e i sottotipi di VARIANT non vengono utilizzati.  
  
## <a name="nested-mode-vs-auto-mode"></a>Modalità NESTED e Modalità AUTO  
 La modalità NESTED di FOR XML sul lato client è simile alla modalità AUTO di FOR XML sul lato server, con le eccezioni seguenti:  
  
### <a name="when-you-query-views-using-auto-mode-on-the-server-side-the-view-name-is-returned-as-the-element-name-in-the-resulting-xml"></a>Quando si esegue una query sulle viste utilizzando la modalità AUTO sul lato server, viene restituito il nome della vista come nome dell'elemento nel codice XML risultante.  
 Si supponga, ad esempio, nella tabella Person. Contact il AdventureWorksdatabase verrà creata la seguente visualizzazione:  
  
```  
CREATE VIEW ContactView AS (SELECT ContactID as CID,  
                               FirstName  as FName,  
                               LastName  as LName  
                        FROM Person.Contact)  
```  
  
 Nel modello seguente viene specificata una query sulla vista ContactView e viene inoltre specificata la formattazione XML sul lato server:  
  
```  
 <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <sql:query client-side-xml="0">  
    SELECT *  
    FROM   ContactView  
    FOR XML AUTO  
  </sql:query>  
</ROOT>  
```  
  
 Quando si esegue il modello, viene restituito il seguente codice XML. (Solo risultati parziali vengono visualizzati). Si noti che i nomi degli elementi sono i nomi delle viste in cui viene eseguita la query.  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <ContactView CID="1" FName="Gustavo" LName="Achong" />   
  <ContactView CID="2" FName="Catherine" LName="Abel" />   
...  
</ROOT>  
```  
  
 Quando si specifica la formattazione XML sul lato client tramite la modalità NESTED corrispondente, vengono restituiti i nomi delle tabelle di base come nomi degli elementi nel codice XML risultante. Ad esempio, il modello aggiornato seguente esegue la stessa istruzione SELECT, ma la formattazione XML viene eseguita sul lato client (ovvero, **xml del client** è impostata su true nel modello):  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <sql:query client-side-xml="1">  
    SELECT *  
    FROM   ContactView  
    FOR XML NESTED  
  </sql:query>  
</ROOT>  
```  
  
 L'esecuzione di questo modello genera il seguente codice XML. Notare che in questo caso il nome dell'elemento è il nome della tabella di base.  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <Person.Contact CID="1" FName="Gustavo" LName="Achong" />   
  <Person.Contact CID="2" FName="Catherine" LName="Abel" />   
...  
</ROOT>  
```  
  
### <a name="when-you-use-auto-mode-of-the-server-side-for-xml-the-table-aliases-specified-in-the-query-are-returned-as-element-names-in-the-resulting-xml"></a>Quando si utilizza la modalità AUTO di FOR XML sul lato server, vengono restituiti gli alias delle tabelle specificati nella query come nomi degli elementi nel codice XML risultante.  
 Considerare ad esempio il modello seguente:  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <sql:query client-side-xml="0">  
    SELECT FirstName as fname,  
           LastName as lname  
    FROM   Person.Contact C  
    FOR XML AUTO  
  </sql:query>  
</ROOT>  
```  
  
 L'esecuzione di questo modello genera il seguente codice XML.  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <C fname="Gustavo" lname="Achong" />   
  <C fname="Catherine" lname="Abel" />   
...  
</ROOT>   
```  
  
 Quando si utilizza la modalità NESTED di FOR XML sul lato client, vengono restituiti i nomi delle tabelle come nomi degli elementi nel codice XML risultante. (Alias di tabella specificati nella query non vengono usati). Considerare ad esempio il modello seguente:  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <sql:query client-side-xml="1">  
    SELECT FirstName as fname,  
           LastName as lname  
    FROM   Person.Contact C  
    FOR XML NESTED  
  </sql:query>  
</ROOT>  
```  
  
 L'esecuzione di questo modello genera il seguente codice XML.  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <Person.Contact fname="Gustavo" lname="Achong" />   
  <Person.Contact fname="Catherine" lname="Abel" />   
...  
</ROOT>  
```  
  
### <a name="if-you-have-a-query-that-returns-columns-as-dbobject-queries-you-cannot-use-aliases-for-these-columns"></a>Se si dispone di una query che restituisce colonne come query dbobject, non è possibile utilizzare gli alias per tali colonne.  
 Considerare ad esempio il modello seguente in cui viene eseguita una query che restituisce un ID dipendente e una foto.  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
<sql:query client-side-xml="1">  
   SELECT ProductPhotoID, LargePhoto as P  
   FROM   Production.ProductPhoto  
   WHERE  ProductPhotoID=5  
   FOR XML NESTED, elements  
</sql:query>  
</ROOT>  
```  
  
 L'esecuzione di questo modello restituisce la colonna Photo come query dbobject. In questa query dbobject `@P` si riferisce a un nome della colonna che non esiste.  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <Production.ProductPhoto>  
    <ProductPhotoID>5</ProductPhotoID>  
    <LargePhoto>dbobject/Production.ProductPhoto[@ProductPhotoID='5']/@P</LargePhoto>  
  </Production.ProductPhoto>  
</ROOT>  
```  
  
 Se la formattazione XML viene eseguita sul server (**xml del client = "0"**), è possibile utilizzare l'alias per le colonne che restituiscono dbobject una query nella quale tabella effettiva e una colonna vengono restituiti i nomi (anche se si dispone di alias specificati). Ad esempio, il modello seguente esegue una query e la formattazione XML viene eseguita sul server (il **xml del client** non è specificata l'opzione e la **eseguito sul Client** opzione non è selezionata per il directory principale virtuale). La query specifica anche la modalità AUTO (non la modalità NESTED sul lato client).  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
<sql:query   
   SELECT ProductPhotoID, LargePhoto as P  
   FROM   Production.ProductPhoto  
   WHERE  ProductPhotoID=5  
   FOR XML AUTO, elements  
</sql:query>  
</ROOT>  
```  
  
 Quando viene eseguito questo modello, viene restituito il documento XML seguente (notare che non vengono utilizzati gli alias nella query dbobject per la colonna LargePhoto):  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <Production.ProductPhoto>  
    <ProductPhotoID>5</ProductPhotoID>  
    <LargePhoto>dbobject/Production.ProductPhoto[@ProductPhotoID='5']/@LargePhoto</LargePhoto>  
  </Production.ProductPhoto>  
</ROOT>  
```  
  
### <a name="client-side-vs-server-side-xpath"></a>Lato client e XPath sul lato server  
 XPath sul lato client e XPath sul lato server funzionano allo stesso modo ad eccezione delle seguenti differenze:  
  
-   Le conversioni dei dati applicate quando si utilizzano le query XPath sul lato client sono diverse da quelle applicate quando si utilizzano le query XPath sul lato server. XPath sul lato client utilizza la modalità CAST anziché la modalità CONVERT 126.  
  
-   Quando si specifica **xml del client = "0"** (false) in un modello, si richiede la formattazione XML lato server. Pertanto, non è possibile specificare FOR XML NESTED poiché il server non riconosce l'opzione NESTED e viene quindi generato un errore. È necessario utilizzare le modalità AUTO, RAW o EXPLICIT riconosciute dal server.  
  
-   Quando si specifica **xml del client = "1"** (true) in un modello, si richiede la formattazione XML lato client. In questo caso, è possibile specificare FOR XML NESTED. Se si specifica FOR XML AUTO, la formattazione XML si verifica sul lato server anche se **xml del client = "1"** è specificato nel modello.  
  
## <a name="see-also"></a>Vedere anche  
 [Per considerazioni sulla sicurezza XML &#40;SQLXML 4.0&#41;](../../sqlxml-annotated-xsd-schemas-xpath-queries/security/for-xml-security-considerations-sqlxml-4-0.md)   
 [Formattazione XML sul lato client &#40;SQLXML 4.0&#41;](client-side-xml-formatting-sqlxml-4-0.md)   
 [Formattazione XML sul lato server &#40;SQLXML 4.0&#41;](server-side-xml-formatting-sqlxml-4-0.md)  
  
  
