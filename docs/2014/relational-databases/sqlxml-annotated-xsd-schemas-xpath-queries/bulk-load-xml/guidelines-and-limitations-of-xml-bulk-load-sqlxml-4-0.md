---
title: Linee guida e le limitazioni di XML in blocco carico (SQLXML 4.0) | Documenti di Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- XML Bulk Load [SQLXML], about XML Bulk Load
- bulk load [SQLXML], about bulk load
ms.assetid: c5885d14-c7c1-47b3-a389-455e99a7ece1
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: b7a569bbc5672b0fc5996507e37ed250721bd2fe
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52774923"
---
# <a name="guidelines-and-limitations-of-xml-bulk-load-sqlxml-40"></a>Linee guida e limitazioni per il caricamento bulk XML (SQLXML 4.0)
  Quando si utilizza il caricamento bulk XML, è consigliabile disporre di una certa familiarità con le linee guida e le limitazioni seguenti:  
  
-   Gli schemi inline non sono supportati.  
  
     Se nel documento XML di origine è presente uno schema inline, questo viene ignorato dal caricamento bulk XML. È necessario specificare lo schema di mapping per il caricamento bulk XML come esterno ai dati XML. Non è possibile specificare lo schema di mapping in un nodo utilizzando il **xmlns = "x: schema"** attributo.  
  
-   Un documento XML viene controllato per verificare che utilizzi un formato corretto, ma non viene convalidato.  
  
     Caricamento Bulk XML controlla il documento XML per determinare se sia ben-formed-che è, per garantire che il codice XML sia conforme ai requisiti di sintassi della raccomandazione XML 1.0 del World Wide Web Consortium. Se il formato del documento non è corretto, il caricamento bulk XML annulla l'elaborazione e restituisce un errore. L'unica eccezione a questo comportamento è costituita dal caso in cui il documento è un frammento, ad esempio non dispone di un singolo elemento radice. In questo caso, il documento verrà caricato.  
  
     Il caricamento bulk XML non convalida il documento rispetto ad alcuno schema dati XML o DTD definito o a cui si fa riferimento all'interno del file di dati XML. Il caricamento bulk XML, inoltre, non convalida il file di dati XML rispetto allo schema di mapping fornito.  
  
-   Vengono ignorate tutte le informazioni sui prologhi XML.  
  
     Caricamento di massa XML Ignora tutte le informazioni prima e dopo la \<principale > elemento del documento XML. Il caricamento bulk XML, ad esempio, ignora qualsiasi dichiarazione XML, qualsiasi definizione DTD interna e tutti i riferimenti DTD esterni, i commenti e così via.  
  
-   Se è presente uno schema di mapping che definisce una relazione di chiave primaria/chiave esterna tra due tabelle, ad esempio tra Customer e CustOrder, la tabella con la chiave primaria deve essere descritta per prima nello schema. La tabella con la colonna chiave esterna deve essere visualizzata come successiva nello schema. La ragione è che l'ordine in cui vengono identificate le tabelle nello schema è l'ordine utilizzato per caricarli nel database. Ad esempio, il seguente schema XDR verrà generato un errore quando viene utilizzata nel caricamento di massa XML perché il  **\<ordine >** elemento descritto prima di  **\<cliente >** elemento. La colonna CustomerID in CustOrder è una colonna chiave esterna che fa riferimento alla colonna chiave primaria CustomerID nella tabella Cust.  
  
    ```  
    <?xml version="1.0" ?>  
    <Schema xmlns="urn:schemas-microsoft-com:xml-data"   
            xmlns:dt="urn:schemas-microsoft-com:xml:datatypes"    
            xmlns:sql="urn:schemas-microsoft-com:xml-sql" >  
  
        <ElementType name="Order" sql:relation="CustOrder" >  
          <AttributeType name="OrderID" />  
          <AttributeType name="CustomerID" />  
          <attribute type="OrderID" />  
          <attribute type="CustomerID" />  
        </ElementType>  
  
       <ElementType name="CustomerID" dt:type="int" />  
       <ElementType name="CompanyName" dt:type="string" />  
       <ElementType name="City" dt:type="string" />  
  
       <ElementType name="root" sql:is-constant="1">  
          <element type="Customers" />  
       </ElementType>  
       <ElementType name="Customers" sql:relation="Cust"   
                         sql:overflow-field="OverflowColumn"  >  
          <element type="CustomerID" sql:field="CustomerID" />  
          <element type="CompanyName" sql:field="CompanyName" />  
          <element type="City" sql:field="City" />  
          <element type="Order" >   
               <sql:relationship  
                   key-relation="Cust"  
                    key="CustomerID"  
                    foreign-key="CustomerID"  
                    foreign-relation="CustOrder" />  
          </element>  
       </ElementType>  
    </Schema>  
    ```  
  
-   Se lo schema non specifica colonne di overflow tramite l'annotazione `sql:overflow-field`, il caricamento bulk XML ignora tutti i dati presenti nel documento XML ma che non sono descritti nello schema di mapping.  
  
     Il caricamento bulk XML applica lo schema di mapping specificato ogni volta che rileva tag noti nel flusso di dati XML e ignora i dati presenti nel documento XML ma che non sono descritti nello schema. Ad esempio, si supponga di disporre di uno schema di mapping che descrive un  **\<cliente >** elemento. Nel file di dati XML sono un  **\<AllCustomers >** principale tag (che non è descritto nello schema) che racchiude tutte le  **\<cliente >** elementi:  
  
    ```  
    <AllCustomers>  
      <Customer>...</Customer>  
      <Customer>...</Customer>  
       ...  
    </AllCustomers>  
    ```  
  
     In questo caso, il caricamento di massa XML ignora il  **\<AllCustomers >** elemento e inizia in lingua inglese di  **\<cliente >** elemento. Il caricamento bulk XML ignora gli elementi non descritti nello schema ma che sono presenti nel documento XML.  
  
     Si consideri un altro file di dati origine XML contenente  **\<ordine >** elementi. Tali elementi non vengono descritti nello schema di mapping:  
  
    ```  
    <AllCustomers>  
      <Customer>...</Customer>  
        <Order> ... </Order>  
        <Order> ... </Order>  
         ...  
      <Customer>...</Customer>  
        <Order> ... </Order>  
        <Order> ... </Order>  
         ...  
      ...  
    </AllCustomers>  
    ```  
  
     Caricamento di massa XML ignora questi  **\<ordine >** elementi. Se tuttavia si utilizza il `sql:overflow-field`annotazione nello schema per identificare una colonna come colonna di overflow, il caricamento Bulk XML archivia tutti i dati non utilizzati in questa colonna.  
  
-   Le sezioni CDATA e i riferimenti a entità vengono convertiti nei rispettivi equivalenti in formato stringa prima di essere archiviati nel database.  
  
     In questo esempio, una sezione CDATA include il valore per la  **\<città >** elemento. Caricamento di massa XML estrae il valore di stringa ("NY") prima di inserire la  **\<città >** elemento nel database.  
  
    ```  
    <City><![CDATA[NY]]> </City>  
    ```  
  
     Il caricamento bulk XML non mantiene i riferimenti alle entità.  
  
-   Se lo schema di mapping specifica il valore predefinito per un attributo e i dati di origine XML non contengono tale attributo, il caricamento bulk XML utilizza il valore predefinito.  
  
     Lo schema XDR di esempio seguente viene assegnato un valore predefinito per il **HireDate** attributo:  
  
    ```  
    <?xml version="1.0" ?>  
    <Schema xmlns="urn:schemas-microsoft-com:xml-data"   
            xmlns:dt="urn:schemas-microsoft-com:xml:datatypes"    
            xmlns:sql="urn:schemas-microsoft-com:xml-sql" >  
       <ElementType name="root" sql:is-constant="1">  
          <element type="Customers" />  
       </ElementType>  
  
       <ElementType name="Customers" sql:relation="Cust3" >  
          <AttributeType name="CustomerID" dt:type="int"  />  
          <AttributeType name="HireDate"  default="2000-01-01" />  
          <AttributeType name="Salary"   />  
  
          <attribute type="CustomerID" sql:field="CustomerID" />  
          <attribute type="HireDate"   sql:field="HireDate"  />  
          <attribute type="Salary"     sql:field="Salary"    />  
       </ElementType>  
    </Schema>  
    ```  
  
     In questi dati XML, il **HireDate** non è presente il secondo attributo  **\<clienti >** elemento. Quando il caricamento di massa XML consente di inserire il secondo  **\<clienti >** elemento nel database, viene utilizzato il valore predefinito specificato nello schema.  
  
    ```  
    <ROOT>  
      <Customers CustomerID="1" HireDate="1999-01-01" Salary="10000" />  
      <Customers CustomerID="2" Salary="10000" />  
    </ROOT>  
    ```  
  
-   L'annotazione `sql:url-encode` non è supportata.  
  
     Non è possibile specificare un URL nei dati XML di input e prevedere che il caricamento bulk legga i dati da tale posizione.  
  
     Vengono create le tabelle identificate nello schema di mapping (il database deve essere presente). Se esiste già uno o più delle tabelle nel database, la proprietà SGDropTables determina se queste tabelle preesistenti devono essere eliminati e ricreati.  
  
-   Se si specifica la proprietà SchemaGen (ad esempio, SchemaGen = true), vengono create le tabelle che vengono identificate nello schema di mapping. SchemaGen senza tuttavia creare eventuali vincoli (ad esempio i vincoli di chiave primaria/chiave esterna) in tali tabelle con una sola eccezione: Se i nodi XML che costituiscono la chiave primaria in una relazione sono definiti con un tipo XML dell'ID (vale a dire, `type="xsd:ID"` per XSD) e sguseid-proprietà è impostata su True per SchemaGen, quindi non sono chiavi primarie create solo dall'ID tipizzata nodi , ma primarie/chiave relazioni di chiave esterna vengono create dal mapping di relazioni dello schema.  
  
-   SchemaGen non utilizza estensioni e i facet dello schema XSD per generare il relazionale [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] schema.  
  
-   Se si specifica la proprietà SchemaGen (ad esempio, SchemaGen = true) on Bulk Load, solo tabelle (e non le visualizzazioni del nome condiviso) che sono specificati vengono aggiornati.  
  
-   SchemaGen fornisce solo le funzionalità di base per la generazione dello schema relazionale da annotazioni XSD. Se necessario, l'utente deve modificare manualmente le tabelle generate.  
  
-   In cui sussistono più relazioni tra tabelle, SchemaGen prova a creare una singola relazione che include tutte le chiavi interessate tra le due tabelle. Questa limitazione può essere la causa di un errore [!INCLUDE[tsql](../../../includes/tsql-md.md)].  
  
-   Quando si esegue il caricamento bulk di dati XML in un database, deve essere presente almeno un attributo o un elemento figlio nello schema di mapping mappato a una colonna del database.  
  
-   Se si inseriscono valori di data tramite il caricamento bulk XML, i valori devono essere specificati nel formato (-)AAAA-MM-GG((+-)FO). Si tratta del formato XSD standard per la data.  
  
-   Alcuni flag della proprietà non sono compatibili con altri flag della proprietà stessa. Il caricamento bulk, ad esempio, non supporta il flag `Ignoreduplicatekeys=true` utilizzato con `Keepidentity=false`. Nel caso in cui `Keepidentity=false`, durante il caricamento bulk si prevede che il server generi i valori della chiave. Nelle tabelle deve essere presente un vincolo `IDENTITY` sulla chiave. Il server non genererà chiavi duplicate, il che significa che non c'è bisogno di impostare `Ignoreduplicatekeys` su `true`. `Ignoreduplicatekeys` deve essere impostato su `true` solo quando viene eseguito il caricamento di valori di chiave primaria dai dati in entrata in una tabella con righe ed è possibile un conflitto di valori di chiave primaria.  
  
  
