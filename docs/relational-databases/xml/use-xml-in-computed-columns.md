---
title: Usare codice XML nelle colonne calcolate | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- computed columns, XML
- XML [SQL Server], computed columns
ms.assetid: 1313b889-69b4-4018-9868-0496dd83bf44
author: MightyPen
ms.author: genemi
ms.openlocfilehash: b11588e7f8a1e075b5091e73fe71879c7b035fd4
ms.sourcegitcommit: 68583d986ff5539fed73eacb7b2586a71c37b1fa
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/04/2020
ms.locfileid: "80664946"
---
# <a name="use-xml-in-computed-columns"></a>Utilizzo del codice XML nelle colonne calcolate
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Le istanze XML possono rappresentare o l'origine o il tipo di una colonna calcolata. Gli esempi contenuti in questo argomento mostrano come utilizzare il codice XML con le colonne calcolate.  
  
## <a name="creating-computed-columns-from-xml-columns"></a>Creazione di colonne calcolate da colonne XML  
 Ad esempio, nell'istruzione seguente `CREATE TABLE` una colonna di tipo `xml` (`col2`) viene calcolata da `col1`:  
  
```  
CREATE TABLE T(col1 varchar(max), col2 AS CAST(col1 AS xml) )    
```  
  
 Il tipo di dati `xml` può inoltre rappresentare l'origine per la creazione di una colonna calcolata, come illustrato nell'istruzione `CREATE TABLE` seguente:  
  
```  
CREATE TABLE T (col1 xml, col2 as cast(col1 as varchar(1000) ))   
```  
  
 È possibile creare una colonna calcolata mediante l'estrazione di un valore da una colonna di tipo `xml` , come illustrato nell'esempio seguente. Poiché non è possibile usare direttamente i metodi con tipo di dati **xml** per la creazione di colonne calcolate, nell'esempio viene definita innanzitutto una funzione (`my_udf`) che restituisce un valore da un'istanza XML. La funzione esegue il wrapping del metodo `value()` del tipo `xml` . Il nome della funzione viene quindi specificato nell'istruzione `CREATE TABLE` per la colonna calcolata.  
  
```  
CREATE FUNCTION my_udf(@var xml) returns int  
AS BEGIN   
RETURN @var.value('(/ProductDescription/@ProductModelID)[1]' , 'int')  
END  
GO  
-- Use the function in CREATE TABLE.  
CREATE TABLE T (col1 xml, col2 as dbo.my_udf(col1) )  
GO  
-- Try adding a row.   
INSERT INTO T values('<ProductDescription ProductModelID="1" />')  
GO  
-- Verify results.  
SELECT col2, col1  
FROM T  
  
```  
  
 Come il precedente, l'esempio successivo definisce una funzione per la restituzione di un'istanza con tipo di dati **xml** per una colonna calcolata. All'interno della funzione, il metodo `query()` con tipo di dati `xml` recupera un valore da un parametro del tipo `xml` .  
  
```  
CREATE FUNCTION my_udf(@var xml)   
  RETURNS xml AS   
BEGIN   
   RETURN @var.query('ProductDescription/Features')  
END  
```  
  
 Nell'istruzione seguente `CREATE TABLE` , `Col2` rappresenta una colonna calcolata che utilizza i dati XML (elemento`<Features>` ) restituiti dalla funzione:  
  
```  
CREATE TABLE T (Col1 xml, Col2 as dbo.my_udf(Col1) )  
-- Insert a row in table T.  
INSERT INTO T VALUES('  
<ProductDescription ProductModelID="1" >  
  <Features>  
    <Feature1>description</Feature1>  
    <Feature2>description</Feature2>  
  </Features>  
</ProductDescription>')  
-- Verify the results.  
SELECT *  
FROM T  
```  
  
### <a name="in-this-section"></a>Contenuto della sezione  
  
|Argomento|Descrizione|  
|-----------|-----------------|  
|[Promuovere i valori XML di uso frequente mediante colonne calcolate](../../relational-databases/xml/promote-frequently-used-xml-values-with-computed-columns.md)|Viene descritta la modalità di utilizzo della promozione della proprietà con colonne calcolate e tabelle delle proprietà.|  
  
  
