---
title: Problemi di concorrenza di database negli updategram (SQLXML)
description: Viene illustrato come utilizzare il meccanismo di controllo della concorrenza ottimistica negli updategram (SQLXML 4,0) per gestire i problemi di concorrenza del database.
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- <before> block
- low concurrency protection
- database concurrency [SQLXML]
- timestamp column [SQLXML]
- updategrams [SQLXML], database concurrency
- high concurrency protection [SQLXML]
- optimistic concurrency control
- concurrency [SQLXML]
- intermediate concurrency protection [SQLXML]
ms.assetid: d4b908d1-b25b-4ad9-8478-9cd882e8c44e
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 0f7c39eac7fc19d9f35c800f71ac874159fe284b
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2020
ms.locfileid: "97479202"
---
# <a name="handling-database-concurrency-issues-in-updategrams-sqlxml-40"></a>Gestione dei problemi di concorrenza di database negli updategram (SQLXML 4.0)
[!INCLUDE [SQL Server Azure SQL Database](../../../includes/applies-to-version/sql-asdb.md)]
  Analogamente ad altri meccanismi di aggiornamento del database, gli updategram devono gestire aggiornamenti simultanei ai dati in un ambiente multiutente. Gli updategram utilizzano il controllo della concorrenza ottimistica, che esegue il confronto dei dati di campo come snapshot per garantire che i dati da aggiornare non siano già stati modificati da un'altra applicazione utente dal momento in cui sono stati letti dal database. Gli updategram includono questi valori di snapshot nel **\<before>** blocco degli updategram. Prima di aggiornare il database, l'updategram controlla i valori specificati nel **\<before>** blocco rispetto ai valori attualmente presenti nel database per garantire che l'aggiornamento sia valido.  
  
 Il controllo della concorrenza ottimistica offre tre livelli di protezione in un updategram: basso (nessuno), intermedio ed elevato. È possibile stabilire il livello di protezione necessario specificando l'updategram di conseguenza.  
  
## <a name="lowest-level-of-protection"></a>Livello di protezione più basso  
 Questo livello corrisponde a un aggiornamento nascosto, in cui l'aggiornamento viene elaborato senza riferimento ad altri aggiornamenti eseguiti dall'ultima lettura del database. In tal caso, si specificano solo le colonne chiave primaria nel **\<before>** blocco per identificare il record e si specificano le informazioni aggiornate nel **\<after>** blocco.  
  
 Il nuovo numero di telefono del contatto nell'updategram seguente, ad esempio, è corretto, indipendentemente dal numero di telefono precedente. Si noti che il **\<before>** blocco specifica solo la colonna chiave primaria (ContactID).  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
<updg:sync >  
<updg:before>  
   <Person.Contact ContactID="1" />  
</updg:before>  
<updg:after>  
   <Person.Contact ContactID="1" Phone="111-111-1111" />  
</updg:after>  
</updg:sync>  
</ROOT>  
```  
  
## <a name="intermediate-level-of-protection"></a>Livello di protezione intermedio  
 In questo livello di protezione l'updategram confronta i valori correnti dei dati aggiornati con i valori nelle colonne del database per verificare che i valori non siano stati modificati da altre transazioni dalla lettura del record da parte della transazione.  
  
 È possibile ottenere questo livello di protezione specificando le colonne chiave primaria e le colonne che si stanno aggiornando nel **\<before>** blocco.  
  
 Questo updategram, ad esempio, modifica il valore nella colonna Phone della tabella Person.Contact per il contatto con ContactID 1. Il **\<before>** blocco specifica l'attributo **Phone** per garantire che il valore dell'attributo corrisponda al valore nella colonna corrispondente nel database prima di applicare il valore aggiornato.  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
<updg:sync >  
<updg:before>  
   <Person.Contact ContactID="1" Phone="398-555-0132" />  
</updg:before>  
<updg:after>  
   <Person.Contact ContactID="1" Phone="111-111-1111" />  
</updg:after>  
</updg:sync>  
</ROOT>  
```  
  
## <a name="high-level-of-protection"></a>Livello di protezione elevato  
 Un livello di protezione elevato garantisce che il record resti inalterato dall'ultima lettura da parte dell'applicazione, ovvero dal momento in cui l'applicazione ha letto il record, che non è stato modificato da alcuna transazione.  
  
 Per ottenere questo livello di protezione elevato contro aggiornamenti simultanei, sono disponibili due metodi:  
  
-   Consente di specificare colonne aggiuntive nella tabella del **\<before>** blocco.  
  
     Se si specificano colonne aggiuntive nel **\<before>** blocco, l'updategram confronta i valori specificati per le colonne con i valori presenti nel database prima di applicare l'aggiornamento. Se una o più delle colonne dei record è stata modificata dal momento in cui la transazione ha letto il record, l'updategram non esegue l'aggiornamento.  
  
     Nell'updategram seguente, ad esempio, viene aggiornato il nome dello spostamento, ma vengono specificate colonne aggiuntive (StartTime, EndTime) nel **\<before>** blocco, in modo da richiedere un livello di protezione più elevato rispetto agli aggiornamenti simultanei.  
  
    ```  
    <ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
    <updg:sync >  
    <updg:before>  
       <HumanResources.Shift ShiftID="1"   
                 Name="Day"   
                 StartTime="1900-01-01 07:00:00.000"   
                 EndTime="1900-01-01 15:00:00.000" />  
    </updg:before>  
    <updg:after>  
       <HumanResources.Shift Name="Morning" />  
    </updg:after>  
    </updg:sync>  
    </ROOT>  
    ```  
  
     In questo esempio viene specificato il livello di protezione più elevato specificando tutti i valori di colonna per il record nel **\<before>** blocco.  
  
-   Consente di specificare la colonna timestamp, se disponibile, nel **\<before>** blocco.  
  
     Anziché specificare tutte le colonne dei record nel blocco * * \<before**> , è possibile specificare solo la colonna timestamp, se presente nella tabella, insieme alle colonne chiave primaria nel **\<before>** blocco. Il database aggiorna la colonna timestamp a un valore univoco dopo ogni aggiornamento del record. In questo caso, l'updategram confronta il valore del timestamp con il valore corrispondente nel database. Il valore del timestamp archiviato nel database è un valore binary. Pertanto, è necessario specificare la colonna timestamp nello schema come **DT: Type = "bin. Hex"**, **DT: Type = "bin. base64"** o **SQL: DataType = "timestamp"**. È possibile specificare il tipo di dati **XML** o [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] tipo di dati.)  
  
#### <a name="to-test-the-updategram"></a>Per testare l'updategram  
  
1.  Creare questa tabella nel database **tempdb** :  
  
    ```  
    USE tempdb  
    CREATE TABLE Customer (  
                 CustomerID  varchar(5),  
                 ContactName varchar(20),  
                 LastUpdated timestamp)  
    ```  
  
2.  Aggiungere il record di esempio seguente:  
  
    ```  
    INSERT INTO Customer (CustomerID, ContactName) VALUES   
                         ('C1', 'Andrew Fuller')  
    ```  
  
3.  Copiare lo schema XSD seguente e incollarlo in Blocco note. Salvarlo come file ConcurrencySampleSchema.xml:  
  
    ```  
    <xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
                xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
      <xsd:element name="Customer" sql:relation="Customer" >  
       <xsd:complexType>  
            <xsd:attribute name="CustomerID"    
                           sql:field="CustomerID"   
                           type="xsd:string" />   
  
            <xsd:attribute name="ContactName"    
                           sql:field="ContactName"   
                           type="xsd:string" />  
  
            <xsd:attribute name="LastUpdated"   
                           sql:field="LastUpdated"   
                           type="xsd:hexBinary"   
                 sql:datatype="timestamp" />  
  
        </xsd:complexType>  
      </xsd:element>  
    </xsd:schema>  
    ```  
  
4.  Copiare il codice dell'updategram seguente in Blocco note e salvarlo come ConcurrencySampleTemplate.xml nella stessa directory in cui è stato salvato lo schema creato nel passaggio precedente. Si noti che il valore del timestamp indicato di seguito per LastUpdated differirà nella tabella Customer di esempio. Copiare pertanto il valore effettivo di LastUpdated dalla tabella e incollarlo nell'updategram.  
  
    ```  
    <ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
    <updg:sync mapping-schema="SampleSchema.xml" >  
    <updg:before>  
       <Customer CustomerID="C1"   
                 LastUpdated = "0x00000000000007D1" />  
    </updg:before>  
    <updg:after>  
       <Customer ContactName="Robert King" />  
    </updg:after>  
    </updg:sync>  
    </ROOT>  
    ```  
  
5.  Creare e utilizzare lo script di test SQLXML 4.0 (Sqlxml4test.vbs) per eseguire il modello.  
  
     Per ulteriori informazioni, vedere [utilizzo di ADO per eseguire query SQLXML 4,0](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
 Di seguito viene indicato lo schema XDR equivalente:  
  
```  
<?xml version="1.0" ?>  
<Schema xmlns="urn:schemas-microsoft-com:xml-data"  
        xmlns:dt="urn:schemas-microsoft-com:datatypes"  
        xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
<ElementType name="Customer" sql:relation="Customer" >  
    <AttributeType name="CustomerID" />  
    <AttributeType name="ContactName" />  
    <AttributeType name="LastUpdated"  dt:type="bin.hex"   
                                       sql:datatype="timestamp" />  
    <attribute type="CustomerID" />  
    <attribute type="ContactName" />  
    <attribute type="LastUpdated" />  
</ElementType>  
</Schema>  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Considerazioni sulla sicurezza degli updategram &#40;SQLXML 4,0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/security/updategram-security-considerations-sqlxml-4-0.md)  
  
  
