---
title: Direttiva TYPE in query FOR XML | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- FOR XML clause, TYPE directive
- TYPE directive
ms.assetid: a3df6c30-1f25-45dc-b5a9-bd0e41921293
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 21ff73c95bb85167dfba64d434ed7b6c42051c07
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63193282"
---
# <a name="type-directive-in-for-xml-queries"></a>Direttiva TYPE in query FOR XML
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] supporto per la [xml &#40;Transact-SQL&#41; ](/sql/t-sql/xml/xml-transact-sql) consente di richiedere facoltativamente che il risultato di una query FOR XML venga restituito come `xml` tipo di dati, specificando la direttiva TYPE. In questo modo è possibile elaborare il risultato di una query FOR XML sul server. Ad esempio, è possibile specificare un'espressione XQuery, assegnare il risultato a un `xml` variabile di tipo oppure scrivere [query FOR XML annidate](use-nested-for-xml-queries.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] restituisce dati di istanza di tipo XML al client come risultato di diversi costrutti server, ad esempio query FOR XML che utilizzano la direttiva TYPE o in cui il tipo di dati `xml` viene utilizzato per la restituzione di valori dei dati dell'istanza XML da colonne di tabella e parametri di output SQL. Nel codice delle applicazioni client, il provider ADO.NET richiede che le informazioni sui tipi di dati XML vengano inviate dal server in codifica binaria. Se tuttavia si utilizza FOR XML senza la direttiva TYPE, i dati XML vengono restituiti come tipo stringa. In tutti i casi, il provider client sarà sempre in grado di gestire entrambe i formati di XML. La clausola FOR XML di livello principale senza la direttiva TYPE non può essere utilizzata con i cursori.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene illustrato l'utilizzo della direttiva TYPE con le query FOR XML.  
  
### <a name="retrieving-for-xml-query-results-as-xml-type"></a>Recupero dei risultati di una query FOR XML come tipo xml  
 La query seguente recupera le informazioni di contatto del cliente dalla tabella `Contacts` . Poiché in `TYPE` è specificata la direttiva `FOR XML`, il risultato viene restituito come tipo `xml`.  
  
```  
USE AdventureWorks2012;  
Go  
SELECT BusinessEntityID, FirstName, LastName  
FROM Person.Person  
ORDER BY BusinessEntityID  
FOR XML AUTO, TYPE;  
```  
  
 Risultato parziale:  
  
 `<Person.Person BusinessEntityID="1" FirstName="Ken" LastName="S??nchez"/>`  
  
 `<Person.Person BusinessEntityID="2" FirstName="Terri" LastName="Duffy"/>`  
  
 `...`  
  
### <a name="assigning-for-xml-query-results-to-an-xml-type-variable"></a>Assegnazione dei risultati di una query FOR XML a una variabile di tipo xml  
 Nell'esempio seguente il risultato di una query FOR XML viene assegnato a una variabile di tipo `xml`, `@x`. La query recupera le informazioni di contatto, ad esempio la `BusinessEntityID`, `FirstName`, `LastName`, aggiuntive e i numeri di telefono dal `AdditionalContactInfo` colonna di `xml``TYPE`. Poiché la clausola `FOR XML` specifica la direttiva `TYPE`, il codice XML viene restituito come tipo `xml` e assegnato a una variabile.  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @x xml;  
SET @x = (  
   SELECT BusinessEntityID,   
          FirstName,   
          LastName,   
          AdditionalContactInfo.query('  
declare namespace aci="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactInfo";  
declare namespace act="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes";  
              //act:telephoneNumber/act:number') as MorePhoneNumbers  
   FROM Person.Person  
   FOR XML AUTO, TYPE);  
SELECT @x;  
GO  
```  
  
### <a name="querying-results-of-a-for-xml-query"></a>Esecuzione di una query sui risultati di una query FOR XML  
 La query FOR XML restituisce codice XML. È pertanto possibile applicare al risultato XML restituito dalle query FOR XML i metodi con tipo `xml`, ad esempio `query()` e `value()`.  
  
 Nella query seguente il metodo `query()` del tipo di dati `xml` viene utilizzato per l'esecuzione di una query sui risultati della query `FOR XML`. Per altre informazioni, vedere [Metodo query&#40;&#41; con &#40;tipo di dati XML&#41;](/sql/t-sql/xml/query-method-xml-data-type).  
  
```  
USE AdventureWorks2012;  
GO  
SELECT (SELECT BusinessEntityID, FirstName, LastName, AdditionalContactInfo.query('  
DECLARE namespace aci="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactInfo";  
DECLARE namespace act="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes";  
 //act:telephoneNumber/act:number  
') AS PhoneNumbers  
FROM Person.Person  
FOR XML AUTO, TYPE).query('/Person.Person[1]');  
```  
  
 La query interna `SELECT ... FOR XML` restituisce un risultato di tipo `xml` al quale la query esterna `SELECT` applica il metodo `query()` al tipo `xml`. Si noti la direttiva `TYPE` specificata.  
  
 Questo è il risultato:  
  
 `<Person.Person BusinessEntityID="1" FirstName="Ken" LastName="S??nchez">`  
  
 `<PhoneNumbers>`  
  
 `<act:number xmlns:act="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes">111-111-1111</act:number>`  
  
 `<act:number xmlns:act="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes">112-111-1111</act:number>`  
  
 `</PhoneNumbers>`  
  
 `</Person.Person>`  
  
 Nella query seguente il metodo `value()` con il tipo di dati `xml` viene utilizzato per recuperare un valore dal risultato XML restituito dalla query `SELECT...FOR XML`. Per altre informazioni, vedere [Metodo value&#40;&#41; &#40;tipo di dati XML&#41;](/sql/t-sql/xml/value-method-xml-data-type).  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @FirstPhoneFromAdditionalContactInfo varchar(40);  
SELECT @FirstPhoneFromAdditionalContactInfo =   
 ( SELECT BusinessEntityID, FirstName, LastName, AdditionalContactInfo.query('  
declare namespace aci="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactInfo";  
declare namespace act="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes";  
   //act:telephoneNumber/act:number  
   ') AS PhoneNumbers  
   FROM Person.Person Contact  
   FOR XML AUTO, TYPE).value('  
declare namespace act="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes";  
  /Contact[@BusinessEntityID="1"][1]/PhoneNumbers[1]/act:number[1]', 'varchar(40)'  
 )  
SELECT @FirstPhoneFromAdditionalContactInfo;  
```  
  
 L'espressione di percorso XQuery nel metodo `value()` recupera il primo numero di telefono di un cliente il cui `BusinessEntityID` è `1`.  
  
> [!NOTE]  
>  Se non si specifica la direttiva TYPE, il risultato della query FOR XML viene restituito come tipo `nvarchar(max)`.  
  
### <a name="using-for-xml-query-results-in-insert-update-and-delete-transact-sql-dml"></a>Utilizzo dei risultati di query FOR XML in istruzioni INSERT, UPDATE e DELETE (DML Transact-SQL)  
 Nell'esempio seguente viene illustrato l'utilizzo delle query FOR XML nelle istruzioni DML (Data Manipulation Language). Nell'esempio la query `FOR XML` restituisce un'istanza di tipo `xml`. L'istruzione `INSERT` inserisce il codice XML in una tabella.  
  
```  
CREATE TABLE T1(intCol int, XmlCol xml);  
GO  
INSERT INTO T1   
VALUES(1, '<Root><ProductDescription ProductModelID="1" /></Root>');  
GO  
  
CREATE TABLE T2(XmlCol xml)  
GO  
INSERT INTO T2(XmlCol)   
SELECT (SELECT XmlCol.query('/Root')   
        FROM T1   
        FOR XML AUTO,TYPE);   
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [FOR XML &#40;SQL Server&#41;](../xml/for-xml-sql-server.md)  
  
  
