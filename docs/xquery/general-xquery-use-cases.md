---
title: Casi di utilizzo di XQuery generale | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- XQuery, general usage cases
ms.assetid: 5187c97b-6866-474d-8bdb-a082634039cc
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: cb95142a49fffef666be2e775e6e419c4df55290
ms.sourcegitcommit: bfa10c54e871700de285d7f819095d51ef70d997
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/14/2019
ms.locfileid: "54256216"
---
# <a name="general-xquery-use-cases"></a>Esempi di carattere generale sull'utilizzo di XQuery
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  In questo argomento vengono forniti esempi di carattere generale sull'utilizzo di XQuery.  
  
## <a name="examples"></a>Esempi  
  
### <a name="a-query-catalog-descriptions-to-find-products-and-weights"></a>A. Esecuzione di query sulle descrizioni del catalogo per la ricerca di prodotti e pesi  
 La query seguente restituisce gli ID e i pesi del modello di prodotto, se esistenti, disponibili nella descrizione del catalogo dei prodotti. La query costruisce un'istanza XML con il formato seguente:  
  
```  
<Product ProductModelID="...">  
  <Weight>...</Weight>  
</Product>  
```  
  
 Query:  
  
```  
SELECT CatalogDescription.query('  
declare namespace p1="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
  <Product  ProductModelID="{ (/p1:ProductDescription/@ProductModelID)[1] }">  
     {   
       /p1:ProductDescription/p1:Specifications/Weight   
     }   
  </Product>  
') as Result  
FROM Production.ProductModel  
WHERE CatalogDescription is not null  
```  
  
 Dalla query precedente si noti quanto segue:  
  
-   Il **dello spazio dei nomi** parola chiave nel prologo della XQuery definisce un prefisso dello spazio dei nomi utilizzato nel corpo della query.  
  
-   Il corpo della query costruisce il codice XML richiesto.  
  
-   Nella clausola WHERE, il **exist ()** metodo viene utilizzato per trovare solo le righe che contengono le descrizioni del catalogo prodotti. ovvero, il codice XML che contiene l'elemento <`ProductDescription`>.  
  
 Questo è il risultato:  
  
```  
<Product ProductModelID="19"/>  
<Product ProductModelID="23"/>   
<Product ProductModelID="25"/>   
<Product ProductModelID="28"><Weight>Varies with size.</Weight></Product>  
<Product ProductModelID="34"/>  
<Product ProductModelID="35"/>  
```  
  
 La query seguente recupera le stesse informazioni, ma solo per i modelli per i quali le descrizioni del catalogo dei prodotti includono il peso, ovvero l'elemento <`Weight`> nelle specifiche rappresentate dall'elemento <`Specifications`>. In questo esempio viene utilizzata WITH XMLNAMESPACES per dichiarare il prefisso pd e la relativa associazione dello spazio dei nomi. In questo modo, l'associazione non è descritto in entrambe le **query ()** metodo e nel **exist ()** (metodo).  
  
```  
WITH XMLNAMESPACES ('https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS pd)  
SELECT CatalogDescription.query('  
          <Product  ProductModelID="{ (/pd:ProductDescription/@ProductModelID)[1] }">  
                 {   
                      /pd:ProductDescription/pd:Specifications/Weight   
                 }   
          </Product>  
') as x  
FROM Production.ProductModel  
WHERE CatalogDescription.exist('/pd:ProductDescription/pd:Specifications//Weight ') = 1  
```  
  
 Nella query precedente, il **exist ()** metodo del **xml** tipo di dati nella clausola WHERE verifica se è presente un <`Weight`> elemento il <`Specifications`> elemento.  
  
### <a name="b-find-product-model-ids-for-product-models-whose-catalog-descriptions-include-front-angle-and-small-size-pictures"></a>b. Ricerca degli ID dei modelli del prodotto per cui sono disponibili descrizioni del catalogo che includono immagini frontali e di piccole dimensioni  
 La descrizione del catalogo prodotti XML include le immagini dei prodotti, ovvero l'elemento <`Picture`>. Ogni immagine ha diverse proprietà, che includono l'angolazione, ovvero l'elemento <`Angle`>, e le dimensioni, ovvero l'elemento <`Size`>.  
  
 Per i modelli con descrizioni del catalogo che includono immagini frontali e di piccole dimensioni, la query costruisce codice XML nel formato seguente:  
  
```  
< Product ProductModelID="...">  
  <Picture>  
    <Angle>front</Angle>  
    <Size>small</Size>  
  </Picture>  
</Product>  
WITH XMLNAMESPACES ('https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS pd)  
SELECT CatalogDescription.query('  
   <pd:Product  ProductModelID="{ (/pd:ProductDescription/@ProductModelID)[1] }">  
      <Picture>  
         {  /pd:ProductDescription/pd:Picture/pd:Angle }   
         {  /pd:ProductDescription/pd:Picture/pd:Size }   
      </Picture>  
   </pd:Product>  
') as Result  
FROM  Production.ProductModel  
WHERE CatalogDescription.exist('/pd:ProductDescription/pd:Picture') = 1  
AND   CatalogDescription.value('(/pd:ProductDescription/pd:Picture/pd:Angle)[1]', 'varchar(20)')  = 'front'  
AND   CatalogDescription.value('(/pd:ProductDescription/pd:Picture/pd:Size)[1]', 'varchar(20)')  = 'small'  
```  
  
 Dalla query precedente si noti quanto segue:  
  
-   Nella clausola WHERE, il **exist ()** metodo viene utilizzato per recuperare solo le righe che includono descrizioni del catalogo prodotti con il <`Picture`> elemento.  
  
-   La clausola WHERE utilizza il **Value ()** metodo due volte per confrontare i valori del <`Size`> e <`Angle`> elementi.  
  
 Risultato parziale:  
  
```  
<p1:Product   
  xmlns:p1="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription"   
  ProductModelID="19">  
  <Picture>  
    <p1:Angle>front</p1:Angle>  
    <p1:Size>small</p1:Size>  
  </Picture>  
</p1:Product>  
...  
```  
  
### <a name="c-create-a-flat-list-of-the-product-model-name-and-feature-pairs-with-each-pair-enclosed-in-the-features-element"></a>C. Creare un elenco semplice del prodotto coppie di nome e la funzione di modello, con ogni coppia racchiusa nel \<funzionalità > elemento  
 Nella descrizione del catalogo dei modelli, il codice XML contiene numerose caratteristiche del prodotto, che sono incluse nell'elemento <`Features`>. La query utilizza [costruzione di strutture XML (XQuery)](../xquery/xml-construction-xquery.md) per costruire il codice XML richiesto. L'espressione racchiusa tra parentesi graffe viene sostituita dal risultato.  
  
```  
SELECT CatalogDescription.query('  
declare namespace p1="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
  for $pd in /p1:ProductDescription,  
   $f in $pd/p1:Features/*  
  return  
   <Feature>  
     <ProductModelName> { data($pd/@ProductModelName) } </ProductModelName>  
     { $f }  
  </Feature>          
') as x  
FROM Production.ProductModel  
WHERE ProductModelID=19  
```  
  
 Dalla query precedente si noti quanto segue:  
  
-   $pd/p1:Features/* restituisce solo i nodi figlio di <`Features`>, mentre $pd/p1:Features/node() restituisce tutti i nodi, inclusi i nodi elemento, i nodi di testo, le istruzioni di elaborazione e i commenti.  
  
-   I due cicli FOR generano un prodotto cartesiano che restituisce il nome del prodotto e la singola caratteristica.  
  
-   Il **ProductName** è un attributo. e la costruzione XML di questa query lo restituisce come un elemento.  
  
 Risultato parziale:  
  
```  
<Feature>  
 <ProductModelName>Mountain 100</ProductModelName>  
 <ProductModelID>19</ProductModelID>  
 <p1:Warranty   
   xmlns:p1="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain">  
    <p1:WarrantyPeriod>3 year</p1:WarrantyPeriod>  
    <p1:Description>parts and labor</p1:Description>  
 </p1:Warranty>  
</Feature>  
<Feature>  
 <ProductModelName>Mountain 100</ProductModelName>  
 <ProductModelID>19</ProductModelID>  
 <p2:Maintenance xmlns:p2="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain">  
    <p2:NoOfYears>10</p2:NoOfYears>  
    <p2:Description>maintenance contact available through your dealer   
           or any AdventureWorks retail store.</p2:Description>  
    </p2:Maintenance>  
</Feature>  
...  
...      
```  
  
### <a name="d-from-the-catalog-description-of-a-product-model-list-the-product-model-name-model-id-and-features-grouped-inside-a-product-element"></a>D. Dalla descrizione del catalogo di un modello di prodotto, ID di modello, nome del modello elenco il prodotto e caratteristiche raggruppati all'interno di un \<Product > elemento  
 Usando le informazioni archiviate nella descrizione del catalogo del modello del prodotto, la query seguente elenca il nome del modello del prodotto, ID di modello, e caratteristiche raggruppati all'interno di un \<Product > elemento.  
  
```  
SELECT ProductModelID, CatalogDescription.query('  
     declare namespace pd="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
     <Product>  
         <ProductModelName>   
           { data(/pd:ProductDescription/@ProductModelName) }   
         </ProductModelName>  
         <ProductModelID>   
           { data(/pd:ProductDescription/@ProductModelID) }   
         </ProductModelID>  
         { /pd:ProductDescription/pd:Features/* }  
     </Product>          
') as x  
FROM Production.ProductModel  
WHERE ProductModelID=19  
```  
  
 Risultato parziale:  
  
```  
<Product>  
  <ProductModelName>Mountain 100</ProductModelName>  
  <ProductModelID>19</ProductModelID>  
  <p1:Warranty>... </p1:Warranty>  
  <p2:Maintenance>...  </p2:Maintenance>  
  <p3:wheel xmlns:p3="https://www.adventure-works.com/schemas/OtherFeatures">High performance wheels.</p3:wheel>  
  <p4:saddle xmlns:p4="https://www.adventure-works.com/schemas/OtherFeatures">  
    <p5:i xmlns:p5="http://www.w3.org/1999/xhtml">Anatomic design</p5:i> and made from durable leather for a full-day of riding in comfort.</p4:saddle>  
  <p6:pedal xmlns:p6="https://www.adventure-works.com/schemas/OtherFeatures">  
    <p7:b xmlns:p7="http://www.w3.org/1999/xhtml">Top-of-the-line</p7:b> clipless pedals with adjustable tension.</p6:pedal>  
   ...  
```  
  
### <a name="e-retrieve-product-model-feature-descriptions"></a>E. Recupero delle descrizioni delle caratteristiche del modello di prodotto  
 La query seguente costruisce codice XML che include un <`Product`> elemento avente **ProducModelID**, **ProductModelName** attributi e i primi due caratteristiche del prodotto. In particolare, le prime due caratteristiche del prodotto sono i primi due elementi figlio dell'elemento <`Features`>. Se sono disponibili più caratteristiche, verrà restituito un elemento <`There-is-more/`> vuoto.  
  
```  
SELECT CatalogDescription.query('  
declare namespace pd="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
     <Product>   
          { /pd:ProductDescription/@ProductModelID }  
          { /pd:ProductDescription/@ProductModelName }   
          {  
            for $f in /pd:ProductDescription/pd:Features/*[position()<=2]  
            return  
            $f   
          }  
          {  
            if (count(/pd:ProductDescription/pd:Features/*) > 2)  
            then <there-is-more/>  
            else ()  
          }   
     </Product>          
') as Result  
FROM Production.ProductModel  
WHERE CatalogDescription is not NULL  
```  
  
 Dalla query precedente si noti quanto segue:  
  
-   La struttura del ciclo FOR ... RETURN recupera le prime due caratteristiche del prodotto. Il **Position** funzione viene utilizzata per trovare la posizione degli elementi nella sequenza.  
  
### <a name="f-find-element-names-from-the-product-catalog-description-that-end-with-ons"></a>F. Ricerca dei nomi di elementi che terminano con "ons" nella descrizione del catalogo dei prodotti  
 La query seguente esegue una ricerca nelle descrizioni del catalogo e restituisce tutti gli elementi dell'elemento <`ProductDescription`> che terminano con "ons".  
  
```  
SELECT ProductModelID, CatalogDescription.query('  
     declare namespace p1="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
      for $pd in /p1:ProductDescription/*[substring(local-name(.),string-length(local-name(.))-2,3)="ons"]  
      return   
          <Root>  
             { $pd }  
          </Root>  
') as Result  
FROM Production.ProductModel  
WHERE CatalogDescription is not NULL  
```  
  
 Risultato parziale:  
  
```  
ProductModelID   Result  
-----------------------------------------  
         19        <Root>         
                     <p1:Specifications xmlns:p1="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription">          
                          ...         
                     </p1:Specifications>         
                   </Root>          
```  
  
### <a name="g-find-summary-descriptions-that-contain-the-word-aerodynamic"></a>G. Ricerca delle descrizioni di riepilogo che contengono la parola "Aerodynamic"  
 La query seguente recupera i modelli per cui sono disponibili descrizioni del catalogo che contengono la parola "Aerodynamic" nella descrizione di riepilogo:  
  
```  
WITH XMLNAMESPACES ('https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS pd)  
SELECT ProductModelID, CatalogDescription.query('  
          <Prod >  
             { /pd:ProductDescription/@ProductModelID }  
             { /pd:ProductDescription/pd:Summary }  
          </Prod>  
 ') as Result  
FROM Production.ProductModel  
WHERE CatalogDescription.value('  
     contains( string( (/pd:ProductDescription/pd:Summary)[1] ),"Aerodynamic")','bit') = 1  
```  
  
 Si noti che la query SELECT specifica **query ()** e **Value ()** metodi del **xml** tipo di dati. Anziché ripetere la dichiarazione dello spazio dei nomi in due prologhi di query diversi, nella query viene pertanto utilizzato il prefisso pd che è definito una sola volta tramite WITH XMLNAMESPACES.  
  
 Dalla query precedente si noti quanto segue:  
  
-   Viene utilizzata la clausola WHERE per recuperare solo le righe per le quali la descrizione del catalogo contiene la parola "Aerodynamic" nell'elemento <`Summary`>.  
  
-   Il **Contains ()** funzione viene utilizzata per determinare se la parola è inclusa nel testo.  
  
-   Il **Value ()** metodo per il **xml** tipo di dati confronta il valore restituito da **Contains ()** su 1.  
  
 Questo è il risultato:  
  
```  
ProductModelID Result        
-------------- ------------------------------------------  
28     <Prod ProductModelID="28">  
        <pd:Summary xmlns:pd="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription">  
       <p1:p xmlns:p1="http://www.w3.org/1999/xhtml">  
         A TRUE multi-sport bike that offers streamlined riding and a  
         revolutionary design. Aerodynamic design lets you ride with the   
         pros, and the gearing will conquer hilly roads.</p1:p>  
       </pd:Summary>  
      </Prod>    
```  
  
### <a name="h-find-product-models-whose-catalog-descriptions-do-not-include-product-model-pictures"></a>H. Ricerca dei modelli del prodotto per i quali le descrizioni del catalogo non includono immagini  
 La query seguente recupera i valori ProductModelID dei modelli per i quali le descrizioni del catalogo non includono un elemento <`Picture`>.  
  
```  
SELECT  ProductModelID  
FROM    Production.ProductModel  
WHERE   CatalogDescription is not NULL  
AND     CatalogDescription.exist('declare namespace p1="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
     /p1:ProductDescription/p1:Picture  
') = 0  
```  
  
 Dalla query precedente si noti quanto segue:  
  
-   Se il **exist ()** metodo nella clausola WHERE restituisce False (0), viene restituito l'ID di modello di prodotto. In caso contrario, l'ID del modello non viene restituito.  
  
-   Poiché tutte le descrizioni di prodotto includono un elemento <`Picture`>, in questo caso il set di risultati è vuoto.  
  
## <a name="see-also"></a>Vedere anche  
 [XQueries Involving Hierarchy](../xquery/xqueries-involving-hierarchy.md)   
 [XQueries Involving Order](../xquery/xqueries-involving-order.md)   
 [XQuery per la gestione di dati relazionali](../xquery/xqueries-handling-relational-data.md)   
 [Ricerca di stringhe in XQuery](../xquery/string-search-in-xquery.md)   
 [Gestione degli spazi dei nomi in XQuery](../xquery/handling-namespaces-in-xquery.md)   
 [Aggiungere spazi dei nomi alle query con WITH XMLNAMESPACES](../relational-databases/xml/add-namespaces-to-queries-with-with-xmlnamespaces.md)   
 [Dati XML &#40;SQL Server&#41;](../relational-databases/xml/xml-data-sql-server.md)   
 [Riferimento al linguaggio XQuery &#40;SQL Server&#41;](../xquery/xquery-language-reference-sql-server.md)  
  
  
