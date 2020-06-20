---
title: Linee guida e limitazioni del caricamento bulk XML (SQLXML 4,0) | Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 1b39f5347a7ace6dc449be804144b105957b33e3
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85068194"
---
# <a name="guidelines-and-limitations-of-xml-bulk-load-sqlxml-40"></a>Linee guida e limitazioni per il caricamento bulk XML (SQLXML 4.0)
  Quando si utilizza il caricamento bulk XML, è consigliabile disporre di una certa familiarità con le linee guida e le limitazioni seguenti:  
  
-   Gli schemi inline non sono supportati.  
  
     Se nel documento XML di origine è presente uno schema inline, questo viene ignorato dal caricamento bulk XML. È necessario specificare lo schema di mapping per il caricamento bulk XML come esterno ai dati XML. Non è possibile specificare lo schema di mapping in un nodo usando l'attributo **xmlns = "x:schema"** .  
  
-   Un documento XML viene controllato per verificare che utilizzi un formato corretto, ma non viene convalidato.  
  
     Il caricamento bulk XML controlla il documento XML per determinare se il formato è corretto, ovvero per garantire che il codice XML sia conforme ai requisiti di sintassi della raccomandazione XML 1,0 del World Wide Web Consortium. Se il formato del documento non è corretto, il caricamento bulk XML annulla l'elaborazione e restituisce un errore. L'unica eccezione a questo comportamento è costituita dal caso in cui il documento è un frammento, ad esempio non dispone di un singolo elemento radice. In questo caso, il documento verrà caricato.  
  
     Il caricamento bulk XML non convalida il documento rispetto ad alcuno schema dati XML o DTD definito o a cui si fa riferimento all'interno del file di dati XML. Il caricamento bulk XML, inoltre, non convalida il file di dati XML rispetto allo schema di mapping fornito.  
  
-   Vengono ignorate tutte le informazioni sui prologhi XML.  
  
     Il caricamento bulk XML ignora tutte le informazioni prima e dopo l' \<root> elemento nel documento XML. Il caricamento bulk XML, ad esempio, ignora qualsiasi dichiarazione XML, qualsiasi definizione DTD interna e tutti i riferimenti DTD esterni, i commenti e così via.  
  
-   Se è presente uno schema di mapping che definisce una relazione di chiave primaria/chiave esterna tra due tabelle, ad esempio tra Customer e CustOrder, la tabella con la chiave primaria deve essere descritta per prima nello schema. La tabella con la colonna chiave esterna deve essere visualizzata come successiva nello schema. Il motivo è che l'ordine in cui le tabelle vengono identificate nello schema è l'ordine utilizzato per caricarle nel database. Lo schema XDR seguente, ad esempio, genera un errore quando viene utilizzato nel caricamento bulk XML, in quanto l' **\<Order>** elemento viene descritto prima dell' **\<Customer>** elemento. La colonna CustomerID in CustOrder è una colonna chiave esterna che fa riferimento alla colonna chiave primaria CustomerID nella tabella Cust.  
  
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
  
     Il caricamento bulk XML applica lo schema di mapping specificato ogni volta che rileva tag noti nel flusso di dati XML e ignora i dati presenti nel documento XML ma che non sono descritti nello schema. Si supponga, ad esempio, di disporre di uno schema di mapping che descrive un **\<Customer>** elemento. Il file di dati XML contiene un **\<AllCustomers>** tag radice, che non è descritto nello schema, che racchiude tutti gli **\<Customer>** elementi:  
  
    ```  
    <AllCustomers>  
      <Customer>...</Customer>  
      <Customer>...</Customer>  
       ...  
    </AllCustomers>  
    ```  
  
     In questo caso, il caricamento bulk XML ignora l' **\<AllCustomers>** elemento e inizia il mapping nell' **\<Customer>** elemento. Il caricamento bulk XML ignora gli elementi non descritti nello schema ma che sono presenti nel documento XML.  
  
     Si consideri un altro file di dati di origine XML contenente **\<Order>** elementi. Tali elementi non vengono descritti nello schema di mapping:  
  
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
  
     Questi elementi vengono ignorati dal caricamento bulk XML **\<Order>** . Tuttavia, se si utilizza l' `sql:overflow-field` annotazione nello schema per identificare una colonna come colonna di overflow, il caricamento bulk XML archivia tutti i dati non utilizzati in questa colonna.  
  
-   Le sezioni CDATA e i riferimenti a entità vengono convertiti nei rispettivi equivalenti in formato stringa prima di essere archiviati nel database.  
  
     In questo esempio una sezione CDATA esegue il wrapping del valore per l' **\<City>** elemento. Il caricamento bulk XML estrae il valore stringa ("NY") prima di inserire l' **\<City>** elemento nel database.  
  
    ```  
    <City><![CDATA[NY]]> </City>  
    ```  
  
     Il caricamento bulk XML non mantiene i riferimenti alle entità.  
  
-   Se lo schema di mapping specifica il valore predefinito per un attributo e i dati di origine XML non contengono tale attributo, il caricamento bulk XML utilizza il valore predefinito.  
  
     Nello schema XDR di esempio seguente viene assegnato un valore predefinito all'attributo **hirete** :  
  
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
  
     In questi dati XML non è presente l'attributo **Hiret** dal secondo **\<Customers>** elemento. Quando il caricamento bulk XML inserisce il secondo **\<Customers>** elemento nel database, utilizza il valore predefinito specificato nello schema.  
  
    ```  
    <ROOT>  
      <Customers CustomerID="1" HireDate="1999-01-01" Salary="10000" />  
      <Customers CustomerID="2" Salary="10000" />  
    </ROOT>  
    ```  
  
-   L'annotazione `sql:url-encode` non è supportata.  
  
     Non è possibile specificare un URL nei dati XML di input e prevedere che il caricamento bulk legga i dati da tale posizione.  
  
     Vengono create le tabelle identificate nello schema di mapping (il database deve essere presente). Se una o più tabelle sono già presenti nel database, la proprietà SGDropTables determina se le tabelle preesistenti devono essere eliminate e ricreate.  
  
-   Se si specifica la proprietà SchemaGen, ad esempio SchemaGen = true, vengono create le tabelle identificate nello schema di mapping. Tuttavia, SchemaGen non crea vincoli, ad esempio i vincoli PRIMARY KEY o FOREIGN KEY, in queste tabelle con un'unica eccezione: se i nodi XML che costituiscono la chiave primaria in una relazione sono definiti con un tipo XML di ID (ovvero `type="xsd:ID"` per XSD) e la proprietà SGUseID è impostata su true per SchemaGen, non solo le chiavi primarie vengono create dai nodi con ID tipizzato, ma le relazioni tra chiave primaria e chiave esterna vengono create dalle relazioni dello schema di mapping.  
  
-   In SchemaGen non vengono utilizzati facet e estensioni dello schema XSD per generare lo [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] schema relazionale.  
  
-   Se si specifica la proprietà SchemaGen (ad esempio, SchemaGen = true) per il caricamento bulk, verranno aggiornate solo le tabelle (e non le visualizzazioni di nome condiviso) specificate.  
  
-   SchemaGen fornisce solo le funzionalità di base per la generazione dello schema relazionale da XSD con annotazioni. Se necessario, l'utente deve modificare manualmente le tabelle generate.  
  
-   Quando tra le tabelle è presente più di una relazione, SchemaGen tenta di creare una singola relazione che include tutte le chiavi incluse tra le due tabelle. Questa limitazione può essere la causa di un errore [!INCLUDE[tsql](../../../includes/tsql-md.md)].  
  
-   Quando si esegue il caricamento bulk di dati XML in un database, deve essere presente almeno un attributo o un elemento figlio nello schema di mapping mappato a una colonna del database.  
  
-   Se si inseriscono valori di data tramite il caricamento bulk XML, i valori devono essere specificati nel formato (-)AAAA-MM-GG((+-)FO). Si tratta del formato XSD standard per la data.  
  
-   Alcuni flag della proprietà non sono compatibili con altri flag della proprietà stessa. Il caricamento bulk, ad esempio, non supporta il flag `Ignoreduplicatekeys=true` utilizzato con `Keepidentity=false`. Nel caso in cui `Keepidentity=false`, durante il caricamento bulk si prevede che il server generi i valori della chiave. Nelle tabelle deve essere presente un vincolo `IDENTITY` sulla chiave. Il server non genererà chiavi duplicate, il che significa che non c'è bisogno di impostare `Ignoreduplicatekeys` su `true`. `Ignoreduplicatekeys` deve essere impostato su `true` solo quando viene eseguito il caricamento di valori di chiave primaria dai dati in entrata in una tabella con righe ed è possibile un conflitto di valori di chiave primaria.  
  
  
