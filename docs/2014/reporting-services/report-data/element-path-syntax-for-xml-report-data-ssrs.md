---
title: Sintassi del percorso di elemento per i dati del report XML (SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- ElementPath syntax
- XML [Reporting Services], data retrieval
ms.assetid: 07bd7a4e-fd7a-4a72-9344-3258f7c286d1
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 65dc39f60805cf5e3587639404be2bb19b4ea443
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62696115"
---
# <a name="element-path-syntax-for-xml-report-data-ssrs"></a>Sintassi del percorso di elemento per i dati del report XML (SSRS)
  In Progettazione report è possibile specificare i dati da utilizzare per un report da un'origine dati XML definendo un percorso di elemento con distinzione tra maiuscole e minuscole. Un percorso di elemento indica come attraversare i nodi gerarchici XML e i relativi attributi nell'origine dei dati XML. Per utilizzare il percorso di elemento predefinito, lasciare vuota la query del set di dati o il nodo `ElementPath` XML dell'elemento `Query` XML. Quando vengono recuperati i dati dall'origine dei dati XML, i nodi elemento con valori di testo e gli attributi dei nodi elemento diventano colonne del set di risultati. Quando si esegue la query, i valori dei nodi e degli attributi diventano i dati delle righe. Le colonne sono visualizzate come raccolta di campi di set di dati nel riquadro Dati report. In questo argomento viene descritta la sintassi del percorso di elemento.  
  
> [!NOTE]  
>  La sintassi del percorso di elemento è indipendente dallo spazio dei nomi. Per usare gli spazi dei nomi in un percorso di elemento, usare la sintassi di query XML che include un file XML `ElementPath` descritto in [sintassi di Query XML per dati del Report XML &#40;SSRS&#41;](report-data-ssrs.md).  
  
 Nella tabella seguente vengono descritte le convenzioni utilizzate per definire un percorso di elemento.  
  
|Convenzione|Utilizzo|  
|----------------|--------------|  
|**grassetto**|Il testo deve essere digitato esattamente come illustrato.|  
|&#124; (barra verticale)|Separa gli elementi della sintassi. Indica che è possibile scegliere un solo elemento.|  
|`[ ] (brackets)`|Elementi sintattici facoltativi. Le parentesi quadre non devono essere digitate.|  
|**{ }** (parentesi graffe)|Delimitano i parametri degli elementi della sintassi.|  
|[**,**...*n*]|Indica che l'elemento precedente può essere ripetuto *n* volte. Le varie occorrenze dell'elemento sono separate da una virgola.|  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
Element path ::=  
    ElementNode[/Element path]  
ElementNode ::=  
    XMLName[(Encoding)][{[FieldList]}]  
XMLName ::=  
    [NamespacePrefix:]XMLLocalName  
Encoding ::=  
        HTMLEncoded | Base64Encoded  
FieldList ::=  
    Field[,FieldList]  
Field ::=  
    Attribute | Value | Element | ElementNode  
Attribute ::=  
        @XMLName[(Type)]  
Value ::=  
        @[(Type)]  
Element ::=  
    XMLName[(Type)]  
Type ::=  
        String | Integer | Boolean | Float | Decimal | Date | XML   
NamespacePrefix ::=  
    Identifier that specifies the namespace.  
XMLLocalName :: =  
    Identifier in the XML tag.   
```  
  
## <a name="remarks"></a>Note  
 Nella tabella seguente sono riepilogati i termini del percorso di elemento. Gli esempi della tabella si riferiscono al documento XML di esempio Customers.xml, incluso nella sezione relativa agli esempi di questo argomento.  
  
> [!NOTE]  
>  Nei tag XML viene fatta distinzione tra maiuscole e minuscole. Se nel percorso di elemento si specifica un nodo ElementNode, è necessario che corrisponda esattamente ai tag XML dell'origine dei dati.  
  
|Nome|Definizione|  
|----------|----------------|  
|Element path|Definisce la sequenza di nodi da attraversare nel documento XML per recuperare i dati del campo di un set di dati con un'origine dei dati XML.|  
|`ElementNode`|Nodo XML nel documento XML. I nodi sono designati da tag e sono correlati agli altri nodi in base a una relazione gerarchica. Customers>\<, ad esempio, è il nodo elemento radice. Customer>\< è un sottoelemento di Customers>\<.|  
|`XMLName`|Nome del nodo. Il nome del nodo Customers, ad esempio, è Customers. `XMLName` può essere preceduto da un identificatore dello spazio dei nomi, per assegnare a ogni nodo un nome univoco.|  
|`Encoding`|Indica che il valore `Value` dell'elemento è un valore XML con codifica e deve essere decodificato e incluso come sottoelemento dell'elemento.|  
|`FieldList`|Definisce il set di elementi e attributi da utilizzare per recuperare i dati.<br /><br /> Se non specificato, vengono utilizzati come campi tutti gli attributi e i sottoelementi. Se viene specificato l'elenco dei campi vuoto (**{}**), non verrà usato alcun campo di questo nodo.<br /><br /> Un elemento `FieldList` potrebbe non contenere sia `Value` che `Element` o `ElementNode`.|  
|`Field`|Specifica i dati recuperati come campo del set di dati.|  
|`Attribute`|Coppia nome-valore contenuta in `ElementNode`. Ad esempio, nel nodo dell'elemento \<Customer ID = "1" >, `ID` è un attributo e `@ID(Integer)` restituisce "1" come tipo integer nel campo dati corrispondente `ID`.|  
|`Value`|Valore dell'elemento. `Value` può essere utilizzato solo nell'ultimo `ElementNode` del percorso di elemento. Ad esempio, in quanto \<restituire > è un nodo foglia, se lo si include alla fine di un percorso di elemento, il valore di `Return {@}` è `Chair`.|  
|`Element`|Valore del sottoelemento denominato. Customers {}/Customer {}/LastName recupera, ad esempio, i valori solo per l'elemento LastName.|  
|`Type`|Tipo di dati facoltativo da utilizzare per il campo creato da questo elemento.|  
|`NamespacePrefix`|`NamespacePrefix` è definito nell'elemento Query XML. Se non è presente alcun elemento Query XML, gli spazi dei nomi del nodo `ElementPath` XML vengono ignorati. Se è presente un elemento Query XML, il nodo `ElementPath` XML include un attributo `IgnoreNamespaces` facoltativo. Se IgnoreNamespaces `true`, gli spazi dei nomi nel codice XML `ElementPath` e il documento XML vengono ignorati. Per altre informazioni, vedere [Sintassi di XML Query per i dati del report XML &#40;SSRS&#41;](report-data-ssrs.md).|  
  
## <a name="example---no-namespaces"></a>Esempio - Nessuno spazio dei nomi  
 Negli esempi seguenti viene utilizzato il documento XML Customers.xml. In questa tabella sono illustrati esempi di sintassi del percorso di elemento e i risultati dell'utilizzo del percorso di elemento in una query per la definizione di un set di dati, basata sul documento XML come origine dati.  
  
 Si noti che quando il percorso dell'elemento è vuoto, la query Usa il percorso di elemento predefinito: il primo percorso di una raccolta di nodi foglia. Nel primo esempio l'utilizzo di un percorso di elemento vuoto corrisponde alla definizione del percorso di elemento /Customers/Customer/Orders/Order. Tutti gli attributi e i valori del nodo nel percorso vengono restituiti nel set di risultati, mentre i nomi degli attributi e del nodo vengono visualizzati come campi del set di dati.  
  
-   *Vuoto*  
  
    |JSON|Qty|ID|FirstName|LastName|Customer.ID|xmlns|  
    |-----------|---------|--------|---------------|--------------|-----------------|-----------|  
    |Chair|6|1|Bobby|Moore|11|http://www.adventure-works.com|  
    |Tabella|1|2|Bobby|Moore|11|http://www.adventure-works.com|  
    |Sofa|2|8|Crystal|Hu|20|http://www.adventure-works.com|  
    |EndTables|2|15|Wyatt|Diaz|33|http://www.adventure-works.com|  
  
-   `Customers {}/Customer`  
  
    |FirstName|LastName|ID|  
    |---------------|--------------|--------|  
    |Bobby|Moore|11|  
    |Crystal|Hu|20|  
    |Wyatt|Diaz|33|  
  
-   `Customers {}/Customer {}/LastName`  
  
    |LastName|  
    |--------------|  
    |Moore|  
    |Hu|  
    |Diaz|  
  
-   `Customers {}/Customer {}/Orders/Order {@,@Qty}`  
  
    |JSON|Qty|  
    |-----------|---------|  
    |Chair|6|  
    |Tabella|1|  
    |Sofa|2|  
    |EndTables|2|  
  
-   `Customers {}/Customer/Orders/Order{ @ID(Integer)}`  
  
    |Order.ID|FirstName|LastName|ID|  
    |--------------|---------------|--------------|--------|  
    |1|Bobby|Moore|11|  
    |2|Bobby|Moore|11|  
    |8|Crystal|Hu|20|  
    |15|Wyatt|Diaz|33|  
  
#### <a name="xml-document-customersxml"></a>Documento XML: Customers.xml  
 Per provare gli esempi di percorso di elemento nella sezione precedente, copiare questo codice XML e salvarlo in un URL accessibile da Progettazione report e quindi usare il documento XML come origine dati XML, ad esempio `http://localhost/Customers.xml`.  
  
```  
<?xml version="1.0"?>  
<Customers xmlns="http://www.adventure-works.com">  
   <Customer ID="11">  
      <FirstName>Bobby</FirstName>  
      <LastName>Moore</LastName>  
      <Orders>  
         <Order ID="1" Qty="6">Chair</Order>  
         <Order ID="2" Qty="1">Table</Order>  
      </Orders>  
      <Returns>  
         <Return ID="1" Qty="2">Chair</Return>  
      </Returns>  
   </Customer>  
   <Customer ID="20">  
      <FirstName>Crystal</FirstName>  
      <LastName>Hu</LastName>  
      <Orders>  
         <Order ID="8" Qty="2">Sofa</Order>  
      </Orders>  
      <Returns/>  
   </Customer>  
   <Customer ID="33">  
      <FirstName>Wyatt</FirstName>  
      <LastName>Diaz</LastName>  
      <Orders>  
         <Order ID="15" Qty="2">EndTables</Order>  
      </Orders>  
      <Returns/>  
   </Customer>  
</Customers>  
```  
  
 In alternativa, è possibile creare un'origine dati XML senza una stringa di connessione e incorporare Customers.XML nella query, attenendosi alla procedura seguente:  
  
###### <a name="to-embed-customersxml-in-a-query"></a>Per incorporare Customers.XML in una query  
  
1.  Creare un'origine dati XML con una stringa di connessione vuota.  
  
2.  Creare un nuovo set di dati per l'origine dati XML.  
  
3.  Nella finestra di dialogo **Proprietà set di dati** fare clic su **Progettazione query**. Verrà visualizzata la finestra di dialogo Progettazione query basata su testo.  
  
4.  Nel riquadro delle query immettere le due righe seguenti:  
  
     `<Query>`  
  
     `<XmlData>`  
  
5.  Copiare Customers.XML e incollare il testo nel riquadro delle query dopo `<XmlData>`.  
  
6.  Nel riquadro delle query eliminare la prima riga copiata da Customers.XML: `<?xml version="1.0"?>`  
  
7.  Aggiungere le due righe seguenti alla fine della query:  
  
     `<XmlData>`  
  
     `<Query>`  
  
8.  Fare clic su **Esegui query** (!).  
  
     Nel set di risultati vengono visualizzate 4 righe di dati con le colonne seguenti: `xmlns`, `Customer.ID`, `FirstName`, `LastName`, `ID`, `Qty`, `Order`.  
  
9. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>Vedere anche  
 [Tipo di connessione XML &#40;SSRS&#41;](xml-connection-type-ssrs.md)   
 [Esercitazioni su Reporting Services &#40;SSRS&#41;](../reporting-services-tutorials-ssrs.md)   
 [Aggiunta, modifica e aggiornamento di campi nel riquadro dei dati del report &#40;Generatore report e SSRS&#41;](add-edit-refresh-fields-in-the-report-data-pane-report-builder-and-ssrs.md)  
  
  
